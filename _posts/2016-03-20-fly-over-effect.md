---
layout: post
title: Fly over effect
---



It ought to be cool if you do a fly over the landscape of data. I actually don't know if ArcGIS js api supoorts fly over effect.

I run into this appliation. It seems to be a good one. I need to read it through. The code is shared at github. 

[FlywithMe](https://geonet.esri.com/blogs/james/2015/06/01/comeflywithme-a-arcgis-js-flightaware-api-mashup)

<code> 

	renderer = new THREE.WebGLRenderer({
		antialias: false
	});
	renderer.setSize(window.innerWidth, window.innerHeight);
	container.appendChild(renderer.domElement);

	window.addEventListener('resize', onWindowResize, false);


	function animate() {
	var position = ((Date.now() - startTime) * 0.03) % 4000;

	camera.position.z = -position + 4000;
	camera.rotation.x = -Math.PI / 2;
	camera.rotation.y = 0;

	renderer.render(scene, camera);
	requestAnimationFrame(animate);
    };

    function updateFlightPath() {
	$('#map').css('transform', 'rotate(' + (360 - flight.heading) + 'deg)');

	var distance = flight.groundspeed * 1000 / (60 * 60 * 10);

	var newLatLong = new LatLon(lat, lng).destinationPoint(distance, flight.heading, 6371000);
	lat = newLatLong.lat;
	lng = newLatLong.lon;

	//	console.log(newLatLong);

	map.centerAt(new ESRIPoint(lng, lat));
    };

    setInterval(function () {
	if (flight && flight.ident) {
		updateFlightPath()
	}
     }, 100);


</code>


I copied some relevant code here. Hope it can inspire me to write my own fly over with arcgis js 4.0. 








