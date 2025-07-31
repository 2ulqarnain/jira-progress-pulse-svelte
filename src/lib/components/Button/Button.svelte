<script lang="ts">
	import { cn } from '$lib/utils';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import Loading from '../icons/Loading.svelte';
	import { cva, type VariantProps } from 'class-variance-authority';

	export const buttonVariants = cva(
		'disabled:bg-muted-background disabled:text-muted-foreground disabled:border-muted-foreground disabled:pointer-events-none hover:-translate-1 hover:shadow-[6px_6px_0px_#888] transition-[box-shadow,translate]',
		{
			variants: {
				variant: {
					default: 'rounded-xl p-2 px-3 bg-primary text-zinc-200 border border-primary-light',
					secondary: 'bg-secondary bg-secondary-foreground'
				},
				size: {}
			},
			default: {
				variant: '',
				size: ''
			}
		}
	);

	type ButtonProps = HTMLButtonAttributes &
		VariantProps<typeof buttonVariants> & {
			isLoading?: boolean;
			loadingText?: string;
		};
	const {
		isLoading = false,
		class: className,
		children,
		variant = 'default',
		size,
		loadingText,
		...buttonProps
	}: ButtonProps = $props();
</script>

{#if isLoading}
	<button
		{...buttonProps}
		disabled
		class={cn('flex items-center justify-center', buttonVariants({ variant, size, className }))}
		>{loadingText ?? 'Loading...'}<Loading class="size-7" /></button
	>
{:else}
	<button {...buttonProps} class={cn(buttonVariants({ variant, size, className }))}
		>{@render children()}</button
	>
{/if}
