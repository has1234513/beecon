<script>
	// @ts-nocheck
	import { onMount } from 'svelte';
	import 'maplibre-gl/dist/maplibre-gl.css';
	import { Loader } from '@googlemaps/js-api-loader';

	const api_key = import.meta.env.VITE_GOOGLE_MAPS_API_KEY;

	let map; // Declare the map variable


	onMount(() => {
		const loader = new Loader({
			apiKey: api_key,
			version: 'weekly'
		});

		loader.load().then(async () => {
			const { Map } = await google.maps.importLibrary('maps');

			map = new Map(document.getElementById('map-container'), {
				// Corrected ID
				center: { lat: -34.08, lng: 18.54 },
				zoom: 8
			});

			// Get the location from your server or other source
			const deviceLocation = { lat: -34.078238963294666, lng: 18.550834410232856 };

			// Create a marker at that location
			const marker = new google.maps.Marker({
				position: deviceLocation,
				map: map,
				title: 'My Device',
				icon: 'https://maps.google.com/mapfiles/ms/icons/blue-dot.png' // Optional: custom icon
			});

			// Optionally, set the map's center to the device's location
			map.setCenter(deviceLocation);
		});
	});
</script>

<div class="map-wrap">
	<div id="map-container"><!-- Corrected ID --></div>
</div>

<style>
	.map-wrap {
		position: relative;
		width: 100%;
		height: calc(80vh - 77px); /* calculate height of the screen minus the heading */
	}

	#map-container {
		/* Updated CSS selector */
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.watermark {
		position: absolute;
		left: 10px;
		bottom: 10px;
		z-index: 999;
	}
</style>
