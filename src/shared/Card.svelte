<div class="poll-card">
    <slot />
</div>

<style>
    .poll-card {
        display: flex;
        flex-direction: column;
        width: 445px;
        background-color: #ffffff;
        box-shadow: 0 2px 5px #e3e3e3;
        border: 0 solid;
        border-radius: 5px;
        padding: 1rem;
        margin: 0 1rem;
        gap: 1rem;
    }

    @media (max-width: 500px) {
        .poll-card {
            width: 90vw;
            min-width: 300px;
        }
    }
</style>
