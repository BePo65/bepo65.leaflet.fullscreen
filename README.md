# @bepo65/leaflet.fullscreen
![Version](https://img.shields.io/badge/version-2.0.1-blue.svg?cacheSeconds=2592000)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/kefranabg/readme-md-generator/blob/master/LICENSE)

> leaflet.fullscreen is a clone of the project [brunob/leaflet.fullscreen](https://github.com/brunob/leaflet.fullscreen). Modifications were made to adapt it to the requirements of typescript users, e.g. for Angular (tested) and React (not tested).

## Objective
Simple plugin for Leaflet that adds fullscreen button to your maps.  
Inspired by http://elidupuis.github.com/leaflet.zoomfs/.

Uses the native javascript fullscreen API with help of https://github.com/sindresorhus/screenfull.js.

## Installation

__Typescript environments__:

```
npm i @bepo65/leaflet.fullscreen
```
This package includes the type definitions needed for typescript environments.


__Plain javascript environments__:

Include `screenfull.js`, `Control.FullScreen.js` and `Control.FullScreen.css` in your page. The package `screenfull.js` **must** stand before `Control.FullScreen.js` and can be loaded from a CDN:

``` html
 <link rel="stylesheet" href="Control.FullScreen.css" />
 <script src="https://cdnjs.cloudflare.com/ajax/libs/screenfull.js/5.1.0/screenfull.min.js"></script>
 <script src="Control.FullScreen.js"></script>
```

## Example for usage

If your map has a zoomControl, the fullscreen button will be added at the bottom of this one.  
If your map doesn't have a zoomContron, the fullscreen button will be added to topleft corner of the map (same as the zoomcontrol; defined by the `position` option).

If you want to use the plugin on a map embedded in an iframe, don't forget to set `allowfullscreen` attribute on your iframe.


__Typescript environments__:

Add the fullscreen control to the map:

``` js
import * as leaflet from 'leaflet';
import '@bepo65/leaflet.fullscreen';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements AfterViewInit {
  private map: leaflet.Map;

  // configuration of initial map
  private readonly osmDe = {
    url: 'https://{s}.tile.openstreetmap.de/{z}/{x}/{y}.png',
    options: {
      detectRetina: true,
      maxZoom: 18,
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }
  };
  private mapOptions: leaflet.MapOptions = {
    layers: [
      leaflet.tileLayer(this.osmDe.url, this.osmDe.options)
    ],
    center: leaflet.latLng([47.732889, 11.8123253]),
    zoomControl: true,
    zoomSnap: 0.25,
    zoom: 10,
    fullscreenControl: true,
    fullscreenControlOptions: {
      position: 'topleft',
      title: 'fullscreen map',
      titleCancel: 'exit fullscreen display'
    }
  } ;

  ngAfterViewInit(): void {
    this.map = new leaflet.Map('map', this.mapOptions);
    this.map.on('enterFullscreen', () => console.log('enterFullscreen'));
    this.map.on('exitFullscreen', () => console.log('exitFullscreen'));
  }
}
```

__Plain javascript environments__:

Add the fullscreen control to the map:

``` js
var map = new L.Map('map', {
  fullscreenControl: true,
  fullscreenControlOptions: {
    position: 'topleft'
  }
});
```

## Events of leaflet.fullscreen

``` js
map.on('enterFullscreen', () => {
  console.log('entered fullscreen');
});

map.on('exitFullscreen', () => {
  console.log('exited fullscreen');
});
```

## Methods of leaflet.fullscreen

``` js
  // you can also toggle fullscreen from map object
  map.toggleFullScreen();

// create a fullscreen button and add it to the map
L.control.fullscreen({
  position: 'topleft',
  title: 'Show me the fullscreen !',
  titleCancel: 'Exit fullscreen mode',
  content: null,
  forceSeparateButton: true,
  forcePseudoFullscreen: true,
  fullscreenElement: false
}).addTo(map);
```

## Options of leaflet.fullscreen

``` js
position: 'topleft', // change the position of the button can be topleft, topright, bottomright or bottomleft, defaut topleft
title: 'Show me the fullscreen !', // change the title of the button, default Full Screen
titleCancel: 'Exit fullscreen mode', // change the title of the button when fullscreen is on, default Exit Full Screen
content: null, // change the content of the button, can be HTML, default null
forceSeparateButton: true, // force seperate button to detach from zoom buttons, default false
forcePseudoFullscreen: true, // force use of pseudo full screen (show fullscreen in element and not in whole browser window) even if full screen API is available, default false
fullscreenElement: false // Dom element to render in full screen, false by default, fallback to map._container
```

## Where to find more information
Source code : https://github.com/BePo65/leaflet.fullscreen

Demo with plain javascript : https://BePo65.github.com/leaflet.fullscreen/

External dependencies : https://www.npmjs.com/package/screenfull

## Changelog
For list of changes and bugfixes, see [CHANGELOG.md](CHANGELOG.md).

## Contributing
The [CHANGELOG.md](CHANGELOG.md) is generated with `standard-changelog` (`npm run release`).
The following is the list of supported scopes:
* fullscreen
* none/empty string: useful for test and refactor changes that are done across all packages (e.g. test: add missing unit tests) and for docs changes that are not related to a specific package (e.g. docs: fix typo in tutorial).

## Author

**Bernhard Pottler**

  on Github: [@BePo65](https://github.com/BePo65)


## License

Copyright © 2021 [Bernhard Pottler](https://github.com/BePo65).

This project and all of its packages are released under [MIT](https://github.com/BePo65/leaflet.fullscreen/blob/master/LICENSE) license.
