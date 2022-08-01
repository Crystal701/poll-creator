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
        gap: 1rem;
    }

    @media (max-width: 450px) {
        .poll-card {
            max-width: 445px;
            min-width: 300px;
            margin: 0 1rem;
        }
    }
</style>
