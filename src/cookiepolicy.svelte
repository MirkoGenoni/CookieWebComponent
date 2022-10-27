<svelte:options tag={"cookie-policy"} />

<script>
    export let openpolicy;
    const titles = [
        "Lorem ipsum dolor sit amet",
        "Lorem ipsum dolor sit amet",
        "Lorem ipsum dolor sit amet",
    ];
    const bodies = [
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh.",
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh.",
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean dolor eget netus non, imperdiet et, elementum tincidunt integer. Mauris vulputate in magna suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt quam sed nibh.",
    ];
</script>

<div id="fullpage">
    <div id="policy">
        <div id="containerpolicy">
            <div id="title">Cookie Policy</div>
            <div id="text">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Massa
                quisque dictumst nisl volutpat. Aenean dolor eget netus non,
                imperdiet et, elementum tincidunt integer. Mauris vulputate in
                magna suspendisse pulvinar eu. Habitant felis feugiat purus
                tincidunt quam sed nibh. Lorem ipsum dolor sit amet, consectetur
                adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean
                dolor eget netus non, imperdiet et, elementum tincidunt integer.
                Mauris vulputate in magna suspendisse pulvinar eu. Habitant
                felis feugiat purus tincidunt quam sed nibh. Lorem ipsum dolor
                sit amet, consectetur adipiscing elit. Massa quisque dictumst
                nisl volutpat. Aenean dolor eget netus non, imperdiet et,
                elementum tincidunt integer. Mauris vulputate in magna
                suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt
                quam sed nibh. Lorem ipsum dolor sit amet, consectetur
                adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean
                dolor eget netus non, imperdiet et, elementum tincidunt integer.
                Mauris vulputate in magna suspendisse pulvinar eu. Habitant
                felis feugiat purus tincidunt quam sed nibh.Lorem ipsum dolor
                sit amet, consectetur adipiscing elit. Massa quisque dictumst
                nisl volutpat. Aenean dolor eget netus non, imperdiet et,
                elementum tincidunt integer. Mauris vulputate in magna
                suspendisse pulvinar eu. Habitant felis feugiat purus tincidunt
                quam sed nibh. Lorem ipsum dolor sit amet, consectetur
                adipiscing elit. Massa quisque dictumst nisl volutpat. Aenean
                dolor eget netus non, imperdiet et, elementum tincidunt integer.
                Mauris vulputate in magna suspendisse pulvinar eu. Habitant
                felis feugiat purus tincidunt quam sed nibh.
            </div>
            {#each titles as title, i}
                <div class="titleparagrafo">{title}</div>
                <div class="bodyparagrafo">{bodies[i]}</div>
            {/each}
            <div class="bbottomcontainer">
                <div class="closebutton" on:click={()=>{openpolicy=false}}>Chiudi</div>
            </div>
        </div>
    </div>
</div>
