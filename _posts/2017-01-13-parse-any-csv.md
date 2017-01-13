---
layout: post
title:  "Parse any csv into HTML"
date:   2017-01-13 03:39:33 +0100
categories: JavaScript
---
It is hard to create good CSV parser but using NodeJS `fast-csv` this is not hard at all.

| name    |	address    |	stars |	contact	| phone	| uri |
|---------|------------|----------|---------|-------|-----|
|Bond	   Bond Street 007 | 	5	| Ian Fleming	| 1-270-665 |	http://www.007.com/contact/ |


```javascript
/**
 * CSV processor based on fast-csv
 * Author: Dejan Batanjac
 *
 */
var fs = require( 'fs' );
var parser1 = require( 'fast-csv');
var XRegExp = require( 'xregexp' );
var validUrl = require( 'valid-url' ); // alternative https://github.com/chriso/validator.js


/**
 * This function should return false if the string buffer contains non UTF8 characters.
 * @param  string buffer
 * @return boolean true|false
 * http://stackoverflow.com/questions/17006799/how-do-i-capture-utf-8-decode-errors-in-node-js
 */
function isValidUTF8( buf ) {
    return Buffer.compare( new Buffer( buf.toString(), 'utf8' ), buf ) === 0;
}

var stream = fs.createReadStream( 'anything.csv' );

/**
 * Fast-csv parsing options as defined https://www.npmjs.com/package/fast-csv.
 */
var parsingOptions = {
    headers: true,
    trim: true,
    objectMode: true,
    ignoreEmpty: true,
    strictColumnHandling: true
};

var outputFile1 = 'out1.json';
if ( fs.existsSync( outputFile1 ) ) {
    fs.unlink( outputFile1 );
}
/**
 * Make sure the end file uses utf8 encoding and we open a file so we can append.
 */
var fileOptions = {
    encoding: 'utf8',
    flag: 'a'
};

/**
 * The main essence of the parser1 is the validate part.
 * We have three conditions in there as per our request.
 * In case we have invalid data we don't write JSON to the
 * outputFile1.
 */
parser1
    .fromStream( stream, parsingOptions )
    .validate( function( data ) {
        var validateStatus = false;
        var condition1 = validUrl.isUri( data['uri'] );
        var i = parseInt( data['stars'] );
        var condition2 = Number.isInteger( i ) && i > 0 && i < 6;
        //var unicodeWord = XRegExp(''); // haven't had time.
        //var condition3 = unicodeWord.test(data['name']);
        var condition3 = isValidUTF8( new Buffer( data['name'] ), 'utf8' );
        return validateStatus = ( condition1 && condition2 && condition3 );

    })
    .on('data-invalid', function(data) {
        console.log( 'Invalid data detected' );
        console.log( data );
        //process.exit(1);
    })
    .on( 'data', function( data ) {
        fs.writeFile( outputFile1, JSON.stringify( data, null, 2 ), fileOptions );
        console.log( data );
    })
    .on( 'end', function() {
        console.log('done');
    });

    // another output now in HTML
    var outputFile2 = 'out2.html';
    if ( fs.existsSync( outputFile2 ) ) {
        fs.unlink( outputFile2 );
    }
    fs.writeFile( outputFile2, '<!DOCTYPE html><html lang="en"><head>	<meta charset="UTF-8">	<title>Document</title></head><body>', fileOptions );
```
