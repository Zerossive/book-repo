<script lang="ts">
	import Book from '$lib/components/Book.svelte'
	import { flip } from 'svelte/animate'
	import { circInOut } from 'svelte/easing'
	import { crossfade, blur, fade, fly, slide, scale } from 'svelte/transition'

	type viewType = 'all' | 'new' | 'top'
	let view: viewType = $state('all')
	let views: viewType[] = ['all', 'new', 'top']
</script>

<div
	class="flex h-86 w-full items-end overflow-clip bg-[url(https://picsum.photos/id/329/1920/1080/?blur)] bg-cover bg-fixed bg-center"
>
	<div class="container mx-auto space-y-3 px-6 py-16">
		<h1
			class="text-4xl font-bold text-black uppercase text-shadow-white/50 text-shadow-xs md:text-5xl"
		>
			<span class="text-5xl md:text-6xl">b</span>ook
			<span class="text-5xl md:text-6xl">r</span>epository
		</h1>
		<p class="max-w-[60ch] text-shadow-md">
			A repository of made up books for the purpose of learning Svelte.
		</p>
	</div>
</div>

<main class="container mx-auto p-6" in:fly={{ x: -100, y: 50 }}>
	<div class="mb-6 flex flex-wrap gap-3 border-b">
		{#each views as item, i (i)}
			<button
				class={[
					'cursor-pointer border-b-2 border-transparent px-4 py-2 capitalize duration-75',
					view === item && 'border-white'
				]}
				onclick={() => (view = item)}>{item}</button
			>
		{/each}
	</div>

	{#if view === 'all'}
		{@render bookList()}
	{:else if view === 'new'}
		{@render bookList()}
	{:else if view === 'top'}
		{@render bookList()}
	{/if}
</main>

{#snippet bookList()}
	<div class="flex flex-wrap gap-3 pb-9 text-black">
		<label class="flex w-full flex-col gap-2">
			<span class="text-white capitalize underline">search:</span>
			<input type="text" class="w-full rounded-md bg-white px-4 py-2" placeholder="Search" />
		</label>
		<!-- tags -->
		<label class="flex w-[20ch] grow flex-col gap-2">
			<span class="text-white capitalize underline">tags:</span>
			<select class="w-full rounded-md bg-white px-4 py-2 capitalize">
				<option value="tag 1">Tag 1</option>
				<option value="tag 2">Tag 2</option>
				<option value="tag 3">Tag 3</option>
			</select>
		</label>
		<!-- rating -->
		<label class="flex w-[20ch] grow flex-col gap-2">
			<span class="text-white capitalize underline">rating:</span>
			<select class="w-full rounded-md bg-white px-4 py-2 capitalize">
				<option value="all">All</option>
				<option value="5">5 stars</option>
				<option value="4">4 stars</option>
				<option value="3">3 stars</option>
				<option value="2">2 stars</option>
				<option value="1">1 star</option>
			</select>
		</label>
		<!-- sort -->
		<label class="flex w-[20ch] grow flex-col gap-2">
			<span class="text-white capitalize underline">sort:</span>
			<select class="w-full rounded-md bg-white px-4 py-2 capitalize">
				<option value="all">Default</option>
				<option value="newest">Newest</option>
				<option value="oldest">Oldest</option>
				<option value="highest">Highest</option>
				<option value="lowest">Lowest</option>
			</select>
		</label>
	</div>
	<section class="flex flex-wrap gap-6" in:blur={{ delay: 150 }} out:blur={{ duration: 150 }}>
		{#each { length: 20 } as _, i (i)}
			<div animate:flip class="flex grow">
				<Book />
			</div>
		{/each}
	</section>
{/snippet}
