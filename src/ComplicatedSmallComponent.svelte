<script>
    export let data;

    import OpenTaskComponent from "./OpenTaskComponent.svelte"
    import ParticipantsComponent from "./ParticipantsComponent.svelte"
    // let radopen = (a) => {
    //     console.log(a);
    // }
    const openTask = (link) => {
       radopen(link);
    }
</script>
{#if data.taskId}
<div 
    class="simple-small-block containers complicated-container" 
    class:triangle-active={data.highlight=="1"}
    class:triangle-default={data.highlight=="0"}>     
        <div class="center-bar">
            <div class="mnp-rating-item">
                <div class="mnp-rating-progress">
                    <div style="width:{data.bar}%;" class="mnp-rating-progress-bar"></div>
                </div>
            </div>
        </div>
        
        <div class="headers paddings align-content"><span>{data.headerName} <a class="" on:click={() => {openTask(data.allTasksLink)}}>[{data.allTasks}]</a> </span></div>
        <div >
            <div class="simple-small-block">
                <span><span class="bold-text">Категория: </span>{data.category}</span>
                <span><span class="bold-text">Статус: </span>{data.state}</span>
                <span><span class="bold-text">Текущий срок: </span>{data.orderedTime}</span>
            </div>
        </div>
        <div class="align-content">
        <div class="icons-div">
            <div class="left-icons-small">
                {#if data.riskState == "red"}
                    <span 
                        class="icons-size"
                        style="color: #f44336;"
                        ><i class="fa fa-exclamation" aria-hidden="true"></i>
                    </span> 
                {:else if data.riskState == "yellow"}     
                    <span 
                        class="icons-size"
                        style="color: #ffcd00;"
                        ><i class="fa fa-exclamation" aria-hidden="true"></i>
                    </span>                    
                {:else if data.riskState == "green"}     
                    <span 
                        class="icons-size"
                        style="color: rgb(120, 190, 120);"
                        ><i class="fa fa-check" aria-hidden="true"></i>
                    </span>         
                {/if}
                {#if data.hasRisk == "1"}
                    <span on:click={() => {openTask(data.hasRiskLink)}} class="icons-size" style="color: #f44336">
                        <i class="fa fa-bullhorn" aria-hidden="true"></i>
                    </span>
                {/if}
            </div>
            <div class="center-icons">
                <OpenTaskComponent link={"/MainTaskForm.aspx?TaskID="+ data.taskId} />
                {#if data.participants}
                <ParticipantsComponent data={data.participants} />
                {/if}
            </div>
            <div class="right-icons-small">
                <div on:click={() => {openTask(data.greenLink)}} class="green-tasks-small">{data.green}</div>
                <div on:click={() => {openTask(data.yellowLink)}} class="yellow-tasks-small">{data.yellow}</div>
                <div on:click={() => {openTask(data.redLink)}} class="red-tasks-small">{data.red}</div>
            </div>
        </div>
        </div>
</div>
{/if}