scout
=====

this was developed because i needed (wanted) a simple way to fire javascript through incoming html, without any extra requests. it should run fine on any modern browser ( chrome, ff 3.5+, opera 10+, ie 9+, safari 3.2+ ).

now compatible with (but does not require) jquery, zepto, and jqmobi/intel app framework. others will be added as needed. testing for window.$ is avoided because it could break things. if a compatible library is detected, scout will use the selector engine built in to it, which enables pseudo selectors not available to native javascript. 

for example, let's say you have a basic website using ajax which returns plain html from a server.

> one of the pages could look like this
>
> ```html
> <p data-subscribe="foo">i am a paragraph, yet i contain very little information.</p>
> ```

&nbsp;

> to setup a trigger with scout, you could do
>
> ```javascript
> scout.on( '[data-subscribe]', function ( element, index )
>     {
>         // let's pretend the subscribe function subscribes the client to a websocket channel
>         subscribe( element.getAttribute( 'data-subscribe' ) )
> 
>         // client has subscribed to channel 'foo'
>     }
> )
> ```
> 
> when a new trigger is added, it will automatically check the page one time.

&nbsp;

> to manually check triggers, you have to tell scout when to look. for example, in an ajax or statechange handler.
> ```javascript
> $( '#foo' ).load( 'ajax.html', function ()
>     {
>         // ... do some stuff ...
> 
>         // passing no arguments checks all of the triggers
>         scout.check()
> 
>         // passing a string will check for specific selectors that have already been defined
>         scout.check( '.bar' )
>     }
> )
>
> $( window ).on( 'statechange', function ( e )
>     {
>         // ... do some stuff ... 
>         
>         scout.check()
>     }
> )
> ```

chainable for your convenience
> ```javascript
> scout
>     .on( '.foo', doClass )
>     .on( '[data-bar]', doAttribute )
>     .once( '#once', doIdOnce )
> ```

license
----

The MIT License (MIT)

Copyright (c) 2014 kevin von flotow
