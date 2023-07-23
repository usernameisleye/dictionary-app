<script>
  import Block from "./Block.svelte"

  export let data
  const { word, phonetics, origin, meanings, sourceUrls } = data[0]

  const speak = () => {
    let speech = new SpeechSynthesisUtterance(word)
    speechSynthesis.speak(speech)
  }
</script>

{#if data}
    <section class="result">
        <div class="head">
            <div>
                <h2 class="word">{word}</h2>
                {#if phonetics[0].text} 
                    <p class="phonetics">{phonetics[0].text}</p>
                {/if}
            </div>

            <button aria-label="play-button" class="play" on:click={speak}>
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

        {#each meanings as meaning}
            <Block {meaning} />
        {/each}

        {#if origin}
            <div class="origin">
                <small>Origin</small>
                <small class="content">{origin}</small>
            </div>
        {/if}

        <div class="link">
            <small>Source</small>
            <div class="target">
                <a href={sourceUrls} target="_blank">{sourceUrls}</a>
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

    .link, 
    .origin {
        display: flex;
        flex-wrap: wrap;
        gap: var(--size-300);
        font-family: monospace;
        font-size: var(--fs-400);
        color: var(--clr-bg-sec);
        padding-top: var(--size-500);
    }

    .link {
        text-decoration: underline;
        border-top: 1px solid var(--clr-border-line);
    }

    .link .target a,
    .origin .content {
        color: var(--clr-text);
    }

    .link .target img {
        display: inline;
    }
</style>