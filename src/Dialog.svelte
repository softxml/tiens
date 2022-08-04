<script>
	let isOpen = true;
	let name = '';
	let email = '';
	
	export function openModal() {
		isOpen = true;
	}
	
	export function reset() {
		name = '';
		email = '';
	}
	
	export function closeModal() {
		isOpen = false;
		reset();
	}
</script>

{#if isOpen}
	<div class="dialog">
		<span class="close" on:click={closeModal}>x</span>
		<label>
			Name
			<input bind:value={name} />
		</label>
		<label>
			Email
			<input type="email" bind:value={email} />
		</label>		
	</div>
{/if}

<style>
	.dialog {
		padding: 16px;
		border: 1px solid black;
		border-radius: 4px;
		position: relative;
		margin: 8px;
	}
	.close {
		position: absolute;
		right: 8px;
		top: 8px;
		cursor: pointer;
	}
</style>