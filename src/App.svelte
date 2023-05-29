<script>
	import { onMount } from "svelte";
	import Grid from "gridjs-svelte";
	// import './app.css';
  
	let jsonData = [];
	let tableVisible = false;
  
	onMount(async () => {
	  const response = await fetch("https://api.recruitly.io/api/masterdata/industries?apiKey=TEST9349C0221517DA4942E39B5DF18C68CDA154");
	  const responseData = await response.json();
	  jsonData = responseData.data;
	});
  
	function openTable() {
	  if (!tableVisible) {
		fetchData();
	  }
	}
  
	async function fetchData() {
	  const response = await fetch("https://api.recruitly.io/api/masterdata/industries?apiKey=TEST9349C0221517DA4942E39B5DF18C68CDA154");
	  const responseData = await response.json();
	  jsonData = responseData.data;
	  tableVisible = true;
	}
  </script>
  
  <!-- <button on:click={openTable}>Display Table</button> -->
  <h1>Data Display from Api</h1>
  <main>
	{#if openTable}
	  <Grid
		
		
		pagination={{ enabled: true, limit: 38 }}
		data={jsonData.map(item => ({
			reference: item.id,
		  title: item.name,
		  
		  
		}))} />
	{/if}
  </main>
  
  <style global>
	@import "https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css";
  </style>