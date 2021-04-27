<script lang="ts">
	import Profile from "./Profile.svelte";
	export let name: string = "";
	export let description: string = "";
	let disabled: boolean = true;
	let clearDisabled: boolean = true;
	let users = []



	function add() {
		users = [...users,{
			name : name,
			desc : description
		}]
		name = ""
		description = ""

	}

	function remove(event) {
		let data = event.detail.pos;
		console.log(data)
		users = users.slice(0,data).concat(users.slice(data+1))
		console.log(users)
	}

	function clear() {
		users = []
	}

	$: disabled = name === "" || description === ""
	$: clearDisabled = users.length === 0

	// $ : name =

</script>

<main>
	Name <input bind:value="{name}"/><br>
	Description <input bind:value="{description}"/><br>
	<button on:click={add} disabled={disabled}>Add</button>
	<button on:click={clear} disabled={clearDisabled}>Clear</button>
	{#each users as user, i}
		<Profile username="{user.name}" description="{user.desc}" on:remove={remove} pos={i} />
	{/each}


	</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
