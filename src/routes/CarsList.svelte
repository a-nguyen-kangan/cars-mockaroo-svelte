<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let carsList = [];

    $: if(carsList.length > 5) {
        alert("CarsList - You have too many cars");
    }

    function handleRegoClick(event) {
        dispatch("regoClick", {
            rego: event.target.id  // returns the id of the element that was clicked
        });



    }
</script>

<div>
<p>This is the cars component</p>

{#each carsList as car}
    <p on:click={handleRegoClick} id={car.rego}>{car.rego}</p>
{/each}
</div>

<style>
    div {
        background-color: green;
    }
</style>