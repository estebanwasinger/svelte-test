<script>
    export let username;
    export let description;
    export let pos

    import { createEventDispatcher} from "svelte";

    const dispatch = createEventDispatcher();

    function onRemove() {
        dispatch('remove', {pos : pos})
    }
</script>

<div class="profile">
    <h1>{username} - {pos}</h1>
    <p>{description}</p>
    <button on:click={onRemove} >Remove</button>
</div>
