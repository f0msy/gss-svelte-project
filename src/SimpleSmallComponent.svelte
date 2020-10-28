<script>
    export let data;

    import OpenTaskComponent from "./OpenTaskComponent.svelte"
    import ParticipantsComponent from "./ParticipantsComponent.svelte"

</script>

<div class="simple-small-block containers">
    <span 
        class="icons-size accepted-small"
        class:gray-icon={data.accepted == "0"}
        ><i class="fa fa-pencil" aria-hidden="true"></i>
    </span> 
    <span class="headers paddings">{data.headerName}</span>
    <span><span class="bold-text">Категория:</span> {data.category}</span>
    <span><span class="bold-text">Статус:</span> {data.state}</span>
    <span class="paddings"><span class="bold-text">Длительность:</span> {data.duration}дн</span>
    <div class="icons-div">
        <OpenTaskComponent link={"/MainTaskForm.aspx?TaskID="+ data.taskLink} />
        <ParticipantsComponent data={data.participants} />
    </div>
</div>