<svelte:options tag={"cookie-preferences"} />

<script>
    import { settings } from "./settings.svelte";
    import Selection from "./selection.svelte";

    const mainTitle = settings.preferences_main_title;
    const mainBody = settings.preferences_main_body;
    const sectionsTitle = settings.preferences_sections_titles;
    const sectionsBodies = settings.preferences_sections_bodies;

    export let openpref;
    export let opensection = new Array(sectionsBodies.length).fill(false);
    export let agreed = [];
    export let blocked = [];
    export let theme;

    //VARIABLE THAT TRIGGERS PAGE RELOAD
    let openbody;
</script>

<div
    class="maintitle"
    style="margin-top: 2rem"
    class:darktitle={theme == "dark"}
>
    {mainTitle}
</div>
<div class="maintext">
    {mainBody}
</div>
{#each sectionsTitle as title, i}
    <Selection
        {i}
        {title}
        bind:openbody={opensection[i]}
        agreedn={agreed[i]}
        blocked={blocked[i]}
        {theme}
    />
    {#if opensection[i] || blocked[i]}
        <div class="secondaryb" style="font-weight: 500; margin-bottom: 1rem;">
            {sectionsBodies[i]}
        </div>
    {/if}
    {#if i < sectionsBodies.length - 1}
        <div class="divider" />
    {/if}
{/each}
<div
    class="closebutton"
    on:keydown
    on:click={() => {
        openpref = false;
    }}
    style={opensection[sectionsBodies.length]
        ? "margin-top: 3.5rem; align-self: flex-end;"
        : "margin-top: 2.5rem; align-self: flex-end;"}
>
    Salva e continua
</div>
