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
  export let markers = [{ lat: 50.85499742276381, lng: 4.366053727009928 }];
  export let customMarkerUrl = "marker_svg.svg";

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

      if (markers && customMarkerUrl) {
        const icon = L.icon({
          iconUrl: customMarkerUrl,
          iconSize: [56, 56],
          iconAnchor: [28, 55], // point of the icon which will correspond to marker's location
        });

        markers.forEach((marker) => {
          console.log(marker.lat);
          L.marker([marker.lat, marker.lng], { icon }).addTo(map);
        });
      } else if (markers) {
        markers.forEach((marker) => {
          console.log(marker.lat);
          L.marker([marker.lat, marker.lng], { icon }).addTo(map);
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
