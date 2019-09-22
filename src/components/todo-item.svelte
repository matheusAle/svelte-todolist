<script>
    export let item;

</script>
<style>
    .todo-item {
        width: 100%;
        padding: .9rem 1.5rem;
        cursor: pointer;
        background: white;
        margin: 8px 0;
        border-radius: 5px;
        transition: box-shadow 200ms ease-out, color 200ms ease-out, background-color 200ms ease-out;
        color: #484848;
        position: relative;
    }

    .todo-item:hover {
        box-shadow: 0px 2px 4px 0 rgba(0,0,0,0.1);
    }

    .todo-item.item--completed {
        color: #a5a5a5;
        background-color: rgba(255,255,255,0.63);
    }

    .todo-item.item--completed:before {
        content: ' ';
        width: 0%;
        position: absolute;
        top: calc(50% - 1px);
        left: 0;
        height: 2px;
        background-color: #9a9a9a;
        animation: completedStroke 0ms forwards 200ms ease-out;
    }

    @keyframes completedStroke {
        0% {
            width: 0;
        }
        100% {
            width: 100%;
        }
    }

</style>
<li class="todo-item" class:item--completed="{item.completed}">
    <p>
        {item.text}
    </p>
</li>
