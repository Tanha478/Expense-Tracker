<script>
	import '../app.css';
	import Navbar from './navbar.svelte';
	import Footer from './footer.svelte'

	let { children } = $props();
</script>

<Navbar />
{@render children()}
<Footer />