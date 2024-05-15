<script>
	import '../app.css';
</script>

<div class="h-dvh bg-neutral-800">
	<header class=""></header>
	<div class="flex gap-4 p-4 w-full h-full">
		<main class="max-w-[1000px] m-auto w-full text-red-500">
			<slot />
		</main>
	</div>
	<footer class=""></footer>
</div>
