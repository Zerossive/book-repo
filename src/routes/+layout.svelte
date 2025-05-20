<script lang="ts">
	import '../app.css'
	import { onNavigate } from '$app/navigation'

	let { children } = $props()

	onNavigate((navigation) => {
		if (!document.startViewTransition) return

		return new Promise((resolve) => {
			document.startViewTransition(async () => {
				resolve()
				await navigation.complete
			})
		})
	})
</script>

<header class="sticky top-0 flex items-center justify-center gap-3 bg-black px-12 py-6">
	<nav>
		<ul class="flex gap-6">
			<li><a href="/" class="hover:underline">Home</a></li>
			<li><a href="/about" class="hover:underline">About</a></li>
		</ul>
	</nav>
</header>

{@render children()}

<footer class="container mx-auto px-6">
	<p class="border-t py-6 text-center">Copyright © 2025—{new Date().getFullYear()}</p>
</footer>
