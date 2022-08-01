<script>
    export let type = "primary";
    export let flat = false;
</script>

<button class={type} class:flat={!flat} on:click>
    <slot />
</button>

<style>
    button {
        font-weight: bold;
        font-size: 16px;
        color: #ffffff;
        border: 0 solid;
        border-radius: 5px;
        padding: 0.6rem;
    }

    button:hover {
        cursor: pointer;
    }

    .primary {
        background-color: #50c29c;
        box-shadow: 0 5px 10px #d3d3d3;
    }

    .secondary {
        background-color: #cd0202;
        align-self: center;
        padding: 0.6rem 1rem;
    }

    .primary:hover {
        background-color: #48b691;
    }

    .secondary:hover {
        background-color: #be0000;
    }

    .flat {
        box-shadow: none;
    }
</style>
