<script lang="ts">
	let {
		title = 'book 1: book of bookening',
		authors = ['author 1', 'author 2'],
		series = ['book series', 1],
		description = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magnam aliquam quaerat voluptatem.',
		image = 'https://picsum.photos/400/600',
		tags = ['tag 1', 'tag 2', 'tag 3'],
		datePublished = new Date(),
		rating = 5
	}: {
		title: string
		authors: string[]
		series: [string, number]
		description: string
		image?: string
		tags?: string[]
		datePublished?: Date
		rating?: 0 | 1 | 2 | 3 | 4 | 5
	} = $props()
</script>

<div class="flex w-[30ch] grow flex-col gap-6 rounded-2xl bg-white p-6 text-black lg:w-[40ch]">
	<div class="flex items-stretch gap-6">
		{#if image}
			<img
				src={image}
				alt="book cover"
				class="top-0 right-0 h-24 max-w-1/4 rounded-md object-cover"
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

	{#if tags}
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
