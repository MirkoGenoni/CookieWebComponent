<svelte:options tag={"cookie-banner"} />

<script>
	import Cookiepolicy from "./cookiepolicy.svelte";
	import Cookiepreferences from "./cookiepreferences.svelte";
	import { onMount } from "svelte";
	export let theme = "light";
	let openpolicy = false;
	let openpref = false;
	let rootElement;

	onMount(async () => {
		await loadStyle(rootElement, `global.css`);
	});

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
</svelte:head>

<main bind:this={rootElement}>
	{#if openpolicy == true}
		<Cookiepolicy bind:openpolicy />
	{:else}
		<div id="container">
			<div
				id="bannerContainer"
				class="globprop"
				class:darkbcontainer={theme == "dark"}
				class:lightbcontainer={theme == "light"}
			>
				<div class="fs24" class:darktitle={theme == "dark"}>
					Noi teniamo alla tua Privacy
				</div>
				<div id="body" class="fs16">
					Facendo clic su "Accetta tutti i cookie", accetti la
					memorizzazione dei cookie sul tuo dispositivo per migliorare
					la navigazione del sito, analizzare l'utilizzo del sito e
					assistere nelle nostre attività di marketing, come
					specificato nella <a
						class="cursorp"
						on:click|preventDefault={openPolicy}
						href={undefined}>Cookie Policy</a
					>.
				</div>
				<div id="bottomcontainer" class="lsmin">
					{#if !openpref}
						<div
							class="button underline cursorp"
							on:keydown
							on:click={() => {
								openpref = true;
							}}
						>
							Gestisci le preferenze
						</div>
					{:else}
						<div id="empty"></div>
					{/if}
					<div id="buttoncontainer">
						<div
							class="button cursorp"
							class:rifiutal={theme == "light"}
							class:rifiutad={theme == "dark"}
							id="rifiuta"
						>
							Rifiuta tutti i cookies
						</div>
						<div class="button cursorp" id="accetta">
							Accetta tutti i cookies
						</div>
					</div>
				</div>
				{#if openpref}
					<Cookiepreferences bind:openpref={openpref}/>
				{/if}
			</div>
		</div>
	{/if}
</main>

<style>
	main {
		width: 100%;
		height: 100%;
	}
	#container {
		width: 100%;
		height: 11.7rem;
		display: flex;
		justify-content: center;
		position: fixed;
		bottom: 0;
		left: 0;
	}
	.globprop {
		box-sizing: border-box;
		font-family: "Inter";
		font-size: 16px;
		font-weight: 700;
		line-height: 130%;
		letter-spacing: 0em;
		text-align: left;
	}
	#bannerContainer {
		box-sizing: border-box;
		display: flex;
		position: fixed;
		width: 63rem;
		bottom: 0;
		flex-direction: column;
		font-style: normal;
		font-weight: 700;
		padding: 1.5rem;
	}
	.darkbcontainer {
		background-color: #1a182d;
		color: #ffffff;
	}
	.lightbcontainer {
		background-color: #b9c4ff;
		color: #2d3648;
	}
	.darktitle {
		color: #e1f4ff;
	}
	.fs16 {
		font-size: 16px;
	}
	.fs24 {
		font-size: 24px;
	}
	#body {
		margin-top: 0.5rem;
		font-weight: 500;
	}
	#bottomcontainer {
		margin-top: 0.625rem;
		height: 100%;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
	}
	.rifiutal {
		border: 2px solid #2d3648;
	}
	.rifiutad {
		border: 2px solid #ffffff;
	}
	#accetta {
		margin-left: 1rem;
		background-color: #2d3648;
		color: #ffffff;
	}
	#buttoncontainer {
		display: flex;
		flex-direction: row;
	}
	.underline {
		text-decoration-line: underline;
		font-feature-settings: "calt" off;
	}
	.button {
		box-sizing: border-box;
		padding: 0.75rem 1.25rem;
		border-radius: 6px;
	}
	.lsmin {
		letter-spacing: -0.01em;
	}
	a {
		color: rgb(0, 100, 200);
		text-decoration: underline;
	}
	.cursorp {
		cursor: pointer;
	}
</style>
