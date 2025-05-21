<script lang="ts">
	import { fly, slide } from 'svelte/transition'

	const randomDate = () => {
		const start = new Date(2020, 0, 1)
		const end = new Date()
		return new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()))
	}
	const randomRating = () => Math.floor(Math.random() * 6) as 0 | 1 | 2 | 3 | 4 | 5
	const randomTags = () => {
		const tags: string[] = []
		const length = Math.floor(Math.random() * 6)
		for (let i = 0; i < length; i++) {
			tags.push(`tag ${i + 1}`)
		}
		return tags
	}
	const randomImage = () =>
		`https://picsum.photos/id/${Math.floor(Math.random() * 60) + 30}/40/60`
	const randomSeries = () => {
		let series: [string, number] | null = null
		if (Math.random() > 0.5) {
			series = ['book series', Math.floor(Math.random() * 10) + 1]
		}
		return series
	}
	const randomAuthor = () => {
		let authors = []
		for (let i = 1; i <= Math.floor(Math.random() * 3) + 1; i++) {
			authors.push(`author ${i}`)
		}
		return authors
	}

	let {
		title = 'book: book of bookening',
		authors = randomAuthor(),
		series = randomSeries(),
		description = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magnam aliquam quaerat voluptatem.',
		image = randomImage(),
		tags = randomTags(),
		datePublished = randomDate(),
		rating = randomRating()
	}: {
		title?: string
		authors?: string[]
		series?: [string, number] | null
		description?: string
		image?: string
		tags?: string[]
		datePublished?: Date
		rating?: 0 | 1 | 2 | 3 | 4 | 5
	} = $props()

	let imageLoaded = $state(false)
	let imageError = $state(false)
</script>

<div
	class="flex w-full grow flex-col justify-between gap-6 rounded-2xl bg-white p-6 text-black md:w-[30ch] lg:w-[40ch]"
>
	<div class="flex items-stretch gap-6">
		{#if image}
			<img
				src={image}
				alt={image}
				class="hidden h-24 w-auto max-w-1/4 origin-left rounded-md object-cover duration-150"
				class:opacity-0={!imageLoaded}
				class:scale-x-0={!imageLoaded}
				class:block={imageLoaded}
				class:hidden={imageError}
				onload={() => (imageLoaded = true)}
				onerror={() => (imageError = true)}
				loading="lazy"
			/>
		{/if}
		<div class="flex grow flex-col justify-evenly tracking-widest capitalize">
			<span class="text-lg font-bold">{title}</span>
			{#if series}
				<span class="italic">{series[0]} #{series[1]}</span>
			{/if}
			<span><span class="lowercase">by</span> {authors.join(', ')}</span>
		</div>
	</div>

	<div>
		<label class="italics capitalize underline">description:</label>
		<p>{description}</p>
	</div>

	{#if tags.length}
		<div>
			<label class="italics capitalize underline">tags:</label>
			<ul class="flex flex-wrap gap-2 pt-2">
				{#each tags as tag, index}
					<li
						class="rounded bg-gray-200 px-2 py-1 text-sm font-bold text-gray-800 capitalize"
					>
						{tag}
					</li>
				{/each}
			</ul>
		</div>
	{/if}

	{#if rating}
		<div>
			<label class="italics capitalize underline">rating:</label>
			<span class="">{rating}/10</span>
			<progress max={10} value={rating} class="mt-2 h-3 w-full rounded">{rating}</progress>
		</div>
	{/if}

	{#if datePublished}
		<p class="capitalize">
			<label class="underline">published:</label>
			<span class="">
				{datePublished.toLocaleDateString()}
			</span>
		</p>
	{/if}

	<button
		class="cursor-pointer rounded-md bg-black px-4 py-2 text-white capitalize hover:bg-gray-950 active:bg-gray-900"
		>learn more</button
	>
</div>
