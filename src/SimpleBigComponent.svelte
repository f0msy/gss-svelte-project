<script>
    export let data;

    import OpenTaskComponent from "./OpenTaskComponent.svelte"
    import ParticipantsComponent from "./ParticipantsComponent.svelte"

</script>

<div class="simple-small-block"
    class:back-green={data.highlight=="1"}>
    {#if data.taskId}
    <span 
        class="icons-size accepted-big"
        class:gray-icon={data.accepted == "0"}
        ><i class="fa fa-pencil" aria-hidden="true"></i>
    </span> 
    <span class="headers paddings">{data.headerName}</span>
    <span><span class="bold-text">Статус:</span> {data.state}</span>
    <span><span class="bold-text">Дата согласования:</span> {data.acceptEnd}</span>
    <a href="/component/SignaturesJournal.aspx?TaskID={data.taskId}"><span class="bold-text">Заключение</span></a>
    <div class="icons-div">
        <OpenTaskComponent link={"/MainTaskForm.aspx?TaskID="+ data.taskLink} />
        <ParticipantsComponent data={data.participants} />
    </div>
    {:else}
        <span class="headers paddings">{data.headerName}</span>
        <span class="headers-red paddings">Не создано</span>
    {/if}
</div>