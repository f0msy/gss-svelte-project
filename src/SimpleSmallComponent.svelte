<script>
    export let data;

    import OpenTaskComponent from "./OpenTaskComponent.svelte"
    import ParticipantsComponent from "./ParticipantsComponent.svelte"
    let signaturesList = '/component/SignaturesJournal.aspx?TaskID=' + data.taskId
    //     let radopen = (a) => {
    //     console.log(a);
    // }
    const openTask = (link) => {
       radopen(link);
    }
</script>

<div class="simple-small-block containers"
    class:triangle-active={data.highlight=="1"}
    class:triangle-default={data.highlight=="0"}>
    {#if data.taskId}
        <span class="headers paddings">{data.headerName}</span>
        <span><span class="bold-text">Категория:</span> {data.category}</span>
        <span><span class="bold-text">Статус:</span> {data.state}</span>
        <span class="paddings"><span class="bold-text">Длительность:</span> {data.duration}дн</span>
        <div class="icons-div">
            <div class="left-icons-small"></div>
            <div class="center-icons">
                {#if data.accepted}
                    <span 
                    on:click={() => {openTask(signaturesList)}}
                    class="icons-size"
                    class:gray-icon={data.accepted == "0"}
                    ><i class="fa fa-file-text-o" aria-hidden="true"></i>
                    </span> 
                {/if}
                <OpenTaskComponent link={"/MainTaskForm.aspx?TaskID="+ data.taskId} />
                {#if data.participants}
                <ParticipantsComponent data={data.participants} />
                {/if}
            </div>                
            <div class="right-icons-small"></div>
        </div>
    {:else}
    <span class="headers paddings">{data.headerName}</span>
    <span class="headers-red paddings">Не создано</span>
{/if}

</div>