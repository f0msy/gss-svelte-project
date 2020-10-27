
<script charset="utf-8">
	import ComplicatedBigComponent from "./ComplicatedBigComponent.svelte"
	import ComplicatedSmallComponent from "./ComplicatedSmallComponent.svelte"
	import FlexibleComponent from "./FlexibleComponent.svelte"
	import HeaderComponent from "./HeaderComponent.svelte"
	import SimpleBigComponent from "./SimpleBigComponent.svelte"
	import SimpleSmallComponent from "./SimpleSmallComponent.svelte"

	let mainData;

	const init = async () => {
		const res = await fetch("/data-sources/data.json");
		// const res = await fetch(`/app/v1.2/api/publications/action/get-suppliers-data?year=${cfg.year}&suppId=${cfg.suppId}&stateId=${cfg.stateId}&suppType=${cfg.suppType}&canSave=${cfg.canSave}`);
		mainData = await res.json();
		return mainData;
	  };
	  
  	let initPromise = init();
</script>

<body>
	<div id="roadMap-app">
		{#await initPromise}
      		<p>...загрузка</p>
    	{:then data}
			<div id="header-container" class="containers">
				<HeaderComponent data={mainData.data.header[0]} />
			</div>
			<div class="small-container">
				<SimpleSmallComponent data={mainData.data.product[0]} />
				<SimpleSmallComponent data={mainData.data.analysisKB[0]} />
				<SimpleSmallComponent data={mainData.data.analysisTRIS[0]} />
			</div>
			<div class="containers"><p>Блок</p></div>
			<div class="containers"><p>Блок</p></div>
			<div class="containers"><p>Блок</p></div>
			<div class="containers"><p>Блок</p></div>
		{:catch error}
     		<p style="color: red">{error.message}</p>
    	{/await}
	</div>
</body>

<style>
	:global(#roadMap-app) {
		display: grid;
		grid-template-columns: 1fr;	
		margin-right: 20px;
		margin: 0 15%;
	}

	:global(#roadMap-app #header-block) {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin: 15px 0px 15px 0px;
	}

	:global(#roadMap-app .containers) {
	margin: 5px;
	background-color: white;
	box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
	transition: all 0.3s cubic-bezier(.25,.8,.25,1);
	}

	:global(#roadMap-app .containers):hover {
	box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
	}
	:global(#roadMap-app .main-header) {
		font-weight: 700;
    	color: #0090ff;
    	font-size: 30px;
	}
	:global(#roadMap-app .headers) {
		font-weight: 700;
    	color: #0090ff;
    	font-size: 25px;
	}	
	:global(#roadMap-app .bold-text) {
		font-weight: 600;
	}
	:global(#roadMap-app .paddings) {
		padding-bottom: 10px;
	}
	
	:global(#roadMap-app .simple-small-block) {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin: 15px 0px 15px 0px;
		padding: 10px 0 15px 0;
	}
	:global(#roadMap-app .small-container) {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
    	grid-gap: 0.5vw;
	}
	
	:global(#roadMap-app .icons-size) {
		font-size: 25px;
		cursor: pointer;
		margin: 5px;
	}
	:global(#roadMap-app .hidden) {
		display: none;
	}
	:global(#roadMap-app .icons-div) {
		display: flex;
		flex-direction: row;
	}
</style>