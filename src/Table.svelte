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

    <table>
			<tr>
                <th>ID</th>
                <th>Store</th>
                <th>Address</th>
            </tr>
		
            {#each stores as {name, address}, i}
			    <tr on:click={() => sayId(i)}> 
                    <td>{i}</td>
                    <td>{name}</td> 
				    <td>{address}</td> 
			    </tr>
		    {/each}
	</table>

<style>
	table, th, td {
		border: 1px solid black;
        border-collapse: collapse;
        padding: 5px;
	}
</style>
