<svelte:options tag={"cookie-policy"} />

<script>
    import { settings } from "./settings.svelte";

    export let openpolicy;
    export let theme;

    const maintitle = settings.policy_main_title;
    const mainbody = settings.policy_main_body;
    const titles = settings.policy_titles;
    const bodies = settings.policy_bodies;
</script>

<div
    id="policy"
    class:darkcontainer={theme == "dark"}
    class:lightcontainer={theme == "light"}
>
    <div id="containerpolicy">
        <div class="maintitle" class:darktitle={theme == "dark"}>
            {maintitle}
        </div>
        <div class="maintext">{mainbody}</div>
        {#each titles as title, i}
            <div class="secondaryt" class:darktitle={theme == "dark"}>
                {title}
            </div>
            <div class="secondaryb">{bodies[i]}</div>
        {/each}
        <div class="bottomcontainerpolicy">
            <div
                class="closebutton"
                on:keydown
                on:click={() => {
                    openpolicy = false;
                }}
            >
                Chiudi
            </div>
        </div>
    </div>
</div>
