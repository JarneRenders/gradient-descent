# Gradient Descent
A game of learning the concepts behind gradient descent by exploring the depths looking for treasure.

Developed for the I AM AI exhibiton by IMAGINARY.
Original concept by Aaron Montag.

## Configuration

The `config.json` file is loaded when opening the application. It supports the following keys:

- **defaultLanguage** (string, default: en): Default language to use. Can be overriden by the 
  `lang` query string.
- **useGamepads** (boolean, default: true): Enables gamepad use.
- **useScreenControls** (boolean, default: true): Shows on-screen controllers.
- **useKeyboardControls** (boolean, default: true): Control the game via keyboard (2 players only: <kbd>←</kbd><kbd>↓</kbd><kbd>→</kbd> and <kbd>A</kbd><kbd>S</kbd><kbd>B</kbd>).
- **maxPlayers** (integer, default: 2): Maximum number of players (between 1 and 4).
- **maxTime** (integer or string "Infinity", default: "Infinity"): Maximum number seconds until the game is over.
- **maxProbes** (integer or string "Infinity", default: "Infinity"): Maximum number of probes until the game is over.
- **continuousGame** (boolean, default: false): Skip the title screen and time limit, auto-restart.
- **debugControls** (boolean, default: false): Shows debugging data for controls.

## Remote controlling the game

The game adds a `game` object to the global scope.

### Setting a sea floor map

A sea floor map is just an array of numbers between 0 (close to the water surface) and 1 (distant
from the water surface). The array is used to generate a polyline from the left side of the screen
to the right having equidistant nodes at the elements of the map array.

Maps can be set via `game.setMap(map)`, e.g. setting a very simple V-shaped map could look like this:
```
game.setMap([0, 1, 0]);
```
A simple parabola-like map can be defined like so:
```
const parabola = t => 1 - Math.pow(2 * t - 1, 2);
const createMap = (distance, length) => Array.from(
  { length: length },
  (_, i) => distance(i / (length - 1))
);
game.setMap(createMap(parabola, 100));
```
Passing `null` as map will revert back to auto-generating a new map for every round of the game.

Whenever another game round is started, the current map will be output to the developer console of the
browser. This allows to store the current (possibly auto-generated) map elsewhere and re-use it later.

Note that the map is only applied for new rounds of the game, not the current one.

## Compilation

This web application is built using several compilable languages:

- The HTML pages are built from **pug** template files.
- The CSS stylesheet is pre-compiled from **sass** files.
- The JS scripts are trans-compiled from **es6** (ES2015) files. 

To make any modifications re-compilation is necessary. You should install:

- **node** and **npm**
- **yarn**
- **gulp** (install globally)

Afterwards run the following in the command line:

```
cd src
yarn
```

After it runs succesfuly you can compile as needed:

- **sass (stylesheets)**
    ```
    gulp styles
    ```
  
- **scripts (ES6)**
    ```
    gulp scripts
    ```

- **pug (HTML pages)**
    ```
    gulp html
    ```

- **all**
    ```
    yarn run build
    ```

## Credits

Developed by Christian Stussak and Eric Londaits for IMAGINARY gGmbH.
Based on a prototype by Aaron Montag.

## License

Copyright (c) 2020 IMAGINARY gGmbH
Licensed under the MIT License (see LICENSE)
