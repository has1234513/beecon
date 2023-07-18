<script>
// @ts-nocheck

	import Map from '../../lib/components/Maps.svelte';
	export let ready;
  let GOOGLE_MAPS_API_KEY = "fsdfsdf"
</script>

<svelte:head>
	<script defer async
	src="https://maps.googleapis.com/maps/api/js?key={GOOGLE_MAPS_API_KEY}&callback=initMap">
	</script>
</svelte:head>

<div>
  <h1>Map</h1>

  { #if ready }
  <Map/>
  { /if }
  </div>

