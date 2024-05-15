<script lang="ts">
	import dayjs from 'dayjs';
	import utc from 'dayjs/plugin/utc';
	import timezone from 'dayjs/plugin/timezone';

	dayjs.extend(utc);
	dayjs.extend(timezone);

	let cdDays: string = '';
	let cdHours: string = '';
	let cdMins: string = '';
	let cdSecs: string = '';

	function isPokerNight(date: Date) {
		return (
			date.getDay() === 4 && ((date.getDate() > 7 && date.getDate() < 15) || date.getDate() > 28)
		);
	}

	function pokerNightCountdown() {
		const dateDays = [5, 6, 0, 1, 2, 3, 4];
		const now = new Date();
		const today = now.getDate();

		const potentialDate =
			today === 4 ? now : new Date(now.getTime() + (6 - dateDays.indexOf(now.getDate())) * 8.64e7);

		function checkEligibleDates(date: Date) {
			if (isPokerNight(date)) {
				return date;
			}
			date.setTime(date.getTime() + 8.64e7);
			return checkEligibleDates(date);
		}

		const pokerNight = checkEligibleDates(potentialDate);

		const months = [
			'Jan',
			'Feb',
			'Mar',
			'Apr',
			'May',
			'Jun',
			'Jul',
			'Aug',
			'Sep',
			'Oct',
			'Nov',
			'Dec'
		];

		const pokerNightFormatted = new Date(
			`Fri ${months[pokerNight.getMonth()]} ${pokerNight.getDate()} ${pokerNight.getFullYear()} 20:00:00`
		);

		const pokerNightTimestamp = dayjs(pokerNightFormatted).tz('America/New_York', true).valueOf();

		let remaining = pokerNightTimestamp - Date.now();

		cdDays = String(Math.floor(remaining / 86400000)).padStart(2, '0'); // days
		cdHours = String(Math.floor((remaining %= 86400000) / 3600000)).padStart(2, '0'); // hours
		cdMins = String(Math.floor((remaining %= 3600000) / 60000)).padStart(2, '0'); // minutes
		cdSecs = String(Math.floor((remaining % 60000) / 1000)).padStart(2, '0'); // seconds
	}

	setInterval(pokerNightCountdown, 1000);
	pokerNightCountdown();
</script>

{#if cdDays}
	<h1 class="text-5xl text-cyan-600 text-center mb-4">Gumball Club</h1>
	<h1 class="text-3xl text-cyan-600 text-center">
		{cdDays} : {cdHours} : {cdMins} : {cdSecs}
	</h1>
{/if}
