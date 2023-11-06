<script>
    export let rego;
    export let make;
    export let model;
</script>

{#if !rego}
<h3>no car selected yet</h3>
{:else}
<h3>Rego: {rego}  | Make: {make} | Model: {model}</h3>
{/if}