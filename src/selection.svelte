<svelte:options tag={"selection-menu"} />

<script>
    export let title = "";
</script>

<div class="titleselectioncontainer">
    <div class="secondaryt mb0">{title}</div>
    <div class="displayflex alignitems-c">
        <div class="displayflex cursor-p mr-2375">
            <div class="hidedesc">Nascondi descrizione</div>
            <div class="expand">
                <svg
                    width="12"
                    height="8"
                    viewBox="0 0 12 8"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                    style="margin-bottom: 1px"
                >
                    <path
                        d="M6 0L0 6L1.41 7.41L6 2.83L10.59 7.41L12 6L6 0Z"
                        fill="#424242"
                    />
                </svg>
            </div>
        </div>
        <div class="switch">
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
        </div>
    </div>
</div>
