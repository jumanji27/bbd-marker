jQuery Bounding Boxes with Dot Marker
===================

*Based on [jQuery-select-areas](https://github.com/360Learning/jquery-select-areas) by [360learning](https://360learning.com) and have very similar params and integration.*

![jQuery-bbd-marker Preview](https://raw.githubusercontent.com/jumanji27/jquery-bbd-marker/master/promo.png)

jQuery-bbd-marker is a jQuery plugin that let you select multiple areas of an image with dot,
move them and resize them.

# Quick Start

## Use like so:

    $("#mypic").BBDMarker({
      minSize: [30, 30],    // Minimum size of a selection
      maxSize: [400, 300],  // Maximum size of a selection
      onChanged: $.noop,    // Fired when a selection is released
      onChanging: $.noop,   // Fired during the modification of a selection
      areas: [ ... ]        // Predifined areas, see below
      // And many others params, see example/example.html
    });


## Want an example to learn from?
see *example/example.html*

## Browser Compatibiilty:
This plugin is fully compatible with every modern browser and IE >= 9.

One of the features : scaling image, in order to display it smaller or bigger than it actually is, is not compatible with IE8.
If you need to use this feature and to maintain a compatibility with IE8, you can add the alternate stylesheet *src/jquery.bbd.marker.ie8.css*.
This will make it work but uglify the whole plugin. This stylesheet can be added for IE8 only with conditional comments (see *example/example.html*).

# API Doc

## Area
An area is described (when retrieved or set) by a json object:

    {
        id, // ID identifying the area in the plugin
        x,  // X coordinate (Position)
        y,  // Y coordinate (Position)
        z,  // Z-index (0 when inactive or 100 when focused)
        width,  // Width of the area (Size)
        height,  // Height of the area (Size)
        dot: { // dot
          x, // X coordinate relatively bounding box (area)
          y, // Y coordinate relatively bounding box (area)
          touched // will be true if dot is already changed position
        }
    }

## Dot
if frame is disabled:

    {
        id, // ID identifying the area in the plugin
        z,  // Z-index (0 when inactive or 100 when focused)
        dot: { // dot
          x, // X coordinate relatively bounding box (area)
          y, // Y coordinate relatively bounding box (area)
          touched // will be true if dot is already changed position
        }
    }

## Options
Here is a list of available options for BBDMarker, with their *default value*:

- **allowEdit** (*true*): When set to false, unset allowMove, allowResize, allowSelect and allowDelete
- **allowMove** (*true*): When set to false, Areas can not be moved with a drag & drop.
- **allowFrame** (*true*): When set to false, will be only the dot.
- **allowDot** (*true*): When set to false, Area will be without the dot.
- **allowDotMove** (*true*): When to false, dot can not be moved.
- **allowResize** (*true*): When set to false, Areas can not be resized.
- **allowSelect** (*true*): When set to false, Areas can not be created.
- **allowDelete** (*true*): When set to false, Areas can not be deleted.
- **allowNudge** (*true*): When set to false, Areas can not be moved with arrow keys.
- **aspectRatio** (*0*): When not 0, force a ratio between height and width for the selections.
- **minSize** (*[40, 40]*): When not 0, set the minimum size for a selection [width, height]
- **maxSize** (*[0, 0]*): When not 0, set the maximum size for a selection [width, height]
- **maxAreas** (*0*): When not 0, set the maximum number of area that can be drawn.
- **outlineOpacity** (*0.5*): opacity of the moving dotted outline around a selection.
- **overlayOpacity** (*0.5*): opacity of the overlay layer over the image
- **areas** (*[]*): list of areas to add to the image from the beginning  (id will be ignored)
- **onChanging** (*null*): triggered when the event "changing" is fired
- **onChanged** (*null*): triggered when the event "changed" is fired
- **onLoaded** (*null*): triggered when the event "loaded" is fired
- **width** (*0*): When not 0, scale the image to this width (px). The coordinates of the areas on the full image can be retrieved with method getRelativeAreas()
- **settingTexts** (*['Delete', 'Delete Frame']*): Texts for settings menu

## Events
Three events are fired by the plugin:
- **loaded** : fired when plugin is loaded
- **changing** : fired during the modification of a selection. arguments : (event, id, areas)
- **changed**  : fired when a selection is released. arguments : (event, id, areas)

## Methods
Once you added a *BBDMarker* plugin on an image, several method are exposed to help you
manipulate and retrieve these areas:
- **getAreas ()** : returns an array of areas
- **getRelativeAreas ()** : returns an array of areas, with their size and coordinates on the original image (see option width). Equal to getAreas() when the image is displayed in full size.
- **add (options)** : add an area
- **remove (id)** : remove an area with its id
- **reset ()** : remove all areas
- **destroy ()** : remove the *BBDMarker* plugin
- **blurAll ()** : blur (unfocus) all the areas
- **contains (point)** : return true or false whether or not a point ({x: X, y: Y}) is included in at least one area
