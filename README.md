RIMG
====

This library supports responsive websites to provide a way to optimize images (like CMS-content) in a simple and performant way. Pure Javascript, no server-side code and 2 lines of code (library + definition).

It is based on the idea that when the DOM is loaded, it will traverse the DOM, looking for ```<img>```-nodes, and alter the ```src```-property. You can also manually execute this task, see the documentation.
Rimg uses an adapted version of the [srcset](http://www.w3.org/html/wg/drafts/srcset/w3c-srcset/) specification, while you don't need to define with every image 3(+) breakpoint-images. Just provide the image-basename and let Rimg do the adjustments.

# Getting Started
1. Define custom filenaming strategy, like `-tiny`, `-small`, `-medium`, `-large` and `-huge` to have a clear distinction between all breakpoint-steps.
2. Define initial breakpoints, like 
```javascript
var RimgBreakpoint = '-tiny 320w 1x, -small 480w 1x, -small-retina 480w 2x,
-medium 600w 1x, -medium-retina 600w 2x, -regular 768w 1x, -regular 768w 2x, 
-large 1024w 1x, -large-retina 1024w 2x, -huge w 1x';
``` 
before you load the minified version of Rimg.

3. Load the script, like ```<script src="https://raw.github.com/joeyvandijk/rimg/rimg.min.js"></script>```. You can put it before the ```</body>``` or before the ```</head>``` tags.

will result in something like:

```html
<script>
var RimgBreakpoint = '-tiny 320w 1x, -small 480w 1x, -small-retina 480w 2x, -medium 600w 1x, -medium-retina 600w 2x, -regular 768w 1x, -regular 768w 2x, -large 1024w 1x, -large-retina 1024w 2x, -huge w 1x';</script>
<script async src="//cdnjs.com/rimg"></script>
...
<img data-src="image.jpg"/>
```

Now you have a working setup that will check your DOM-element dimensions to determine which image-file suits best to show in your HTML page.

To see the examples in the `/test`-directory, go to your commandline:
* go the `/test`-directory
* type `npm install` ([nodejs](http://nodejs.org) needed!)
* type `node server.js` and go to `localhost:8080` 

to see the examples.

## Dependencies
* [Mediaqueries](http://caniuse.com/#feat=css-mediaqueries) support in the browser you want to support.
* A clear **filenaming strategy** that you will use with all your image-filenames you use.
* Use **CSS** or ```style=""``` to adjust ```<img>``` dimensions and Rimg will only listen to that values.


# Documentation

## Features
* responsive images that respond to **retina**-screens, **browser-resizes**, **DOMContentLoaded**-events and **DOM-changes**
* **reconfigure** after Rimg is loaded/executed by using ```Rimg.configure(breakpoints);``` 
* **disable** auto introspection, so only **manually** adjustable by using ```Rimg.configure(breakpoints);``` and ```Rimg.execute(targetElement);```
* only ```<img>``` elements with ```data-src``` property will be adjusted by Rimg, so implement on one, some or all images.
* pure frontend (**javascript**) solution and no server-side setup/code is necessary.
* **art direction support**, respect the chosen filenaming strategy and alter your ```<img>``` in any way (square?) and save the file (square?) used in that breakpoint and everything works!

## API
* **Rimg.execute(target)** (Element) - provide a DOM element to determine if it is or has ```<img>``` elements to change.
* **Rimg.configure(breakpoints)** (String) - provide the breakpoints so Rimg can determine which picture to use.
* **Rimg.disableIntrospection()** - prevents scan for images after a DOM-load or DOM-changes or a resize, so manually select <img> to adjust.
* Use the example below before loading the script itself to set initial breakpoints. 

```javascript
var RimgBreakpoint = '-small 480w 1x, -small-retina 480w 2x, -regular 768w 1x, 
-regular 768w 2x, -large 1024w 1x, -large-retina 1024w 2x';
``` 

## Breakpoints
Define a custom filenaming setup. It is based on the [srcset](http://www.w3.org/html/wg/drafts/srcset/w3c-srcset/) specification. For example:

```html
<img data-src="image.jpg"/>
```

will become 

```html
<img src="image-small.jpg" data-src="image.jpg"/>
```

in the situation it uses the `-small 480w 1x` breakpoint you defined for example. `image.jpg` is non-existent but the base filename to use with all images.

The used ```var RimgBreakpoint = '-small 480w 1x, -small-retina 480w 2x, -regular 768w 1x, -regular 768w 2x, -large 1024w 1x, -large-retina 1024w 2x';``` gives you all the freedom by defining 1 (or more) breakpoints with the flexibility to add specific image-files for retina-screens like the iPad, iPhone or Samsung Galaxy Sxxx, etc. 

You may skip the retina option or skip certain breakpoints (`480w` or `768w`) or even add weird ones (like ```-special 456w 1x```).

The `w` in `480w` defines the width property to check. During development of responsive websites I haven't found many examples to use `h` for the height, but I did found issues with javascript returning `0` as the height of non-loaded images. Even when the height is set in `%`.
This is why I provide the option to use `480h` but I do **advise to use the width as a breakpoint** (kind of best practice).

# Examples
See the ```/test``` directory for more information how to use this library.


# Contributing
Please do test, check and come with pull requests/issues to further extend/stabilize this library.


# Changelog
0.1.0 initial release

# FAQ
See the [Wiki](https://github.com/joeyvandijk/rimg/wiki/FAQ) for more information.

# TODO
- [ ] (optional) bandwidth detection solution
- [ ] (optional) srcset support
- [ ] tests/examples for retina-support
- [ ] (optional) namespace change 
- [ ] FAQ on the wiki explaining my choices
- [ ] add to https://github.com/cdnjs/cdnjs
- [ ] last option - retina detection
- [ ] use issues: remove remark or not?
- [ ] data-src changed (not-cross browser support?)
- [ ] (optional) code refactoring (async?)