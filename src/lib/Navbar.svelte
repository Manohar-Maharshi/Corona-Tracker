<script>
	import { onMount } from 'svelte';
	let countryInfoArray = [];
	let worldTotal;
	onMount(async () => {
		const res = await fetch("https://disease.sh/v3/covid-19/countries");
		const worldRes = await fetch("https://disease.sh/v3/covid-19/all");
		const worldjson = await worldRes.json();
		worldTotal =  +worldjson.cases;
		const data = await res.json();
		data.forEach((d) =>{
			countryInfoArray.push(d);
			countryInfoArray = countryInfoArray;
		})
	});
	function numberWithCommas(x) {
	    var parts = x.toString().split(".");
	    parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
	    return parts.join(".");
	}
</script>
<nav>
	<a class="world-link" href="#">
		<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-map" viewBox="0 0 16 16">
		  <path fill-rule="evenodd" d="M15.817.113A.5.5 0 0 1 16 .5v14a.5.5 0 0 1-.402.49l-5 1a.502.502 0 0 1-.196 0L5.5 15.01l-4.902.98A.5.5 0 0 1 0 15.5v-14a.5.5 0 0 1 .402-.49l5-1a.5.5 0 0 1 .196 0L10.5.99l4.902-.98a.5.5 0 0 1 .415.103zM10 1.91l-4-.8v12.98l4 .8V1.91zm1 12.98 4-.8V1.11l-4 .8v12.98zm-6-.8V1.11l-4 .8v12.98l4-.8z"/>
		</svg>
		<p>World</p>
		<p class="country-cases-count">+{worldTotal}</p>
	</a>
	<ul>
		{#each countryInfoArray as countryData}
			<li title="{countryData.country}">
				<a class="country-link" href="#">
					<div class="country-detailes">
						<img class="country-flag" src="{countryData.countryInfo.flag}" alt="{countryData.country}">
						<span class="country-name">{countryData.country}</span>
					</div>
					<p class="country-cases-count">+{numberWithCommas(countryData.cases)}</p>
				</a>
			</li>
		{/each}
	</ul>
</nav>



<style>
	nav{
		padding: 0 1.5rem;
	    margin: 0 auto;
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 5rem;
		margin-top: 1rem;
		-webkit-user-drag: none;
	}
	.world-link{
		border-radius: 3px;
		height: 100%;
		flex: 1;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		text-align: center;
		font-size: 1.5rem;
		margin-right: 0.9rem;
		background-color: #1A1C20;
		font-size: 1.2rem;
		box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
	}
	.world-img{
		width: 1.5rem;
	}
	ul{
		height: 100%;
		flex: 8;
		display: flex;
		align-items: center;
		justify-content: space-between;
		overflow: overlay;
		overflow-y: hidden;
	}
	.country-link{
		border-radius: 3px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		height: 5rem;
		width: 9rem;
		padding: 0.5rem 2rem;
		text-align: center;
		font-size: 1.5rem;
		margin-right: 0.7rem;
		background-color: #222831;
		box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
	}
	.country-link::last-child{
		margin-right: 0;
	}
	.country-detailes{
		line-height: 1.5;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}
	.country-name{
		font-size: 1.2rem;
		padding: 0.1rem 0;
		padding-bottom: 0;
		width: 130px;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	.country-flag{
		width: 1.5rem;
	}
	.country-cases-count{
		margin-top: -0.1rem;
		font-size: 0.6rem;
		font-style: italic;
		opacity: 0.3;
	}
	::-webkit-scrollbar {
	  width: 6px;
	  height: 6px;
	}
	::-webkit-scrollbar-track {
	  border-radius: 10px;
	  background: rgba(0, 0, 0, 0);
	}
	::-webkit-scrollbar-thumb {
	  border-radius: 10px;
	  background: rgba(0, 0, 0, 0.2);
	}
	::-webkit-scrollbar-thumb:hover {
	  background: rgba(0, 0, 0, 0.4);
	}
	::-webkit-scrollbar-thumb:active {
	  background: rgba(0, 0, 0, 0.9);
	}
</style>