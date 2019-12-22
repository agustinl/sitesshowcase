<!--<script context="module">

	let sites;
	let pages;
	let error;

	export async function preload() {

		const res = await this.fetch('API_URL?page=1');
		var data = await res.json();
		
		if(res.ok) {
			return { sites: data.sites, pages: data.pages, error: ''};
		} else {
			return { error: data.msg }
		}

	}

</script>-->

<script>
	import { onMount } from 'svelte';
	import fetch from 'node-fetch';
	import Hero from '../components/Hero.svelte';
	import Siteslist from '../components/Siteslist.svelte';
	import Footer from '../components/Footer.svelte';

	let page = 1;
	let firstrender = false;
	let sites;
	let pages;
	let error;

	async function hashchange() {

		const path = window.location.hash.slice(1);

		if (path.startsWith('/page')) {
			page = +path.slice(6);
			firstrender = true;
		}

	}
		
	$: if (page > 0 && firstrender == true) {
		fetch(`API_URL?page=${page}`)
		.then(r => r.json())
		.then(data => {
			sites = data.sites;
			pages = data.pages;
		});
	}

	onMount(async () => {

		const path = window.location.hash.slice(1);

		if (path.startsWith('/page')) {
			page = +path.slice(6);
		}

		const res = await fetch(`API_URL?page=${page}`);
		const data = await res.json();
		if(res.ok) {
			sites = data.sites;
			pages = data.pages;
			error = '';
		} else {
			error = data.msg
		}
	});
	
</script>

<svelte:head>
	<title>Sites showcase | A community list of personal sites for inspiration</title>
</svelte:head>

<Hero />

<svelte:window on:hashchange={hashchange}/>

<Siteslist {page} {sites} {pages} {error} />

<Footer />