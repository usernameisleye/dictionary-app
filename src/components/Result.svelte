<script>
  import Block from "./Block.svelte"
  import { store } from "../store"
</script>

{#if $store}
    <section class="result">
        <div class="head">
            <div>
                <h2 class="word">{$store[0].word}</h2>
                <p class="phonetics">{$store[0].phonetics[0].text}</p>
            </div>
            <button aria-label="play-button" class="play">
                <svg 
                    xmlns="http://www.w3.org/2000/svg" 
                    width="0.75em" 
                    height="1em" 
                    viewBox="0 0 384 512"
                >
                    <path 
                        fill="#FFF" 
                        d="M73 39c-14.8-9.1-33.4-9.4-48.5-.9S0 62.6 0 80v352c0 17.4 9.4 33.4 24.5 41.9S58.2 482 73 473l288-176c14.3-8.7 23-24.2 23-41s-8.7-32.2-23-41L73 39z"
                    />
                </svg>
            </button>
        </div>

        {#each $store[0].meanings as meaning}
            <Block 
                head={meaning.partOfSpeech} 
                meaning={meaning.definitions}
            />
        {/each}

        <div class="link">
            <small>Source</small>
            <div class="target">
                <a href={$store[0].sourceUrls} target="_blank">{$store[0].sourceUrls}</a>
                <img 
                    src="/static/link.svg"
                    alt="Link icon"
                >
            </div>
        </div>
    </section>
{/if}

<style>
    .result {
        display: grid;
        grid-template-columns: repeat(1, minmax(0, 1fr));
        gap: var(--size-500);
        color: var(--clr-text);
    }

    /* Head */
    .result .head {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .word {
        font-size: var(--fs-700);
    }

    .phonetics {
        font-size: var(--fs-600);
        color: var(--clr-accent);
    }

    .play {
        background: var(--clr-accent-dim);
        height: var(--size-800);
        width: var(--size-800);
        border-radius: 100%;
        display: grid;
        place-items: center;
    }

    .play:hover {
        background: var(--clr-accent);
    }

    .play svg path {
        fill: var(--clr-accent);
    }

    .play:hover svg path {
        fill: white;
    }

    .example {
        font-family: monospace;
        font-size: var(--fs-500);
        color: var(--clr-bg-sec);
    }

    .link {
        display: flex;
        flex-wrap: wrap;
        gap: var(--size-300);
        font-family: monospace;
        font-size: var(--fs-400);
        color: var(--clr-bg-sec);
        padding-top: var(--size-500);
        text-decoration: underline;
        border-top: 1px solid var(--clr-border-line);
    }

    .link .target a {
        color: var(--clr-text);
    }

    .link .target img {
        display: inline;
    }
</style>