---
layout: post
title:  "HTTP PRAGMA NO CACHE and CTRL + F5 to refresh your HTML"
date:   2017-01-16 03:39:33 +0100
categories: Browser
---

Note the `[HTTP_PRAGMA] => no-cache` part from the following array.

```
Array
(
    [USER] => www-data
    [HOME] => /var/www
    [HTTP_ACCEPT_LANGUAGE] => en-US,en;q=0.8,sr;q=0.6
    [HTTP_ACCEPT_ENCODING] => gzip, deflate, sdch
    [HTTP_ACCEPT] => text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    [HTTP_USER_AGENT] => Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.143 Safari/537.36
    [HTTP_UPGRADE_INSECURE_REQUESTS] => 1
    [HTTP_CACHE_CONTROL] => max-age=0
    [HTTP_PRAGMA] => no-cache
    [HTTP_CONNECTION] => keep-alive
    [HTTP_HOST] => test100.com
    [REDIRECT_STATUS] => 200
    [SERVER_NAME] => test100.com
    [SERVER_PORT] => 80
    [SERVER_ADDR] => 127.0.0.1
    [REMOTE_PORT] => 45406
    [REMOTE_ADDR] => 127.0.0.1
    [SERVER_SOFTWARE] => nginx/1.10.0
    [GATEWAY_INTERFACE] => CGI/1.1
    [REQUEST_SCHEME] => http
    [SERVER_PROTOCOL] => HTTP/1.1
    [DOCUMENT_ROOT] => /var/www/html/test100.com
    [DOCUMENT_URI] => /s.php
    [REQUEST_URI] => /s.php
    [SCRIPT_NAME] => /s.php
    [CONTENT_LENGTH] => 
    [CONTENT_TYPE] => 
    [REQUEST_METHOD] => GET
    [QUERY_STRING] => 
    [SCRIPT_FILENAME] => /var/www/html/test100.com/s.php
    [FCGI_ROLE] => RESPONDER
    [PHP_SELF] => /s.php
    [REQUEST_TIME_FLOAT] => 1484607355.2877
    [REQUEST_TIME] => 1484607355
)
```
I created this array via this PHP code

```php
<?php // s.php file
echo '<html>';
echo '<body style="background-color:gold">';
echo '<pre id="s">';
print_r($_SERVER);
echo '</pre>';
echo '</body>';
echo '</html>';
```
 The `[HTTP_PRAGMA] => no-cache` will be there only if you call `CTRL + F5`, else it will not be there.
 
 
