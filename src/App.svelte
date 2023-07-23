<script>
    import Header from "./components/Header.svelte"
    import Result from "./components/Result.svelte"
    import ErrorBlock from "./components/ErrorBlock.svelte"

  let search = ""
  let error = null
  let data = null
  let loading = false
  let disabled = false

  const getData = async () => {
    if(search === "") return
    disabled = true
    loading = true
    error = null
    data = null

    try {
        const url = `https://api.dictionaryapi.dev/api/v2/entries/en/${search}`
        const r = await fetch(url)
        const rjson = await r.json()
        if (!r.ok) {
            error = rjson
            return
        }

        data = rjson
    }
    catch(err) {
        console.error(error.message)
    }
    finally {
        disabled = false
        loading = false
    }
}
</script>

<svelte:document on:keypress={e => {
    if(e.key === "Enter") 
    {
        getData()
    }
}} />

<main>  
    <Header />
    
    <div class="search">
        <div class="input">
            <input 
                type="text"
                bind:value={search}
                placeholder="Search dictionary"
            >
            
            <img 
                src="/static/search.svg" 
                alt="Search icon"
            >
        </div>

        <button {disabled} on:click={getData}>Search</button>
    </div>

    {#if loading}
        <div class="loading">
            <img 
                src="/static/load.svg" 
                alt="Loading..."
            >
        </div>
    {:else if data}
        <Result {data} />
    {:else if error}
        <ErrorBlock {error} />
    {:else}
        <h2 class="default">Search for a word🔎</h2>
    {/if}
</main>


<style>
    :global(input, button) {
        border: none;
        outline: none;
        background: none;
    }

    main {
        display: grid;
        max-width: 60%;
        overflow-x: hidden;
        margin-inline: auto;
        margin-block: var(--size-800);
    }

    .search {
        background: var(--clr-bg-dim);
        height: fit-content;
        width: 100%;
        display: flex;
        padding: var(--size-300);
        justify-content: space-between;
        border-radius: var(--size-700);
        margin-block: var(--size-800) var(--size-600);
    }

    .search .input {
        position: relative;
        flex-grow: 1;
    }

    .search .input input {
        width: 100%;
        color: var(--clr-text);
        padding-block: var(--size-300);
        padding-left: var(--size-700);
    }

    .search .input img {
        position: absolute;
        top: 50%;
        left: 1.5%;
        transform: translateY(-50%);
        width: var(--size-500);
    }

    .search button {
        color: white;
        padding-inline: var(--size-700);
        border-radius: var(--size-600);
        background: var(--clr-accent);
    }

    .search button:hover,
    .search button:focus-within {
        filter: brightness(110%);
    }

    .search button:disabled {
        background: var(--clr-bg-sec);
        cursor: not-allowed;
    }

    .default {
        font-size: var(--fs-600);
        color: var(--clr-accent);
        text-align: center;
    }

    .loading {
        display: grid;
        place-items: center;
    }

    .loading img {
        width: var(--size-900);
    }

    @media (max-width: 50em) {
        main {
            max-width: 100%;
            padding: var(--size-500);
            margin-block: var(--size-600);
        }

        .search button {
            padding-inline: var(--size-600);
        }
    }
</style>