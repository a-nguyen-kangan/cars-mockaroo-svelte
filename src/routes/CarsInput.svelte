<script>
    import { createEventDispatcher } from "svelte";
    
    const dispatch = createEventDispatcher();

    let newRego = "AAA-111";
    let newMake = "Ford";
    let newModel = "Falcon";

    function addCarHandler() {
        console.log("addCar function called from CarsInput.svelte")

        dispatch("addCar", {
            rego: newRego,
            make: newMake,
            model: newModel
        });
    }
</script>

<div class="input">
    <input type="text" placeholder="Enter a car rego" bind:value={newRego}/>
    <input type="text" placeholder="Enter a car make" bind:value={newMake}/>
    <input type="text" placeholder="Enter a car model" bind:value={newModel}/>
    <br>
    <button on:click={addCarHandler}>Add Car</button>
</div>

<style>
    .input {
        background-color: yellow;
    }
</style>