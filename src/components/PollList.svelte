<script>
    import { fade, scale } from "svelte/transition";
    import { flip } from "svelte/animate";
    import PollStore from "../store/PollStore.js";
    import VoteDetails from "./VoteDetails.svelte";
</script>

<div class="polls-container">
    {#each $PollStore as poll (poll.id)}
        <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
            <VoteDetails {poll} />
        </div>
    {/each}
</div>

<style>
    .polls-container {
        display: flex;
        gap: 2rem;
        justify-content: flex-start;
        align-items: flex-end;
        width: 100%;
        flex-wrap: wrap;
    }

    @media (max-width: 1150px) {
        .polls-container {
            justify-content: center;
            align-items: flex-end;
        }
    }
</style>
