<script>
    let getTheme
    let theme

    const toggle = () => {
        getTheme = document.documentElement.getAttribute("data-theme")
        theme = getTheme == "dark" ? "light" : "dark"

        document.documentElement.setAttribute('data-theme', theme)
    }
</script>

<header>
    <img 
        src="/static/Logo.svg" 
        alt="Logo"
    >

    <div class="settings">
        <div></div>

        <button id="theme-toggle" on:click={toggle}>
            {#if theme == "dark"}
                <img 
                    src="/static/sun.svg" 
                    alt="Sun icon" 
                >

            {:else}
                <img 
                    src="/static/moon.svg"
                    alt="Moon icon"
                >
            {/if}
        </button>
    </div>
 
</header>

<style>
    header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        --width: 9rem;
    }

    header > img {
        width: var(--width);
    }

    .settings button {
        padding: var(--size-200);
        background: var(--clr-bg-dim);
        border-radius: var(--size-100);
    }

    .settings button img {
        width: var(--size-500);
    }
</style>