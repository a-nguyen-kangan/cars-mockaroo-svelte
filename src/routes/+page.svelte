<script>
    import { onMount } from 'svelte';
    import CarsList from './CarsList.svelte';
    import CarsInput from './CarsInput.svelte';
    import CarDetail from './CarDetail.svelte';

    onMount( () => {
        getCars();
    });

    let cdRego;
    let cdMake;
    let cdModel;

    let cars = [];

    //let promise = getCars();

    $: if(cars.length > 5) {
        alert("+page.svelte - You have too many cars");
    }

    function createDefaultCars() {
        cars = [
            {rego: "CCC-333", make: "Honda", model: "Accord"},
            {rego: "BBB-222", make: "Holden", model: "Commodore"},
        ]
    }

    function addCarMessageHandler(event) {
        // cars.push({rego: newRego, make: newMake, model: newModel});
        // cars = cars;
        cars = [...cars, {rego: event.detail.rego, make: event.detail.make, model: event.detail.model}];

        console.log(cars);
    }

    async function getCars() {
        // const response = await fetch('https://my.api.mockaroo.com/cars.json?key=47956d40');
        // const data = await response.json();
        // console.log(data);

        const response = await fetch('https://my.api.mockaroo.com/cars.json?key=47956d40')
                        .then(response => response.json())
                        .catch(error => {
                            console.log("error: ", error);
                            createDefaultCars();
                        });

        if(response.error) {
            console.log("error: ", response.error);
            createDefaultCars();
        } else {
            cars = response;
        }
    }

    function handleRegoClick(event) {
        console.log(event.detail.rego);

        // find the car with the rego that was clicked
        var foundCar = cars.filter(car => {
            return car.rego === event.detail.rego;
        })
        console.log(foundCar[0]);

        cdRego = foundCar[0].rego;
        cdMake = foundCar[0].make;
        cdModel = foundCar[0].model;

    }  

</script>

<h1>Mockaroo Cars application</h1>
<CarDetail rego={cdRego} make={cdMake} model={cdModel}/>

<CarsInput on:addCar={addCarMessageHandler}/>


{#if cars.length > 0}
    <CarsList carsList={cars} on:regoClick={handleRegoClick}/>
{:else}
    <p>Please wait while I'm fetching some cars for you</p>
{/if}


<style>
  h1 {
    color: red;
  }


</style>
