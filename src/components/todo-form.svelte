<script>
    import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	let todo = '';

	function add(event) {
	    if (event.code !== 'Enter' || !todo.trim()) {
            return;
        }

	  dispatch('submit', { todo: { text: todo, completed: false, id: Date.now() } });
	  todo = '';
	}
</script>
<style>
    .form {
        width: 100%;
        padding: 20px 0;
    }

    .form_field {
        width: 100%;
        display: block;
        outline: none;
        border: none;
        font-size: 14px;
        text-align: center;
        background-color: transparent;
    }
</style>
<div class="form">
    <input type="text" class="form_field" bind:value={todo} on:keyup={add} placeholder="press enter to add a item...">
</div>
