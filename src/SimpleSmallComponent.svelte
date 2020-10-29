<script>
    export let data;

    import OpenTaskComponent from "./OpenTaskComponent.svelte"
    import ParticipantsComponent from "./ParticipantsComponent.svelte"

</script>

<div class="simple-small-block containers"
    class:back-green={data.highlight=="1"}>
    {#if data.taskId}
        {#if data.accepted}
        <span 
        class="icons-size accepted-small"
        class:gray-icon={data.accepted == "0"}
        ><i class="fa fa-pencil" aria-hidden="true"></i>
        </span> 
        {/if}
        <span class="headers paddings">{data.headerName}</span>
        <span><span class="bold-text">Категория:</span> {data.category}</span>
        <span><span class="bold-text">Статус:</span> {data.state}</span>
        <span class="paddings"><span class="bold-text">Длительность:</span> {data.duration}дн</span>
        <div class="icons-div">
            <OpenTaskComponent link={"/MainTaskForm.aspx?TaskID="+ data.taskLink} />
            <ParticipantsComponent data={data.participants} />
        </div>
    {:else}
    <span class="headers paddings">{data.headerName}</span>
    <span class="headers-red paddings">Не создано</span>
{/if}

</div>