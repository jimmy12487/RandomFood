<html>
	<head>
	<meta charset="urf-8">
	<title> Random Food</title>
	<script src="Jquery.js"></script>	  
	<script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC2AcGg9-ZTvKKQz-76qcgq60lZRI7HSbU&libraries=places"></script>
	<style type="text/css">
		#map {
			height : 500px;
			width : 600px;
		}
	</style>
	</head>
	
	<body text="white" bgcolor="black">
		<h1 align="center"> Jimmy's WHATTOEAT <h1><hr>
		<section>
			<article>
				<h6> Current Location& Choices </h6>
				<div id="map"></div>
			<script>
				var map;
				var service;
				var contentstring;
				$(function(){		  
					navigator.geolocation.getCurrentPosition(function(position){
					var lat = position.coords.latitude;
					var lng = position.coords.longitude;
					var currentcenter = new google.maps.LatLng(lat,lng);	
					map = new google.maps.Map(document.getElementById('map'), {
						center: currentcenter,
						zoom: 16
					});
					var request = {
						location: currentcenter	,
						radius: '1500',
						type: ['restaurant', 'food',]
					};
					
					service = new google.maps.places.PlacesService(map);
					service.nearbySearch(request, callback);
										
					function callback(results, status) {
						if (status == google.maps.places.PlacesServiceStatus.OK) {
							for (var i = 0; i < results.length; i++) {
								createMarker(results[i]);
							}
						}
					}
					function createMarker(place) {
						var marker = new google.maps.Marker({
							map: map,
							position: place.geometry.location ,
						});	
						let infowindow = new google.maps.InfoWindow({
							content: place.name
						});
						marker.addListener('click', function() {
							infowindow.open(map, marker);
							infowindow.setContent('<div style="color:#000000" id="name">'+place.name+'</div>');
						});
					}
					
					})
				});
			</script>
			
		</article>
		<article>
		</article>
      </section>
