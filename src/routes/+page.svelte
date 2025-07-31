<script lang="ts">
	import Button from '$lib/components/Button/Button.svelte';
	import Otp from '$lib/components/OTP/otp.svelte';

	let isLoading = $state(false);
	let ticketIdLength = $state(3);

	$effect(() => {
		const elem = document.getElementById('ticket-id-input') as HTMLDivElement;
		elem.addEventListener('wheel', (e) => {
			ticketIdLength = e.deltaY < 0 ? 4 : 3;
		});
		return elem.removeEventListener('wheel', () => {});
	});

	const handleSubmit = () => {
		isLoading = true;
	};
</script>

<main
	class="grid size-full grid-cols-[1fr_2fr_1fr] justify-items-center bg-background p-5 [&>*]:col-start-2"
>
	<h1 class="text-4xl">Jira Progress Pulse</h1>
	<div id="ticket-id-input" class="relative flex h-fit flex-col gap-2">
		<Otp otpLength={ticketIdLength} />
		<Button loadingText="Submitting..." onclick={handleSubmit} {isLoading}>Submit</Button>
		<p class="absolute -bottom-16 left-1/2 w-max -translate-x-1/2">
			Scroll to Change No of Characters
		</p>
	</div>
</main>
