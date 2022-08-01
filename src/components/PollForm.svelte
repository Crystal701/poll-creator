<script>
    import { createEventDispatcher } from "svelte";
    import PollStore from "../store/PollStore";
    import Button from "../shared/Button.svelte";

    let poll = {
        id: Math.random(),
        question: "",
        answerA: "",
        answerB: "",
        voteA: 0,
        voteB: 0,
    };

    let valid = false;
    let error = { question: "", answerA: "", answerB: "" };
    const dispatch = createEventDispatcher();

    const handleSubmit = () => {
        valid = true;

        if (poll.question.trim().length < 5) {
            valid = false;
            error.question = "Question must be more than 5 words";
        } else {
            error.question = "";
        }

        if (poll.answerA.trim() === "") {
            valid = false;
            error.answerA = "Answer A cannot be empty";
        } else {
            error.answerA = "";
        }

        if (poll.answerB.trim() === "") {
            valid = false;
            error.answerB = "Answer B cannot be empty";
        } else {
            error.answerB = "";
        }

        if (valid) {
            PollStore.update((currentPolls) => {
                return [poll, ...currentPolls];
            });
        }
        dispatch("handleSubmit");
    };
</script>

<form on:submit|preventDefault={handleSubmit}>
    <label for="question">Poll Question:</label>
    <input type="text" id="question" bind:value={poll.question} />
    <p class="error">{error.question}</p>

    <label for="answer-a">Answer A:</label>
    <input type="text" id="answer-a" bind:value={poll.answerA} />
    <p class="error">{error.answerA}</p>

    <label for="answer-b">Answer B:</label>
    <input type="text" id="answer-b" bind:value={poll.answerB} />
    <p class="error">{error.answerB}</p>

    <Button>Add Poll</Button>
</form>

<style>
    form {
        display: flex;
        flex-direction: column;
    }

    input {
        display: block;
        width: 400px;
        padding: 0.6rem;
        border: 1px solid #cdcdcd;
        border-radius: 5px;
        margin-top: 0.5rem;
    }

    p {
        color: red;
        font-weight: bold;
        font-size: 14px;
        padding-bottom: 1rem;
    }

    @media (max-width: 450px) {
        form {
            max-width: 445px;
            min-width: 300px;
            margin: 0 1rem;
        }
    }
</style>
