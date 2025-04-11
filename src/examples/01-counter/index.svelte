<script lang="ts">
	let count = $state(0);
</script>
<div class="flex-gap">
	<input type="text" bind:value={count}>
	<button onclick={()=>{count++}}>Count</button></div>