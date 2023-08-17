<script>
  // imports
  import { onMount, onDestroy } from "svelte";
  import { browser } from "$app/environment";
  import "leaflet/dist/leaflet.css";

  // Exports
  export let height = "200px";
  export let width = "200px";
  export let initialView = [50.85695267176521, 4.359590452037109];
  export let initialZoom = 10;
  export let markers = [
    [50.85695267176521, 4.359590452037109],
    [50.6, 4.4],
  ];
  export let customMarker = "";

  let map;

  onMount(async () => {
    if (browser) {
      const L = await import("leaflet");

      map = L.map("map").setView(initialView, initialZoom);
      L.tileLayer(
        "https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png",
        {
          maxZoom: 20,
          attribution:
            '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
        }
      ).addTo(map);

      if (markers && customMarker) {
        const icon = L.icon({
          iconUrl: customMarker,
          iconSize: [36, 36],
          iconAnchor: [18, 36], // point of the icon which will correspond to marker's location
        });

        markers.forEach((marker) => {
          L.marker([marker[0], marker[1]], { icon }).addTo(map);
        });
      } else if (markers) {
        markers.forEach((marker) => {
          L.marker([marker[0], marker[1]]).addTo(map);
        });
      }
    }
  });

  onDestroy(async () => {
    if (map) {
      console.log("Unloading Leaflet map.");
      map.remove();
    }
  });
</script>

<div id="map" style="height: {height}; width: {width};" />

<style>
  #map {
    height: var(--height);
    width: var(--width);
  }
</style>
