<script>
	import { page } from '$app/stores';
	import ImageObserver from '@/components/Image/ImageObserver.svelte';

	// Generate random number to stop the images caching
	/**
	 * @param {number} min
	 * @param {number} max
	 */
	function rand(min, max) {
		let randomNum = Math.random() * (max - min) + min;
		return Math.round(randomNum);
	}

	let n = 0;
	if ($page.data.len) {
		n = +$page.data.len;
	}
	const imgNumbers = Array.from({ length: n }, (_, i) => i + 1);
</script>

<svelte:head>
	<title>Image</title>
	<meta name="description" content="Lazyload Image" />
</svelte:head>

<h2>Image loading demo</h2>

<p>Scroll to see images fade-in</p>

<ul>
	{#each imgNumbers as i}
		<li>
			<ImageObserver
				src={`https://picsum.photos/seed/${i}/800/800`}
				srcBlur={`https://picsum.photos/seed/${i}/10/10`}
				alt="Example image"
				loading="lazy"
			/>
		</li>
	{/each}
</ul>

<style>
	li {
		list-style: none;
		background: #eee;
		width: 200px;
		height: 200px;
		margin: 2em;
	}
</style>
