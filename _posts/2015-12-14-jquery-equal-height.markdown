---
layout: post
title: "jQuery ~ Equal Height"
date: 2015-12-14 14:41:56 -0400
comments: true
categories: jQuery
---

I know what you're thinking. This a problem that should be solved with CSS and not jQuery.
Well you're absolutely right. Come on WC3. Let's decide on that Flexbox spec already.

But until then.. Here's a little diddy about Jack and Diane.

jQuery

    var $equalHeight =  $('selector'); //selector you want to equalize height
    var maxHeight = 0;

    $($equalHeight).each(function() {

        if($(this).height() > maxHeight) {

            maxHeight = $(this).height();

        }

    });

    $($equalHeight).height(maxHeight);

The [codepen](http://codepen.io/jacobnlangley/pen/Qwdyog){:target="_blank"}
