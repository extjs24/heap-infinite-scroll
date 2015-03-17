# heap-infinite-scroll
### plugin for jQuery (1.11.2 or later)
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
        scrollbar: null,
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

Url- function has a parameter is callback- function which it is necessary to pass an array of loaded items

Furthermore, an URL can be an object that already has an interface function with the name execute:

    var obj = {
        execute: function(callback) {
                ...
                // loading items
                ...
                callback(items)
            }
        };
        
    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            url: obj,
            ...
        });
        
So used HeapGoogleSearch ([Examples](http://extjs24.github.io/heap-infinite-scroll/))

    var search = new HeapGoogleSearch();
    
    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            url: search,
            ...
        });

#### Event oncallback

Loaded with a list of items iterated through and displayed. 
If each item is a string, it is regarded as the image address.
If you need additional conversion item, it is necessary to use an event onchallbask, 
which is the parameter item. 
Event should return an object with the necessary parameters to display:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            oncallback: function(item) {
                return {
                    description: item.content
                };
            },
            ...
        });

Returns the parameters for the images, if they are not present in the item or they have to be converted must be:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            oncallback: function(item) {
                return {
                    url: 'http://foo.com/image.png', // image address
                    description: item.content        // description of the item for the selection frame
                };
            },
            ...
        });


If these parameters are already in the cell, but under a different name, you can simply specify the appropriate values in the parameters:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            urlField: 'src',
            descriptionField: 'declaration'
            ...
        });
        
If the item is no 'urlField' field or for him the flag isHtml = true, then the element is not considered an image, 
and is accepted as html item. Then it is necessary to specify the contents of the 'html' field. You can also set the width of an html- item ([Example](http://extjs24.github.io/heap-infinite-scroll/news.html)):

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            oncallback: function(item) {
                return {
                    isHtml: true,
                    description: '....',
                    html: '.....',
                    width: Math.random()*100 + 100
                };
            },
            ...
        });

If you already have html content, but in a different field, then you can simply specify the appropriate value in the htmlField parameter:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...,
            htmlField: 'content',
            ...
        });

#### Other options

+ margin - the distance between the items,
+ maxCount - the maximum count of items in the cache,
+ height - the height of the display items,
+ timeout - time after which will be stopped loading images,
+ frame - the presence of the selection frame,
+ frameWidth - stroke width of the frame (default 'auto'),
+ size - ('proportional' | 'square') determines how the items ([Example](http://extjs24.github.io/heap-infinite-scroll/size-compact.html))
+ compact - (tru | false) determines compactness of the items ([Example](http://extjs24.github.io/heap-infinite-scroll/size-compact.html))
+ autoload - autoload data immediately after the creation of the component,
+ continueMsg - defines a text message when the maxCount number of items,
+ notFoundMsg - defines a text message if there is no information available on request to the server,
+ noMoreMsg - defines a text message if the information is available on request to the server was, and then at the same address ceased
+ downloadIcon - (default hourglass symbol) html icons download data,
+ scrollbar - defines a selector container scrollbars (default in the component) ([Example](http://extjs24.github.io/heap-infinite-scroll/out-scrollbar.html))
+ scrollbarVisible - determines whether the scroll bar,
+ onclick - event item click. Parameter - item,
+ onerror - error event. Parametr - error message,
+ onframeshow - show frame for the item. Parameter - content (jQuery object for the description) ([Example](http://extjs24.github.io/heap-infinite-scroll/custom-frame.html))
 


#### HeapInfiniteScroll - methods

HeapInfiniteScroll.add - add images or html elements:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...
        }),
        items = ['http://foo.com/image1.png', 'http://foo.com/image2.png', ...];
    
    scroll.add(items);

HeapInfiniteScroll.clear - remove all images or html elements:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...
        });
    ...
    
    scroll.clear();

HeapInfiniteScroll.load - load images or html elements from server:

    var scroll = new HeapInfiniteScroll('container-selector', {
            ...
        }),
        url = 'http://foo.com/images';
    ...
    
    scroll.load(url); // or scroll.load() if the url is already set in the options
    
HeapInfiniteScroll.draw - draw component, if no options are specified when creating

    var scroll = new HeapInfiniteScroll()
    ...
    
    scroll.draw('container-selector', options);
    

### Component HeapGoogleSearch

Added to the library component, allows you to search using Google Search.

    var search = new HeapGoogleSearch([type of search], [options]);
    
Identified the following types of search:

    HeapGoogleSearch.IMAGES; // - default value
    HeapGoogleSearch.WEB;
    HeapGoogleSearch.VIDEO;
    HeapGoogleSearch.BLOGS;
    HeapGoogleSearch.NEWS;
    HeapGoogleSearch.BOOKS;
    HeapGoogleSearch.PATENT;
    
Parameter options - options that might be present in the search query (Google Search API)

It has the following methods:

HeapGoogleSearch.execute([callback]) - triggers the start of the search results will be transferred callback- function.    
HeapGoogleSearch.setQuery(query) - defines the search string value query.    
HeapGoogleSearch.complete(handlers) - captures the handlers at the event get search results.

    var search = new HeapGoogleSearch(HeapGoogleSearch.NEWS),
        handler = function(result) {
            console.log(result);
            
            if (result.length) {
                search.execute();
            }
        };
        
    search.complete(handler);
    search.setQuery('art');
    search.execute();

