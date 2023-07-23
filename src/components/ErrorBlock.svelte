<script>
    export let error
</script>

<div class="error-block">
    <h2 class="title">{error.title}</h2>
    <p class="message">{error.message}</p>
    <p class="resolution">{error.resolution}👍🏾</p>
</div>

<style>
    .error-block {
        text-align: center;
    }

    .title,
    .message {
        margin-bottom: var(--size-400);
    }

    .title {
        font-size: var(--fs-600);
        color: var(--clr-error);
    }

    .message,
    .resolution {
        color: var(--clr-bg-sec);
    }
</style>