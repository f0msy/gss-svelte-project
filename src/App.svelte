
<script charset="utf-8">
	export let cfg;
	
	import ComplicatedBigComponent from "./ComplicatedBigComponent.svelte"
	import ComplicatedSmallComponent from "./ComplicatedSmallComponent.svelte"
	import HeaderComponent from "./HeaderComponent.svelte"
	import SimpleBigComponent from "./SimpleBigComponent.svelte"
	import SimpleSmallComponent from "./SimpleSmallComponent.svelte"

	let mainData;

	const init = async () => {
		// const res = await fetch("/data-sources/data.json");
		const res = await fetch(`/app/v1.2/api/publications/action/get-roadmap-data?taskid=${cfg.taskid}`);
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
			<div class="containers"><SimpleBigComponent data={mainData.data.acceptInit[0]} /></div>
			<div class="containers"><ComplicatedBigComponent data={mainData.data.projectPassport[0]} /></div>
			<div class="containers"><SimpleBigComponent data={mainData.data.acceptProject[0]} /></div>
			<div class="small-container">
			{#each mainData.data.stages as item}
				<ComplicatedSmallComponent data={item} />
			{/each}
			</div>
			<div class="small-container-2col">
				<SimpleSmallComponent data={mainData.data.promotion[0]} />
				<SimpleSmallComponent data={mainData.data.realization[0]} />
			</div>
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
		text-align: center;
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
		margin-top: 20px;
	}	

	:global(#roadMap-app .headers a) {
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
		position: relative;
		/* padding: 10px 15px 15px 15px; */
	}
	:global(#roadMap-app .small-container) {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		grid-gap: 0.3vw;
		
	}
	:global(#roadMap-app .small-container-2col) {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 0.3vw;
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
		display: grid;
    	grid-template-columns: 1fr 1fr 1fr;
		width: 100%;
		margin: 15px 0;
	}
	:global(#roadMap-app .accepted-small) {
		width: 85%;
		text-align: left;
	}
	:global(#roadMap-app .accepted-big) {
		width: 95%;
		text-align: left;
	}
	:global(#roadMap-app .gray-icon) {
		color: #bbbbbb;
	}
	:global(#roadMap-app .info-block) {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
	}
	:global(#roadMap-app .info-block-small) {
		display: flex;
		flex-direction: row;
	}
	:global(#roadMap-app .left-icons) {
		display: flex;
		margin: 0 0 0 7%;
		width: 75%;
	}
	:global(#roadMap-app .left-icons-small) {
		display: flex;
		margin: 0 0 0 20%;
		width: 20%;
	}
	:global(#roadMap-app .center-bar) {
		width: 100%;
		top: 0px;
    	position: absolute;
	}
	:global(#roadMap-app .center-icons) {
		display: flex;
    	width: 100%;
		justify-content: center;
	}
	:global(#roadMap-app .center-bar-small) {
		padding: 0px 10px 0 0px;
		width: 50%;
	}
	:global(#roadMap-app .mnp-rating-item) {
		display: flex;
		align-items: center;
		/* padding: 5px 0; */
		height: 10px;
		position: relative;
		/* text-shadow: 1px 1px 1px #000, 0 0 1px #000; */
	}
	:global(#roadMap-app .mnp-rating-points) {
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 10px;
		flex: 1 0 36px;
		z-index: 2;
	}
	:global(#roadMap-app .mnp-rating-progress) {
		position: absolute;
		left:0;
		width: 100%;
		z-index: 1;
		height: 100%;
		background: rgb(0 162 255 / 0.2);
	}
	:global(#roadMap-app .mnp-rating-progress-bar) {
		height: 100%;
		background: #0090ff;
	}	
	:global(#roadMap-app .right-icons) {
		display: flex;
		justify-content: flex-end;
		margin: 10px 7% 0 0;
	}
	:global(#roadMap-app .right-icons-small) {
		display: flex;
		justify-content: flex-end;
		margin: 10px 5% 0 0;
		width: 80%;
	}
	:global(#roadMap-app .green-tasks) {
		cursor: pointer;
		font-weight: 700;
		background-color: rgb(120, 190, 120);
		border: 1px solid rgb(120, 190, 120);
    	border-radius: 5px;
		width: 15%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 3px;		
	}
	:global(#roadMap-app .yellow-tasks) {
		cursor: pointer;
		font-weight: 700;
		background-color: #ffcd00;
		border: 1px solid #ffcd00;
    	border-radius: 5px;
		width: 10%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 3px;
	}
	:global(#roadMap-app .red-tasks) {
		cursor: pointer;
		font-weight: 700;
		background-color: rgb(255, 169, 169);
		border: 1px solid rgb(255, 169, 169);
    	border-radius: 5px;
		width: 10%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
		:global(#roadMap-app .green-tasks-small) {
		cursor: pointer;
		font-weight: 700;
		background-color: rgb(120, 190, 120);
		border: 1px solid rgb(120, 190, 120);
    	border-radius: 5px;
		width: 45%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 3px;		
	}
	:global(#roadMap-app .yellow-tasks-small) {
		cursor: pointer;
		font-weight: 700;
		background-color: #ffcd00;
		border: 1px solid #ffcd00;
    	border-radius: 5px;
		width: 25%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 3px;
	}
	:global(#roadMap-app .red-tasks-small) {
		cursor: pointer;
		font-weight: 700;
		background-color: rgb(255, 169, 169);
		border: 1px solid rgb(255, 169, 169);
    	border-radius: 5px;
		width: 25%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	:global(#roadMap-app .complicated-container) {
		display: grid;
		grid-template-columns: 1fr;
		position: relative;
		/* margin: 5px; */
	}
	 :global(#roadMap-app .align-content) {
		display: flex;
		align-items: center;
		flex-direction: column;
		text-align: center;
	}
	 :global(#roadMap-app .back-green) {
		background-color: #d2ead4;
	}
	 :global(#roadMap-app .headers-red) {
		font-weight: 700;
    	color: #ff6f73;
		font-size: 25px;
	}
	:global(#roadMap-app .triangle-active:after) {
		content: '';
		width: 0;
		height: 0;
		border-style: solid;
		border-width: 30px 30px 0 0;
		border-color: transparent rgb(120, 190, 120) transparent transparent;
		right: 0;
		bottom: 0;
		position: absolute;
	}
		:global(#roadMap-app .triangle-default:after) {
		content: '';
		width: 0;
		height: 0;
		border-style: solid;
		border-width: 30px 30px 0 0;
		border-color: transparent rgb(155, 155, 155) transparent transparent;
		right: 0;
		bottom: 0;
		position: absolute;
	}
</style>