<script lang="ts">
	import { fade } from 'svelte/transition'

	let { title } = $props()
</script>

<div
	class="flex h-auto w-full items-end overflow-clip bg-[url(https://picsum.photos/id/329/1920/1080/?blur)] bg-cover bg-fixed bg-center"
>
	<div class="container mx-auto space-y-3 p-6">
		<h1
			class="text-center text-3xl font-bold uppercase text-shadow-md first-letter:text-4xl md:text-4xl md:first-letter:text-5xl"
		>
			{title}
		</h1>
	</div>
</div>
