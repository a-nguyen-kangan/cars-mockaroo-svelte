<script>
    export let carsList = [];

    $: if(carsList.length > 5) {
        alert("CarsList - You have too many cars");
    }
</script>

<div>
<p>This is the cars component</p>

{#each carsList as car}
    <p>{car.rego} - {car.make} - {car.model}</p>
{/each}
</div>

<style>
    div {
        background-color: green;
    }
</style>