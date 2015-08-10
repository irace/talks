# Node.js for mobile developers
## Bryan Irace

---

# What is Node.js?

> A platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.

---

# Not a web framework or language

--- 

# Components

* [V8](https://code.google.com/p/v8/) (Google's JavaScript engine)
* [libuv](https://github.com/joyent/libuv) (platform Independent I/O bindings)
* [Core libraries](http://nodejs.org/api/) (networking, modules, REPL, streams, logging)
* OpenSSL, etc.

--- 

# What's it good at?

* I/O
* Command line tools
* Not CPU-bound work

---

# Everything is asynchronous

---

# JavaScript

* [Easy to learn](http://www.codecademy.com)
* Powerful
* Runs everywhere (you need to know it anyway...)
* Always getting faster
* [Improving pretty rapidly](https://github.com/lukehoban/es6features)
* Lots of good libraries

--- 

# [NPM](https://www.npmjs.org)

##~70K modules

---

# package.json

```javascript
{
  "name": "lunchr",
  "version": "1.0.0",
  "dependencies": {
    "express": "3.4.3",
    "request": "2.27.0",
    "underscore": "1.6.0"
  }
}
```

---

# Importing

```javascript
var request = require('request');
var _       = require('underscore');
var qs      = require('querystring');
var express = require('express');
```

--- 

# Modules

* [jQuery](http://jquery.com)
* [Underscore](http://underscorejs.org)
* [Express](http://expressjs.com)
* [Async](https://github.com/caolan/async)
* [Request](https://github.com/mikeal/request)

---

# Express

```javascript
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('Hello, world');
});

app.listen(3000);
```

--- 

# Async

```javascript
async.parallel([
  function (callback) {
    ywa('1519698779', 'BOOKMARK_10135', callback);
  },
  function (callback) {
    play('com.tumblr', callback);
  }
], function (err, results) {
  if (err) {
    callback(err);
  }
  else {
    var ywa_data      = results[0]
      , play_rating   = results[1]

    // TODO
  }
}
```

--- 

# Request

```javascript
request({
  url: 'https://rink.hockeyapp.net/api/2/apps/' + app_id + '/statistics',
  headers: {
    'X-HockeyAppToken': '61c40d6b6fac43d880e97c0bd22b4903'
  }
}, function (err, response, body) {
  if (err) {
    callback(err);
  }
  else {
    var versions = JSON.parse(body)['app_versions'];

    // TODO
  }
}
```

--- 

# jQuery

```javascript
$('tr.stathead').remove();
$('tr').removeAttr('align').removeAttr('class');

$('tr:first').find('td').replaceWith(function () {
    return $('<th></th>')
        .html($(this).contents())
        .attr('data-week', index_of($(this)));
});
```

---

# Underscore

```javascript
_.chain([1, 2, 3, 200])
  .filter(function(num) { 
    return num % 2 == 0; 
   })
  .map(function(num) { 
    return num * num 
   })
  .value();
```

--- 

# shell.js

```javascript
require('shelljs/global');

if (!which('git')) {
  echo('Sorry, this script requires git');
  exit(1);
}

// Copy files to release dir
mkdir('-p', 'out/Release');
cp('-R', 'stuff/*', 'out/Release');

// Replace macros in each .js file
cd('lib');
ls('*.js').forEach(function(file) {
  sed('-i', 'BUILD_VERSION', 'v0.1.2', file);
  sed('-i', /.*REMOVE_THIS_LINE.*\n/, '', file);
  sed('-i', /.*REPLACE_LINE_WITH_MACRO.*\n/, cat('macro.js'), file);
});
cd('..');

// Run external tool synchronously
if (exec('git commit -am "Auto-commit"').code !== 0) {
  echo('Error: Git commit failed');
  exit(1);
}
```

---

# Hosting

* Easy to install
    * Windows
    * OS X (just a .dmg file)
* Easy to host
    * Heroku
    * Windows Azure

---

# Debugging

* [node-inspector](https://github.com/node-inspector/node-inspector)
