<script>
	import { fade } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	import { toasts, removeToast } from '../../store/toasts';
	import Cancel from '../icon/Cancel.svelte';
	import ToastIcon from './ToastIcon.svelte';
	import ToastProgress from './ToastProgress.svelte';
</script>

{#if $toasts}
	<div class="z-30 w-full max-w-xs absolute top-8 right-8 flex flex-col-reverse gap-4">
		{#each $toasts as { id, title, message, type } (id)}
			<div
				in:fade
				animate:flip={{ duration: 300 }}
				role="alert"
				class="relative bg-white rounded-md shadow-lg overflow-hidden"
			>
				<div class=" p-6">
					<div class="flex items-center">
						<ToastIcon toastType={type} />
						<div class="ml-3 pl-3 border-l border-neutral-200">
							<p class="text-sm font-semibold text-neutral-900">{title}</p>
							<p class="text-sm font-normal text-neutral-700">{message}</p>
						</div>
					</div>
					<button
						on:click={() => removeToast(id)}
						class="absolute top-2 right-2 p-1 rounded-full bg-white hover:bg-neutral-100 focus-visible:bg-neutral-100 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-neutral-900"
						><Cancel class="text-neutral-900" /><span class="sr-only">Remove notification</span
						></button
					>
				</div>
				<ToastProgress toastType={type} />
			</div>
		{/each}
	</div>
{/if}
