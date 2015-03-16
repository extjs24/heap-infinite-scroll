# heap-infinite-scroll
### version 1.0.1
### Vladimir Neginskiy
## [Examples](http://extjs24.github.io/heap-infinite-scroll/)

### Installation
Include tag for styles in your HTML file:

    <link href="/path/to/heap-infinite-scroll.css" media="screen" rel="stylesheet" type="text/css">

Include script after the jQuery library:

    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js"></script>
    <script type="text/javascript" src="/path/to/jquery.heap-infinite-scroll-1.0.1.min.js"></script>

### Usage

Create and bind plugin to the container in two ways

In the style of jQuery:

    var scroll = $('container-selector').heapInfiniteScroll({options});

Or in the style of Object:

    var scroll = new HeapInfiniteScroll('container-selector', {options});

### Options

The plugin has the following settings with the default values:

    {
        margin: 10,
        maxCount: 200,
        height: 200,
        timeout: 2000,
        frame: true,
        frameWidth: 'auto',                 // 'auto' | numeric
        size: 'proportional',               // 'proportional' | 'square'
        compact: true,
        url: null,                          // null | string | function(load) {... load(items)}
        autoload: false,
        urlField: 'url',
        descriptionField: 'description',
        htmlField: 'html',
        oncallback: null,                   // null | function(item) {... return params;}
        continueMsg: '+ View more?',
        notFoundMsg: 'Infos not found!',
        noMoreMsg: 'No more infos!',
        downloadIcon: '&#8987;',            // html
        crollbar: null,
        scrollbarVisible: true,
        onclick: null,                      // null | function(item) {...}
        onerror: null,                      // null | function(url) {...}
        onframeshow: null                   // null | function(content) {...}
    }

#### Parameter Url

URL parameter indicates the source of a list of items displayed and can be a string or a function.

    {
        ...,
        url: 'http://foo.com... ',
        ...
    }
    
As the function it must be in the form:

    {
        ...,
        url: function(callback) {
            ...
            // loading items
            ...
            callback(items)
        },
        ...
    }

Url- function parameter is callback- function which it is necessary to pass an array of loaded items

description made later