<svelte:options tag={"selection-menu"} />

<script>
    export let i;
    export let title = "";
    export let openbody = false;
    export let agreedn = false;

    async function handle() {
        agreedn = !agreedn;
        this.dispatchEvent(
            new CustomEvent("newsetting", {
                bubbles: true,
                detail: { element: i },
            })
        );
    }
</script>

<div class="titleselectioncontainer">
    <div class="secondaryt mb0">{title}</div>
    <div class="displayflex alignitems-c">
        <div
            class="displayflex cursor-p mr-2375"
            on:keydown
            on:click={() => {
                openbody = !openbody;
            }}
        >
            <div class="hidedesc">
                {openbody ? "Nascondi descrizione" : "Mostra descrizione"}
            </div>
            <div class="expand">
                <svg
                    width="12"
                    height="8"
                    viewBox="0 0 12 8"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                    style="margin-bottom: 1px"
                >
                    {#if openbody}
                        <path
                            d="M6 0L0 6L1.41 7.41L6 2.83L10.59 7.41L12 6L6 0Z"
                            fill="#424242"
                        />
                    {:else}
                        <path
                            d="M10.59 0.589844L6 5.16984L1.41 0.589844L0 1.99984L6 7.99984L12 1.99984L10.59 0.589844Z"
                            fill="#424242"
                        />
                    {/if}
                </svg>
            </div>
        </div>
        <div class="switch" on:keydown on:click={handle}>
            {#if !agreedn}
                <svg
                    width="49"
                    height="26"
                    viewBox="0 0 49 26"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <rect
                        x="1"
                        y="1"
                        width="48"
                        height="24"
                        rx="12"
                        fill="#A5A5A5"
                    />
                    <rect
                        x="0.5"
                        y="0.5"
                        width="25"
                        height="25"
                        rx="12.5"
                        fill="white"
                    />
                    <rect
                        x="0.5"
                        y="0.5"
                        width="25"
                        height="25"
                        rx="12.5"
                        stroke="white"
                    />
                </svg>
            {:else}
                <svg
                    width="49"
                    height="26"
                    viewBox="0 0 49 26"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <rect
                        y="1"
                        width="48"
                        height="24"
                        rx="12"
                        fill="#2D3648"
                        fill-opacity="0.5"
                    />
                    <rect
                        x="23.5"
                        y="0.5"
                        width="25"
                        height="25"
                        rx="12.5"
                        fill="white"
                    />
                    <rect
                        x="23.5"
                        y="0.5"
                        width="25"
                        height="25"
                        rx="12.5"
                        stroke="white"
                    />
                </svg>
            {/if}
        </div>
    </div>
</div>
