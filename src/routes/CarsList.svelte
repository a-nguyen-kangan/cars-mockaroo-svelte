<script>
    export let carsList = [];

    $: if(carsList.length > 5) {
        alert("CarsList - You have too many cars");
    }
</script>

<p>This is the cars component</p>

{#each carsList as car}
    <p>{car.rego} - {car.make} - {car.model}</p>
{/each}
