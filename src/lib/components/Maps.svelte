<script>
// @ts-nocheck

  import { onMount } from 'svelte';
  let map;
  let marker;
  let mapElement;

  // Replace with your own Google Maps API key
  const apiKey = 'My_Api_key';

  // Replace with the initial coordinates of the GPS device
  const initialPosition = { lat: -34.397, lng: 150.644 };

  onMount(async () => {
    // Load the Google Maps JavaScript API script
    const script = document.createElement('script');
    script.src = `https://maps.googleapis.com/maps/api/js?key=${apiKey}`;
    script.async = true;
    document.head.appendChild(script);

    // Wait for the Google Maps JavaScript API script to load
    await new Promise(resolve => {
      script.onload = resolve;
    });

    // Create the map
    map = new google.maps.Map(mapElement, {
      center: initialPosition,
      zoom: 8,
    });

    // Create the marker
    marker = new google.maps.Marker({
      position: initialPosition,
      map,
    });

    // Update the marker position in real-time as new GPS data becomes available
    // Replace this with your own code to get the GPS data
    setInterval(() => {
      const newPosition = getNewPositionFromGPS();
      marker.setPosition(newPosition);
      map.panTo(newPosition);
    }, 1000);
  });
</script>

<svelte:head>
  <style>
    #map {
      height: 400px;
      width: 600px
    }
  </style>
</svelte:head>

<h1>Maps is supposed to be here</h1>

<div id="map" bind:this={mapElement}></div>