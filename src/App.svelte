<script>
	import DisplayData from './DisplayData.svelte';

	let city = "";
	let country ="";
	let API_KEY = 'c18fdf7e433946bc881144552202008';  
	let data;
	let error = false;	
	let isSubmit = false;

	const handleSubmit =async (e) =>{
		let url = `https://api.weatherapi.com/v1/current.json?key=${API_KEY}&q=${city}`;
		isSubmit = true;
		const callData = async () =>{
			const response = await fetch(url).then(res=>{
				if(res.status!==400){
					error = true;
					return res.json();
				} else{
					error = false;
					return
				}

			});
			return response;
		}

		data = callData();
		city="";
		country="";
	}

</script>

<main>
	<section class="app-container">
		<form on:submit|preventDefault={handleSubmit}>
			<input class="city" bind:value={city} type="text" required placeholder="Enter city...">
			<input class="country" bind:value={country} type="text" required placeholder="Enter country...">
			<button type="submit">Enter</button>
			{#await data}
				<p class="text-white p-t">Loading....</p>
				}
			{:then dataReady}
				{#if error}
					<DisplayData data={dataReady}/>
				{:else if isSubmit}
					<p class="text-white p-t">No matching location found.</p>
				{/if}
			{/await}

		</form>
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

				input{
					background: none;
					border: solid 2px #fff;
					padding: 10px;
					border-radius: 10px;
					margin:0 2px;
					outline: none;
					color: #fff;
				}

				button{
					border: none;
					background:#A52277;
					color: #fff;
					padding: 12px 40px;
					border-radius: 10px;
					font-size: 18px;
					cursor: pointer;

					&:hover{
						background : #666666;
					}
				}

				@media screen and (max-width: 768px){
					button{
						margin-top: 20px;
					}
				}
			}
		}


		.text-white{
			color: #fff;
		}

		.p-t{
			margin-top: 100px;
		}
	}
</style>