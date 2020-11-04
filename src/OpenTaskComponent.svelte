<script>
    export let link
    const openTask = (link) => {
       radopen(link);
    }
</script>
<div on:click={() => {openTask(link)}} class="icons-size">
     <i class="fa fa-link" aria-hidden="true"></i>
</div>