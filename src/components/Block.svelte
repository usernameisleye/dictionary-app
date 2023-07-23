<script>
    export let meaning

    const { partOfSpeech, definitions, synonyms } = meaning
</script>

<div class="block">
    <h4>{partOfSpeech}</h4>

    <div class="content">
        <p>Meaning</p>
        <!-- svelte-ignore a11y-no-redundant-roles -->
        <ul role="list">
            {#each definitions.slice(0, 4) as d}
                <li>{d.definition}</li>
            {/each}
        </ul>
    </div>

    {#if synonyms.length > 0}
        <div class="syn">
            <span>Synonyms</span>
            <span class="res">{synonyms.slice(0, 6)}</span>
        </div>
    {/if}

    {#if definitions[0].example}  
        <p class="example">"{definitions[0].example}"</p>
    {/if}
</div>



<style>
    .block {
        display: grid;
        gap: var(--size-400);
    }

    .block h4 {
        font-size: var(--fs-600);
        font-style: italic;
        position: relative;
        /* margin-bottom: var(--size-400); */
    }

    .block h4::after {
        content: "";
        position: absolute;
        height: 1px;
        width: 100%;
        top: 50%;
        margin-left: var(--size-300);
        background: var(--clr-border-line);
    }

    .content p,
    .example {
        font-family: monospace;
        font-size: var(--fs-500);
        color: var(--clr-bg-sec);
    }

    .content ul {
        display: grid;
        gap: var(--size-400);
        margin-top: var(--size-400);
    }

    .content ul li {
        font-size: var(--fs-500);
    }

    .content ul li::before {
        content: url("/static/dot.svg");
        margin-right: 2px;
    }

    .syn {
        font-family: monospace;
        font-size: var(--fs-500);
    }

    .syn .res {
        color: var(--clr-accent);
        font-weight: var(--fw-bold);
        margin-left: var(--size-200);
    }
</style>