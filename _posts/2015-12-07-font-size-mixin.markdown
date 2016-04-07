---
layout: post
title: "Sass Font-Size Mixin"
date: 2015-12-07 14:41:56 -0400
comments: true
categories: Sass
---
Sass Mixin

    @function remCalc($size) { $remSize: $size / 16px; @return $remSize * 1rem; }

    @mixin font-size($size) { font-size: $size; font-size: remCalc($size); }

Implementation

SCSS

        nav {
          @include font-size(12px)    
        }

CSS Output

        nav {
          font-size: 12px; //will be overridden if REM is supported by browser
          font-size: 0.75rem;
        }
