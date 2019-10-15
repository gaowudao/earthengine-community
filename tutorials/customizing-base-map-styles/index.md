---
title: Customizing base map styles
description: This tutorial shows how to change the base map properties in Earth Engine, which is useful if you want a specific visualization for functionality/convenience.
author: TC25
tags: Earth Engine, Base Map, UI, Widgets
date_published: 2019-10-11
---

[Open In Code Editor](https://code.earthengine.google.com/283c86dd3189788452b5fb64174a1b43)

The user is going to learn how to change the options of the map object to create new base maps

## The default maps in Earth Engine

Earth Engine's base maps are those in Google's Map API. The default options include:

- roadmap, which displays the default road map view,
- satellite, which displays Google Earth satellite images,
- hybrid, which displays a mixture of normal and satellite views, and
- terrain, which displays a physical map based on terrain information.

## Changing the basic map style

We can start by changing the style of the base map. One easy fix is to invert the lightness to get a darker background, like so:

```javascript

var baseChange = [
  "stylers": [ {"invert_lightness": true} ]
]

Map.setOptions("baseChange",{"baseChange":baseChange})

```
The main styler options include:

 - hue: indicates the basic color
 - lightness: indicates percentage change in brightness of an element
 - saturation: indicates percentage change in basic color of an element
 - gamma: gamma correction of an element (0.01 and 10.0)
 - invert_lightness: inverts the existing lightness
 - visibility: changes visibility options for an element (on, off, or simplified)
 - color: sets the color of an element (using RGB Hex Strings)
 - weight: sets the weight of a feature in pixels


## Changing map elements

The Google Maps API (and by extension, Earth Engine) gives you the ability to control a huge number of map features and elements.

The full list of elements that you can modify can be found in the Google Maps documentation: https://developers.google.com/maps/documentation/javascript/style-reference

The full list of features (also in the Google Maps API documentation linked above) includes geometries and labels (including their texts and icons). All styler options work with each of these features.

Let's consider a couple of examples to edit other elements and features

```javascript

//Remove icons
var iconChange = [{ // Change map saturation.
  "stylers": [{
    "gamma": .2
  }]
}, { // Change label properties.
  "elementType": "labels",
  "stylers": [{
    "visibility": "off",
    "color": "#000055"
  }]
}, { // Change road properties.
  "featureType": "road",
  "elementType": "geometry",
  "stylers": [{
    "visibility": "off",
    "color": "#000055"
  }]
}, { // Change road labels
  "featureType": "road",
  "elementType": "labels",
  "stylers": [{
    "visibility": "off"
  }]
}, { // Change icon properties
  "elementType": "labels.icon",
  "stylers": [{
    "visibility": "off"
  }]
}, { // Change POI options
  "featureType": "poi",
  "elementType": "all",
  "stylers": [{
    "visibility": "off"
  }]
}, {
  "featureType": "administrative",
  "elementType": "geometry.fill",
  "stylers": [{
    "visibility": "off"
  }]
}, {
  "featureType": "administrative",
  "elementType": "geometry.stroke",
  "stylers": [{
    "visibility": "off"
  }]
}];


//Enhanced road network visualization

var roadNetwork = [{
    "stylers": [{
      "saturation": -100
  }]
}, {
    "featureType": "road.highway",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#000055"
}, {
    "weight": 2.5
  }]
}, {
    "featureType": "road.highway",
    "elementType": "geometry.stroke",
    "stylers": [{
      "color": "#000000"
}, {
    "weight": 2
  }]
}, {
    "featureType": "road.arterial",
    "elementType": "geometry",
    "stylers": [{
      "color": "#FF0000"
}, {
    "weight": 1.8
  }]
}, {
    "featureType": "road.local",
    "elementType": "geometry",
    "stylers": [{
      "color": "#00FF55"
}, {
    "weight": 1.5
  }]
}];

Map.setOptions("roadNetwork", {
  "iconChange": iconChange,
  "roadNetwork": roadNetwork
});
```

![Road](https://github.com/TC25/earthengine-community/blob/patch-2/tutorials/customizing-base-map-styles/road.png?raw=true)

## Cheat codes

There is a way to create almost any base map you want without the hassle of tweaking any options. Enter [Snazzy Maps](https://snazzymaps.com), a community project for creating and sharing great styles for Google Maps. Copy any of the javascript properties from that website and it will show up on Earth Engine. Consider the two examples below:

```javascript


var snazzyBlack = [{
    "featureType": "administrative",
    "elementType": "all",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "administrative",
    "elementType": "labels.text.fill",
    "stylers": [{
      "color": "#444444"
  }]
},{
    "featureType": "landscape",
    "elementType": "all",
    "stylers": [{
        "color": "#000000"
},{
        "visibility": "on"
  }]
},{
    "featureType": "poi",
    "elementType": "all",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "road",
    "elementType": "all",
    "stylers": [{
        "saturation": -100
},{
        "lightness": 45
  }]
},{
    "featureType": "road",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#ffffff"
  }]
},{
    "featureType": "road",
    "elementType": "geometry.stroke",
    "stylers": [{
      "color": "#eaeaea"
  }]
},{
    "featureType": "road",
    "elementType": "labels",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "road",
    "elementType": "labels.text.fill",
    "stylers": [{
      "color": "#dedede"
  }]
},{
    "featureType": "road",
    "elementType": "labels.icon",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "road.highway",
    "elementType": "all",
    "stylers": [{
      "visibility": "simplified"
  }]
},{
    "featureType": "road.arterial",
    "elementType": "labels.icon",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "transit",
    "elementType": "all",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "water",
    "elementType": "all",
    "stylers": [{
        "color": "#434343"
},{
        "visibility": "on"
  }]
}];


var snazzyColor = [{
    "elementType": "labels",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "road",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#0F0919"
  }]
},{
    "featureType": "water",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#E4F7F7"
  }]
},{
    "elementType": "geometry.stroke",
    "stylers": [{
      "visibility": "off"
  }]
},{
    "featureType": "poi.park",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#002FA7"
  }]
},{
    "featureType": "poi.attraction",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#E60003"
  }]
},{
    "featureType": "landscape",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#FBFCF4"
  }]
},{
    "featureType": "poi.business",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#FFED00"
  }]
},{
    "featureType": "poi.government",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#D41C1D"
  }]
},{
    "featureType": "poi.school",
    "elementType": "geometry.fill",
    "stylers": [{
      "color": "#BF0000"
  }]
},{
    "featureType": "transit.line",
    "elementType": "geometry.fill",
    "stylers": [{
      "saturation": -100
  }]
}];

Map.setOptions("snazzyBlack", {
  "snazzyBlack": snazzyBlack,
  "snazzyColor": snazzyColor
})
```

![Dark](https://github.com/TC25/earthengine-community/blob/patch-2/tutorials/customizing-base-map-styles/snazzy-black.png?raw=true)

You can find out more about all the options in Google Maps API here: https://developers.google.com/maps/documentation/javascript/reference#MapTypeStyle