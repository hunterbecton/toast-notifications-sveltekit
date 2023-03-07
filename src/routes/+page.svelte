<script>
	import { addToast } from '../lib/store/toasts';
</script>

<button type="button" on:click={() => addToast('Hello!', 'This is so much fun.', 'error')}
	>Add Toast</button
>
