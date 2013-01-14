node-wgxpath
============

[Wicked Good XPath](http://code.google.com/p/wicked-good-xpath/) is a fast implementation of [document.createEvaluation](https://developer.mozilla.org/en-US/docs/DOM/document.createExpression) and [document.evaluate](https://developer.mozilla.org/en-US/docs/DOM/document.evaluate) ([DOM3-XPath](http://www.w3.org/TR/2004/NOTE-DOM-Level-3-XPath-20040226/DOM3-XPath.html)) in pure Javascript.

Version
------

I'm pretty lazy, so I didn't build Wicked Good XPath myself. When the pre-compiled [wgxpath.install.js](http://code.google.com/p/wicked-good-xpath/downloads/detail?name=wgxpath.install.js) is updated, I'll update this package.

`0.x.y`: `x` refers to the Google SVN revision when `wgxpath.install.js` was built, and any improvements to this library will be indicated by `y`.

Installation
------------

Install with [npm](http://npmjs.org/):

    npm install wgxpath

Example
-------

This example scrapes the Merriam-Webster Word of the Day. This code can also be found in the included `word_of_the_day.js`.

```javascript
var wgxpath = require('wgxpath');
var jsdom = require('jsdom');

var url = 'http://www.merriam-webster.com/word-of-the-day/';
var expressionString = '//*[@id="content"]/div[3]/ul/li[1]/strong';

jsdom.env({
  html: url,
  done: function(errors, window) {
    wgxpath.install(window);
    var expression = window.document.createExpression(expressionString);
    var result = expression.evaluate(window.document,
        wgxpath.XPathResultType.STRING_TYPE);
    console.log('The Word of the Day is "' + result.stringValue + '."');
  }
});
```

