<script>
	import '../app.css';
</script>

<header>The Gumball Club</header>
<div class="flex gap-4 p-4 w-full">
	<main class="max-w-[1000px] bg-neutral-800 m-auto w-full text-red-500">
		<slot />
	</main>
</div>
<footer>footer</footer>
