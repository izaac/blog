---
layout: post
title:  "Personal starter repository for WebdriverIO configurations"
date:   2017-10-14 12:48:00
categories: career javascript nodejs selenium webdriverio
---
I've been using a lot this [WebdriverIO](http://webdriver.io) library to design functional end to end and regression tests
lately, when I started with it I was using old pre-ES6 syntax and even mixed [ES6](http://exploringjs.com/es6/) with vanilla syntax, however now I feel more familar with all the transpilers and in how the JS tools allow me to
use classes for OOP (which it's just [syntactic sugar](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) for Prototypes) in JavaScript.

So after some time I decided to create this [wdioTraining](https://github.com/izaac/wdioTraining) repo to have a reference for historical purposes in case I want not to start from scratch a new project.

I'm including the babel dependencies, WebdriverIO services modules and extra stuff like cloud services integration like [Sauce Labs](https://saucelabs.com) and [TravisCI](https://travis-ci.org), making it publicly available in the process in case anyone else wants to take a look at it, I'm also using simple [Mocha](http://mochajs.org) spec and a few examples of [Page Objects in WebdriverIO](https://github.com/webdriverio/webdriverio/issues/356) all using the ES6 syntax.

As part of the example I'm using a simple search in a travel website, but I plan to maybe switch on using Wikipedia searches instead, just to use an open source website. Hope it's of some help for someone.