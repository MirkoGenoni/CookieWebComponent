<svelte:options tag={"cookie-banner"} />

<script>
	import Cookiepolicy from "./cookiepolicy.svelte";
	import Cookiepreferences from "./cookiepreferences.svelte";
	import { onDestroy, onMount } from "svelte";

	//file that will be received from backend
	import { settings } from "./settings.svelte";

	export let theme = "light";

	//Handle the page modals
	let openpolicy = false;
	let openpref = false;

	//Bind for main element
	let rootElement;

	let agreed = settings.agreed; //Initial agreed cookie preferences
	let blocked = settings.blocked; // Cookie preferences blocked on true
	let closebanner = settings.closebanner; //Display of the close cross on cookie banner

	let bannercontainerHeight;
	let bannercontainer;
	let margin;
	let innerWidth;

	onMount(async () => {
		//Get the current page
		// const url = window.location.href;
		// var xmlHttp = new XMLHttpRequest();
		// xmlHttp.open("GET", url, false);
		// xmlHttp.send(null);
		//const page = String(xmlHttp.responseText);

		//search for all occurrences of "http" in the page fetched
		//let occurences = page.match(/http.+/g);
		//search for all occurrences of "http" in current header
		const page = document.head.innerHTML;
		let occurrences = page.match(/http.+/g);

		console.log(occurrences);
		console.log(document.head);

		blocked.forEach((curr, index) => {
			if (curr) agreed[index] = true;
		});
		await loadStyle(rootElement, `global.css`);
		rootElement.addEventListener("newsetting", handleSelection);
	});

	onDestroy(async () => {
		rootElement.removeEventListener("newsetting");
	});

	//OLD HANDLING INPUT STRING FROM HTML TAG
	/*export let agreedcookie;
	function parseInput() {
		if (agreedcookie) {
			let agreedstring = agreedcookie
				.split(",")
				.map((item) => item.trim());
			agreedstring.forEach((element) => {
				agreed.push(element == "true" ? true : false);
			});
		}
		if (agreed.length < possibilities) {
			for (let i = 0; i < possibilities - (agreed.length - i); i++) {
				agreed.push(false);
			}
		}
	}*/

	const handleSelection = (e) => {
		if (!blocked[e.detail.element])
			agreed[e.detail.element] = !agreed[e.detail.element];
		agreed = agreed;
	};

	const handleAllSelections = (type) => {
		agreed.forEach((el, index) => {
			if (!blocked[index]) agreed[index] = type;
		});
	};

	//STYLE FROM GLOBAL CSS FILE
	const loadStyle = (root, path) => {
		return new Promise((resolve, reject) => {
			try {
				let temp = document.createElement("link");
				temp.setAttribute("rel", "stylesheet");
				temp.setAttribute("type", "text/css");
				temp.setAttribute("href", path);
				temp.onload = function () {
					resolve();
				};
				root.appendChild(temp);
			} catch (err) {
				reject(err);
			}
		});
	};

	function openPolicy() {
		openpolicy = true;
	}

	$: console.log(agreed);

	function topbottomargin(height) {
		if (settings.position == "center" && height && innerWidth > 812) {
			margin =
				"margin: calc((100vh - " +
				height +
				"px)/2) calc((100% - 60vw)/2)";
		} else {
			margin = "";
		}
	}

	$: topbottomargin(bannercontainerHeight);
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:wght@700&display=swap"
		rel="stylesheet"
	/>
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:wght@500&display=swap"
		rel="stylesheet"
	/>
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<svelte:window bind:innerWidth />
<main bind:this={rootElement}>
	{#if openpolicy == true}
		<Cookiepolicy bind:openpolicy {theme} />
	{:else}
		<div
			class={"bannercontainer globprop " + settings.position}
			class:darkcontainer={theme == "dark"}
			class:lightcontainer={theme == "light"}
			bind:clientHeight={bannercontainerHeight}
			style={settings.position == "center" ? margin : ""}
		>
			<div
				class="fs24 noselection"
				class:darktitle={theme == "dark"}
				class:titleclose={closebanner && !openpref}
			>
				Noi teniamo alla tua Privacy
				{#if closebanner && !openpref}
					<div class="closebanner">
						<svg
							width="20"
							height="20"
							viewBox="0 0 20 20"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
							class="cursor-p"
						>
							<path
								d="M19.3337 2.54602L17.4537 0.666016L10.0003 8.11935L2.54699 0.666016L0.666992 2.54602L8.12033 9.99935L0.666992 17.4527L2.54699 19.3327L10.0003 11.8793L17.4537 19.3327L19.3337 17.4527L11.8803 9.99935L19.3337 2.54602Z"
								fill={theme == "light" ? "#2D3648" : "#E1F4FF"}
							/>
						</svg>
					</div>
				{/if}
			</div>

			<div class="body noselection">
				Facendo clic su "Accetta tutti i cookie", accetti la
				memorizzazione dei cookie sul tuo dispositivo per migliorare la
				navigazione del sito, analizzare l'utilizzo del sito e assistere
				nelle nostre attività di marketing, come specificato nella <a
					class="cursor-p"
					on:click|preventDefault={openPolicy}
					href={undefined}>Cookie Policy</a
				>.
			</div>
			<div class="bottomcontainer lsmin">
				{#if !openpref}
					<div
						class="noborderbutton cursor-p"
						on:keydown
						on:click={() => {
							openpref = true;
						}}
					>
						Gestisci le preferenze
					</div>
				{:else}
					<div id="empty" />
				{/if}
				<div class="displayflex">
					<div
						class="closebutton cursor-p"
						class:lightbutton={theme == "light"}
						class:darkbutton={theme == "dark"}
						id="rifiuta"
						on:keydown
						on:click={() => {
							handleAllSelections(false);
						}}
					>
						Rifiuta tutti i cookies
					</div>
					<div
						class="closebutton cursor-p"
						style="margin-left: 1rem;"
						on:keydown
						on:click={() => {
							handleAllSelections(true);
							window.yett.unblock();
						}}
					>
						Accetta tutti i cookies
					</div>
				</div>
			</div>
			{#if openpref}
				<Cookiepreferences bind:openpref {agreed} {blocked} {theme} />
			{/if}
		</div>
	{/if}
</main>

<style>
	main {
		width: 100%;
		height: 100%;
		text-size-adjust: none;
	}

	.globprop {
		box-sizing: border-box;
		font-family: "Inter";
		font-size: 1rem;
		font-weight: 700;
		line-height: 130%;
		letter-spacing: 0em;
		text-align: left;
	}

	.bannercontainer {
		box-sizing: border-box;
		display: flex;
		flex-direction: column;
		position: fixed;
		padding: 1.5rem;
		max-height: 33.5rem;
		overflow: auto;
	}

	/* .fullbottombanner{
		width: 63.375rem;
		bottom: 0;		
		margin: 0 calc((100% - 64.375rem)/2);
	} */

	.body {
		margin-top: 0.5rem;
		font-weight: 500;
		font-size: 1rem;
	}

	.bottomcontainer {
		margin-top: 0.625rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.lsmin {
		letter-spacing: -0.01em;
	}

	a {
		color: #5265cc;
		text-decoration: underline;
	}

	.titleclose {
		display: flex;
		justify-content: space-between;
	}
</style>
