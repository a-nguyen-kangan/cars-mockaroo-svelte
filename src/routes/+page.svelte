<script>
    import CarsList from './CarsList.svelte';
    let newRego = "AAA-111";
    let newMake = "Ford";
    let newModel = "Falcon";

    let cars = [
                    {rego: "ABC123", make: "Toyota", model: "Corolla"},
                    {rego: "DEF456", make: "Toyota", model: "Camry"},
                    {rego: "GHI789", make: "Toyota", model: "Yaris"},   
               ];

    let promise = getCars();

    $: if(cars.length > 5) {
        alert("+page.svelte - You have too many cars");
    }

    
    function addCar() {
        // cars.push({rego: newRego, make: newMake, model: newModel});
        // cars = cars;
        cars = [...cars, {rego: newRego, make: newMake, model: newModel}];

        console.log(cars);
    }

    async function getCars() {
        // const response = await fetch('https://my.api.mockaroo.com/cars.json?key=47956d40');
        // const data = await response.json();
        // console.log(data);

        const response = await fetch('https://my.api.mockaroo.com/cars.json?key=47956d40')
                        .then(response => response.json())
                        .catch(error => {
                            console.log(error);
                        });

        cars = response;
        return response;
    }

</script>

<h1>Mockaroo Cars application</h1>
<div class="input">
    <input type="text" placeholder="Enter a car rego" bind:value={newRego}/>
    <input type="text" placeholder="Enter a car make" bind:value={newMake}/>
    <input type="text" placeholder="Enter a car model" bind:value={newModel}/>
    <br>
    <button on:click={addCar}>Add Car</button>
</div>

{#await promise}
    <p>Sorry for the wait, just getting the cars</p>
{:then onlineCars}
    <CarsList carsList={cars}/>
{:catch error}
    <p>Sorry, there was an error getting the cars</p>
{/await}




{#if newMake === "Toyota"}
    <p style="color: red">There seem to be alot of Toyotas</p>
{/if}

<style>
  h1 {
    color: red;
  }

  .input {
    background-color: yellow;
  }
</style>
