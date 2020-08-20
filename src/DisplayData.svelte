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
				<i class="logo wi wi-night-alt-partly-cloudy"></i>
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
		margin-top: 15px;
		.top{
			display: flex;
			justify-content: center;	
			align-items: flex-end;
			margin-bottom: 20px;
			.logo{
				font-size: 65px;
				padding:0 5px;
			}

			@media screen and (min-width:768px){
				.logo{
					font-size: 80px;
				}
			}

			.description{
				display: flex;
				flex-direction: column;
				align-items: flex-start;

				.location{
					font-size: 17px;
					font-weight: 700;
					margin-bottom: 6px;
				}

				.date{
					font-size: 15px;
				}

				@media screen and (min-width:768px){
					.location{
						font-size: 21px;
					}

					.date{
						font-size: 17px;
					}
				}
			}
		}
		
		.bottom{
			h1{
				font-size: 60px;
				font-weight: 500;
			}

			p{
				font-size: 20px;
				font-weight: 400;
			}
		}

		@media screen and (min-width:768px){
			.bottom{
				h1{
					font-size: 180px;
				}

				p{
					font-size: 20px;

				}
			}
		}
	}
</style>