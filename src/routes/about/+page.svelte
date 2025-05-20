<script>
	import Title from '$lib/components/Title.svelte'
	import { fly, blur, fade, slide } from 'svelte/transition'
</script>

<Title title="about" />

<main class="container mx-auto p-6" in:fly={{ x: -100, y: 50 }}>
	<p>This is the about page.</p>
</main>
