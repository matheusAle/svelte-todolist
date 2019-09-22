<script>
    import TodoForm from './components/todo-form.svelte';
    import TodoItem from './components/todo-item.svelte';
	import { flip } from 'svelte/animate';

    import { crossfade } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

    const [send, receive] = crossfade({
        duration: d => Math.sqrt(d * 200),

        fallback(node, params) {
            const style = getComputedStyle(node);
            const transform = style.transform === 'none' ? '' : style.transform;

            return {
                duration: 350,
                easing: quintOut,
                css: t => `
                    transform: ${transform} scale(${t});
                    opacity: ${t}
                `
            };
        }
    });

    let todos = [
    ];

    function add({ detail: { todo } }) {
      todos = [todo, ...todos];
      console.log(todos);
    }

    function toggleMark(todo) {
      console.log(todos);
      todos[todo].completed = !todos[todo].completed;
      todos = [ ...todos.filter(t => !t.completed), ...todos.filter(t => t.completed) ]
    }

</script>

<style>
	.app {
	    max-width: 978px;
	    width: 978px;
	    margin: auto;
	    padding-top: 30px;
	}

	.app__title h1 {
        font-weight: 100;
        font-size: 50px;
        text-align: center;
        text-transform: uppercase;
        color: rgba(0,0,0,0.38);
	}

	.app__form {
	    margin-top: 50px;
	    width: 100%;
	}


    @media (max-width: 450px){
        .app {
            margin: 0 50px;
            width: unset;
        }
    }
</style>

<div class="app">
    <div class="app__title">
        <h1>
            Todo
        </h1>
    </div>

    <div class="app__form">
        <TodoForm on:submit={add} />
    </div>
    <div class="app__list">
        <ul>
            {#each todos as todo, index (todo.id)}
                <div in:receive="{{key: todo.id}}" out:send="{{key: todo.id}}" animate:flip on:click={() => toggleMark(index)}>
                    <TodoItem item={todo} />
                </div>
            {/each}
        </ul>
    </div>
</div>
