<script>
    export let data;

    import ParticipantsWindowComponent from "./ParticipantsWindowComponent.svelte"

    let display = false;
    const openParticipantsDiv = () => {

        if (display == false) {
            display = true;
        } else {
            display = false;
        }

        setTimeout(() => {
            let modal = document.querySelectorAll('[data-shown="1"]')[0] 
            var span = modal.childNodes[0].childNodes[0];

            modal.style.display = "block";
        
            span.onclick = function() {
                modal.style.display = "none";
            }
            window.onclick = function(event) {
                if (event.target == modal) {
                    modal.style.display = "none";
                }   
            }
            modal.dataset.shown = "0";  
            display = false;
        }, 200)
          
    }

</script>
<div on:click={openParticipantsDiv} class="icons-size">
     <i class="fa fa-users" aria-hidden="true"></i>
</div>
<ParticipantsWindowComponent data={data} bind:showHide={display} />
