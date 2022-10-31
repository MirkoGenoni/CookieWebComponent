<svelte:options tag={"cookie-preferences"} />

<script>
    import Selection from "./selection.svelte";

    const sectionsTitle = [
        "Cookie e tecnologie necessarie",
        "Personalizzazione del sito",
        "Pubblicità personalizzata",
    ];
    const sectionsBodies = [
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh.",
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh.",
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh.",
    ];
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
    Gestisci preferenze
</div>
<div class="maintext">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque
    dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum
    tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu.
    Habitant felis feugiat purus tincidunt quam sed nibh.
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
