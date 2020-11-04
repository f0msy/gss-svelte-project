<script>
    export let data;
</script>

<div id="header-block">
    <span class="main-header paddings">{data.headerName}</span>
    <span class="headers paddings">«{data.productName}»</span>
    <span class="bold-text paddings">(инициатива от {data.initDate}, общая длительность {data.duration}дн)</span>
</div>