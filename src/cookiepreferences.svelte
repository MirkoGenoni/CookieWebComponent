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
</script>

<div class="maintitle" style="margin-top: 2rem">Gestisci preferenze</div>
<div class="maintext">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque
    dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum
    tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu.
    Habitant felis feugiat purus tincidunt quam sed nibh.
</div>
{#each sectionsTitle as title, i}
    <Selection {title} />
    <div class="secondaryb" style="font-weight: 500; margin-bottom: 1rem;">
        {sectionsBodies[i]}
    </div>
    {#if i < sectionsBodies.length - 1}
        <div class="divider" />
    {/if}
{/each}
<div
    class="closebutton"
    on:click={() => {
        openpref = false;
    }}
    style="margin-top: 3.5rem; align-self: flex-end;"
>
    Salva e continua
</div>
