<script>
    export let data;

    import OpenTaskComponent from "./OpenTaskComponent.svelte"
    import ParticipantsComponent from "./ParticipantsComponent.svelte"

    const openTask = (link) => {
       radopen(link);
    }
</script>

<div class="complicated-container"
    class:back-green={data.highlight=="1"}>
    {#if data.taskId}
    <div class="info-block">
        <div class="left-icons">
            <span 
            class="icons-size"
            class:gray-icon={data.accepted == "0"}
            ><i class="fa fa-pencil" aria-hidden="true"></i>
            </span> 
            {#if data.riskState == "red"}
                <span 
                    class="icons-size"
                    style="color: #ff6f00"
                    ><i class="fa fa-fire" aria-hidden="true"></i>
                </span> 
            {:else if data.riskState == "yellow"}     
                <span 
                    class="icons-size"
                    style="color: #ffcd00"
                    ><i class="fa fa-exclamation" aria-hidden="true"></i>
                </span>                    
            {:else if data.riskState == "green"}     
                <span 
                    class="icons-size"
                    style="color: rgb(120, 190, 120)"
                    ><i class="fa fa-check" aria-hidden="true"></i>
                </span>         
            {/if}
            {#if data.hasRisk == "1"}
                <span on:click={openTask(data.hasRiskLink)} class="icons-size" style="color: #ff6f00">
                    <i class="fa fa-bolt" aria-hidden="true"></i>
                </span>
            {/if}
        </div>
        <div class="center-bar">
            <div class="mnp-rating-item">
                <div class="mnp-rating-points">{data.bar}%</div>
                <div class="mnp-rating-progress">
                    <div style="width:{data.bar}%;" class="mnp-rating-progress-bar"></div>
                </div>
            </div>
        </div>
        <div class="right-icons">
            <div on:click={openTask(data.greenLink)} class="green-tasks">{data.green}</div>
            <div on:click={openTask(data.yellowLink)} class="yellow-tasks">{data.yellow}</div>
            <div on:click={openTask(data.redLink)} class="red-tasks">{data.red}</div>
        </div>
    </div>
    <div class="headers paddings align-content" style="margin-top: 20px;"><span>{data.headerName} <a class="headers" href="{data.allTasksLink}">[{data.allTasks}]</a> </span></div>
    <div >
        <div class="simple-small-block">
            <span><span class="bold-text">Статус: </span>{data.state}</span>
            <span><span class="bold-text">Руководитель проекта: </span>{data.projectManager}</span>
            <span><span class="bold-text">Плановый срок: </span>{data.plannedOrderedTime}</span>
        </div>
        <div class="simple-small-block">
            <span><span class="bold-text">Дата начала: </span>{data.startDate}</span>
            <span><span class="bold-text">Дата окончания: </span>{data.endDate}</span>
        </div>
    </div>
    <div class="align-content">
    <div class="icons-div">
        <OpenTaskComponent link={"/MainTaskForm.aspx?TaskID="+ data.taskLink} />
        <ParticipantsComponent data={data.participants} />
        <div on:click={openTask(data.taskId)} class="icons-size">
            <i class="fa fa-sitemap" aria-hidden="true"></i>
        </div>
    </div>
    </div>
    {:else}
        <span class="headers paddings">{data.headerName}</span>
        <span class="headers-red paddings">Не создано</span>
    {/if}
</div>