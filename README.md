# Elkins
_A bookmarklet for easy script injection_

Can't put JavaScript `href` links in GFM. Here's the code

```js
javascript:!function(o){function n(o,n){var e=o.reduce(function(o,n){return o[n]=1,o},{});return n.filter(function(o){return!e[o]})}function e(o){var n=[].lastIndexOf.call(o,".");return n>-1?o.slice(n+1):null}function t(o){var n=document.createElement("link");n.rel="stylesheet",n.href=o,document.head.appendChild(n)}function r(o,n){var e=new XMLHttpRequest;e.open("GET",o),e.onreadystatechange=function(){4===e.readyState&&n(e.response)},e.send()}function a(o,e,t){function r(){document.body.removeChild(a),a=null}var a,c=Object.keys(window);a=document.createElement("script"),a.src=o,a.onload=function(){var t=n(c,Object.keys(window));e&&e(o,t),r()},a.onerror=function(){t&&t(o),r()},document.body.appendChild(a)}function c(o){throw new Error("Script failed to load at "+o)}function s(o,n){console.log("Script loaded at "+o),n&&console.log("Globals created: "+(n.length?n.join(", "):"NONE"))}function l(o,n,r){var l=e(o);if(null==n&&(n=s),null==r&&(r=c),"js"===l)a(o,n,r);else{if("css"!==l)throw new Error("No method for resource "+o);t(o)}}function i(o){if(!j[o])throw new Error(o+" not found. Open a pull request.");return Array.isArray(j[o])?j[o].forEach(l):"string"==typeof j[o]?l(j[o]):void 0}function d(o){var n=m+o;a(n,s,c)}function u(o){var n=o.split("/"),e=n[0],t=n[1],l=n[2]||"master",i=[e,t,l].join("/");r(m+i+"/bower.json",function(o){var n=JSON.parse(o);console.log("bower.json loaded");var e=n.main;"."===e.charAt(0)&&(e=e.slice(1));var t=m+i+e;a(t,s,c)})}var m="https://rawgit.com/",j={jquery:"https://code.jquery.com/jquery-1.11.1.min.js",underscore:"http://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.7.0/underscore-min.js",lodash:"http://cdnjs.cloudflare.com/ajax/libs/lodash.js/2.4.1/lodash.min.js",backbone:"http://cdnjs.cloudflare.com/ajax/libs/backbone.js/1.1.2/backbone-min.js",angular:"http://cdnjs.cloudflare.com/ajax/libs/angular.js/1.2.20/angular.min.js",ember:"http://cdnjs.cloudflare.com/ajax/libs/ember.js/1.7.0/ember.min.js",react:"http://cdnjs.cloudflare.com/ajax/libs/react/0.11.2/react.min.js",moment:"http://cdnjs.cloudflare.com/ajax/libs/moment.js/2.8.3/moment.min.js",d3:"http://cdnjs.cloudflare.com/ajax/libs/d3/3.4.11/d3.min.js",bootstrap:["http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css","http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"]},f={library:i,ghPath:d,bower:u};"undefined"!=typeof module?module.exports=f:o.Elkins=f}(this);
```

The script provides a browser global at `Elkins`.

## Methods

### `.library(String name)`
I hardcoded CDN links to a few popular libraries. Here's what's available:
- `jquery`
- `underscore`
- `lodash`
- `moment`
- `d3`
- `backbone`
- `angular`
- `ember`
- `react`

This will probably change to `.lib.jquery()`, `lib.d3()`, etc. There's more discoverability as to what's available that way. Open a PR to add more.


### `.bower(String id)`
`id` should be the GitHub repo identifier for a package with a valid `bower.json` file. For instance, `mbostock/d3`. This only really works for packages that have a built version checked into GitHub. jQuery, for example, doesn't have one.

### `.ghPath(String path)`
Loads a file from GitHub. `path` should look like `user/repo/branch/path/to/file.js`. This will change soon to allow omitting branch, or to allow including `blob` as it appears in the GitHub web app.

## Why "Elkins"?

Nurse Elkins from [The Knick](http://en.wikipedia.org/wiki/The_Knick) is pretty good at injections.

<img src="https://dl.dropboxusercontent.com/u/26194775/img/theknick_cinemaxpromo__twocolumncontent.jpg">

