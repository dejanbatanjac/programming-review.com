---
layout: post
title:  "Customize images layout in WordPress"
date:   2017-01-08 03:39:33 +0100
categories: wordpress themes images
---
>***In WordPress I need every image to be right aligned. Also, clicking the image should open the full image. How to achieve that?***

This would be the code you need to set inside your theme:

``` php 
add_action( 'after_setup_theme', '_20170108_setup' );

function _20170108_setup() {
    update_option( 'image_default_align', 'right' );
    update_option( 'image_default_link_type', 'file' );
}
```

[WP Codex](https://codex.wordpress.org/Option_Reference)
