<script>
	import "../weather-icons-master/css/weather-icons.min.css";
	import dateformat from 'dateformat';
	
	export let data;
	let city;
	let country; 
	let temp;
	let condition;
	const now = new Date();
	const date = dateformat("dddd, mmmm d");

	if(data){
		console.log(data);
		city = data.location.name;
		country = data.location.country;
		temp = data.current.temp_c;
		condition = data.current.condition.text;
	}

</script>

{#if data}
	<div class="display-data">
		<div class="wrapper">
			<div class="top">
				<i class="wi wi-night-alt-partly-cloudy"></i>
				<div class="logo"></div>
				<div class="description">
					<div class="location">{city}, {country}</div>
					<div class="date">{date}</div>
				</div>
			</div>
			<div class="bottom">
				<h1>{temp}&deg;C</h1>
				<p>{condition}</p>
			</div>
		</div>
	</div>
{/if}

<style type='text/scss'>
	.display-data{
		color: #fff;
	}
</style>