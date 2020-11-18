<script>
	export let stores = [];
    import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function sayId(index) {
		dispatch('message', {
			id: index
		});
    }
</script>	

    <table class="customTable">
        <thead>	
            <tr>
                <th>ID</th>
                <th>Store</th>
                <th>Address</th>
            </tr>
        </thead>
        <tbody>
            {#each stores as {name, address}, i}
			    <tr on:click={() => sayId(i)}> 
                    <td>{i}</td>
                    <td>{name}</td> 
				    <td>{address}</td> 
			    </tr>
		    {/each}
        </tbody>
	</table>

<style>
    table.customTable {
        width: 100%;
        background-color: #55b9f3;
        border-collapse: separate;
        border-width: 2px;
        border-color: #0f0f0f;
        border-style: solid;
        color: #000000;
    }
    table.customTable td, table.customTable th {
        border-width: 2px;
        border-color: #0f0f0f;
        border-style: solid;
        padding: 5px;
    }

    table.customTable thead {
        background-color: #55b9f3;
    }
    table.customTable td, table.customTable th {
        border-width: 2px;
        border-color: #0f0f0f;
        border-style: solid;
        padding: 5px;
    }
</style>
