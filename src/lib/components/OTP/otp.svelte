<script lang="ts">
	import type { ChangeEventHandler, KeyboardEventHandler } from 'svelte/elements';

	const { otpLength = 4 } = $props();
	const handleChange: ChangeEventHandler<HTMLInputElement> = (e) => {
		if (!e.currentTarget.value) {
			const previousSibling = e.currentTarget.previousElementSibling as HTMLInputElement | null;
			previousSibling?.focus();
		} else {
			const nextSibling = e.currentTarget.nextElementSibling as HTMLInputElement | null;
			nextSibling?.focus();
		}
	};
	const handleKeyDown: KeyboardEventHandler<HTMLInputElement> = (e) => {
		const previousSibling = e.currentTarget.previousElementSibling as HTMLInputElement | null;
		const nextSibling = e.currentTarget.nextElementSibling as HTMLInputElement | null;
		if (e.key === 'ArrowLeft') {
			e.preventDefault();
			previousSibling?.focus();
		} else if (e.key === 'ArrowRight') {
			e.preventDefault();
			nextSibling?.focus();
		} else if (e.key === 'Backspace') {
			if (!e.currentTarget.value) {
				e.preventDefault();
				previousSibling?.focus();
			}
		}
	};
</script>

<form class="flex gap-2">
	{#each Array(otpLength).fill(null) as _}
		<input
			type="text"
			maxlength="1"
			class="size-12 rounded-lg border border-border bg-card text-center text-secondary-foreground valid:bg-secondary focus:outline focus:outline-primary"
			required
			oninput={handleChange}
			onkeydown={handleKeyDown}
		/>
	{/each}
</form>
