<script lang="ts">
	let date: Date;

	function onDateChange(event: Event) {
		const target = event.target as HTMLInputElement;
		if (target.value) {
			date = new Date(target.value);
		}
	}

	function isPokerNight(date: Date) {
		return (
			date.getDay() === 4 && ((date.getDate() > 7 && date.getDate() < 15) || date.getDate() > 28)
		);
	}

	function nextPokerNight() {
		return 'soon';
	}
</script>

<h1 class="text-red-500">Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<div class="text-center">
	<h2>Countdown until next poker night: <span>{nextPokerNight()}</span></h2>
	<input type="date" class="bg-neutral-900 placeholder-cyan-500" on:change={onDateChange} />
	<span>date is: {date ? (isPokerNight(date) ? 'POKER NIGHT' : 'lame') : 'select date'}</span>
</div>
