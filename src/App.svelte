<script>
	
    import Table from "./Table.svelte";
	
    let store  = {};
	let editIndex = undefined;
    let stores = [{"name": "A long, long, long name", "address": "A much longer address, with street or avenue, city, post code, state, country, and much more, like floor, room, desk...."}];

	let updateStore = () => {
		stores[editIndex-1] = store;
		stores = [...stores];
        store = {};
		editIndex = undefined;
	}

	let addStore = () => {
		stores = [...stores, store];
        store = {};
	}

	let removeStore = () => {
		let store = stores.splice(selectedStoreId, 1)[0];
		stores = [...stores];
        return store;
	}

	let editStore = () => {
		editIndex = selectedStoreId+1;
		store = {...stores[selectedStoreId]};
	}

	let cancelEdit = () => {
        store = {};
		editIndex = undefined;
	}

    let selectedStoreId;

	function handleMessage(event) {
        selectedStoreId = event.detail.id;
	}
</script>

<main>
	<div>
	    <input type="text" bind:value={store.name} placeholder="Store's name"> 
			<input type="text" bind:value={store.address} placeholder="Store's address"> 

			{#if editIndex }
                <button on:click={() => updateStore()}>Edit</button>
				<button on:click={() => cancelEdit()}>Cancel</button>
			{:else}
				<button on:click={() => addStore()}>Add Store</button>
			{/if}
	</div>
	<hr/>
    {#if selectedStoreId != undefined}    
        <h4>Selected store: {selectedStoreId}</h4>
        <button on:click={() => editStore()}>Edit</button>
        <button on:click={() => removeStore()}>Remove</button>
    {:else}
        <h4>No Store Selected</h4>
    {/if}

	<Table {stores} on:message={handleMessage}/>
</main>
