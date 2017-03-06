# We want to have the same hight for every div in a row in our layout
This instruction is just for me and for Zikula usage. The module should be made with modulestudio

## Preparation

### Download
we choose the jquery tool jquery.matchHight.js
https://github.com/liabru/jquery-match-height

### where to save
I place it normally in the folder ``additions/jquery.matchHeight/jquery.matchHeight.js``

### How to let Zikula know where it is
The best place to add new assets is in the ``/views/base.html.twig``.

you have to address it as following:
``{{ pageAddAsset('javascript', asset('../additions/jquery.matchHeigt/jquery.matchHeight.js')) }}``
The ``../`` is needed because zikula normally expects the assets in the folder ``web``

## Implementation

### Javascript
I found this post very helpfull:
http://stackoverflow.com/questions/30912069/jquery-match-height-not-working-on-first-row

I created (with the help of a Guru) an additional .js file:

````
'use strict';

(function($) {
    function updateDivHeights() {
        $('.row').each(function(i, elem) {
            jQuery(elem)
                .find('.box-item .white-space')   // Only children of this row
                .matchHeight({byRow: true}); // Row detection gets confused so disable it
        });
    }

    $(document).ready(function() {
        updateDivHeights();
        $(document).resize(updateDivHeights);
    });
})(jQuery)
````

This I store in the file ``pulic/js/RKShowRoomModule.box-item.js``
In the ``base.html.twig`` you have to add this as well:
``{{ pageAddAsset('javascript', zasset('@RKShowRoomModule:js/RKShowRoomModule.box-item.js')) }}``

### Templating

In templates it is now very simple. You have to add to your raster divs the ``class="box-item"`` and to the divs you want to have the same hight ``class="white-space"``. white-space is in my case something I configured some background css for my site. You can use other classes as well. In the stackoverflow example they used the bootstratp well instead.

Thats it!

