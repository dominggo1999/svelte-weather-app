<script>
	import { onMount } from 'svelte';
	import axios from "axios";
	import DisplayData from './DisplayData.svelte';

	let city = "";
	let country ="";
	let API_KEY = 'c18fdf7e433946bc881144552202008';  
	let data = {};
	let number =20;

	const handleSubmit =async (e) =>{
		let url = `http://api.weatherapi.com/v1/current.json?key=${API_KEY}&q=${city}`;
		
		const callData = async () =>{
			const res = await fetch(url);
			data = await res.json();
		}

		return callData();
	}

	const countUp = () =>{
		number++;
	}

</script>

<main>
	<section class="app-container">
		<form on:submit|preventDefault={handleSubmit}>
			<input class="city" bind:value={city} type="text" required="" placeholder="Enter city...">
			<input class="country" bind:value={country} type="text" required="" placeholder="Enter country...">
			<button type="submit">Enter</button>
			<p class="text-white">{city || "nowhere"} {country||"nowhere"}</p>
		</form>
		<DisplayData count={number} data={data}/>
		<button on:click={countUp}>Click me</button>
	</section>
</main>

<style type="text/scss">
	:global(*){
		margin:0;
		padding: 0;
		box-sizing: border-box;
	}

	main{
		position: relative;
		width: 100%;
		height: 100vh;
		background: #212121;
		
		section.app-container{
			width: 100%;
			height: 100%;
			position: absolute;
			text-align: center;

			form{
				margin-top: 20px;
			}
		}


		.text-white{
			color: #fff;
		}
	}
</style>