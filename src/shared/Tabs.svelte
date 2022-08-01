<script>
    import { createEventDispatcher } from "svelte";

    export let items;
    export let activeItem;

    const dispatch = createEventDispatcher();
</script>

<div class="tabs">
    <ul>
        {#each items as item}
            <li
                class:active={item === activeItem}
                on:click={() => dispatch("switchTab", item)}
            >
                {item}
            </li>
        {/each}
    </ul>
</div>

<style>
    .tabs {
        margin-bottom: 2rem;
    }

    ul {
        list-style-type: none;
        display: flex;
        justify-content: center;
        gap: 2rem;
    }

    li:hover {
        cursor: pointer;
    }

    .active {
        color: #d91b42;
        border-bottom: 2px solid #d91b42;
        padding-bottom: 0.5rem;
    }
</style>
