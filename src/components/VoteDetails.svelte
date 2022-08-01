<script>
    import { tweened } from "svelte/motion";
    import PollStore from "../store/PollStore";
    import Button from "../shared/Button.svelte";
    import Card from "../shared/Card.svelte";

    export let poll;

    $: totalVotes = poll.voteA + poll.voteB;
    $: percentA = Math.floor((poll.voteA / totalVotes) * 100) || 0;
    $: percentB = Math.floor((poll.voteB / totalVotes) * 100) || 0;

    const widthA = tweened(0);
    const widthB = tweened(0);
    $: widthA.set(percentA);
    $: widthB.set(percentB);

    const handleVote = (id, option) => {
        PollStore.update((currentPolls) => {
            let copiedPolls = [...currentPolls];
            let updatedPoll = copiedPolls.find((poll) => poll.id === id);

            if (option === "a") {
                updatedPoll.voteA++;
            } else if (option === "b") {
                updatedPoll.voteB++;
            }

            return copiedPolls;
        });
    };

    const handleDelete = (id) => {
        PollStore.update((currentPolls) => {
            return currentPolls.filter((poll) => poll.id !== id);
        });
    };
</script>

<Card>
    <div class="title">
        <h3>{poll.question}</h3>
        <p>Total votes: {totalVotes}</p>
    </div>

    <div class="answer" on:click={() => handleVote(poll.id, "a")}>
        <div class="percent percent-a" style="width: {$widthA}%;" />
        <span>{poll.answerA} ({poll.voteA})</span>
    </div>
    <div class="answer" on:click={() => handleVote(poll.id, "b")}>
        <div class="percent percent-b" style="width: {$widthB}%;" />
        <span>{poll.answerB} ({poll.voteB})</span>
    </div>

    <Button
        type="secondary"
        flat={true}
        on:click={() => {
            handleDelete(poll.id);
        }}>Delete</Button
    >
</Card>

<style>
    p {
        font-size: 14px;
        color: #6d6d6d;
    }

    .answer {
        background-color: #f9f9f9;
        padding: 0.5rem 1rem;
        text-align: left;
        position: relative;
    }

    .answer:hover {
        cursor: pointer;
        opacity: 0.8;
    }

    .percent {
        position: absolute;
        height: 100%;
        top: 0;
        left: 0;
        display: flex;
        z-index: 0;
    }

    .percent-a {
        background-color: rgba(27, 171, 111, 0.4);
        border-left: 4px solid #1bab6f;
    }

    .percent-b {
        background-color: rgba(230, 37, 53, 0.4);
        border-left: 4px solid #e62535;
    }
</style>
