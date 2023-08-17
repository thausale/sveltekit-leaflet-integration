# How to implement the Map.svelte component into your project

- be sure to install the leaflet package
- `npm i leaflet`
- then import it where you want to use it

## There are a few options you can pass to the component

| Name            | example                                | Description                                                                  |
| --------------- | -------------------------------------- | ---------------------------------------------------------------------------- |
| height          | "200px"                                | The height of the component                                                  |
| width           | "500px"                                | the width of the component                                                   |
| initialView     | [50.85695267176521, 4.359590452037109] | The initial position of the map                                              |
| initialZoom     | 10                                     | The initial zoom of the map                                                  |
| markers         | [[50.85, 4.35],[50.60,4.40],...]       | Array with marker coordinates                                                |
| customMarkerUrl | "customMarker.svg"                     | The name of the customMarker file, make sure that it's in your static folder |
