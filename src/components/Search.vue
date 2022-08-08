<template>
	<div>
		<input v-on:keyup.enter="search" class="search" type="text" name="search" placeholder="Search gif...">
		<button class="searchBtn" v-on:click="search">Search</button>
	</div>
</template>

<script>
	export default {
		name: 'search',
		props: [
			'search',
		]
	}
</script>

<style scoped>
	.search {
		outline: none;
		margin-top: 5px;
		margin-bottom: 15px;
		margin-left: 25% !important;
		width: 40%;
		padding: 10px;
		border: 2px solid #c7c7c7;
		border-radius: 5px;
		font-family:monospace, sans-serif; 
		font-weight: 700;
		font-size: 18px;
		background-color: #e7e7e7;
		color:#000;
	}
	.search::-webkit-input-placeholder {
		color:#ccc;
	}
	.search:focus {
		background-color: #e7e7e7;
	}
	.search:focus::-webkit-input-placeholder {
		color:#ccc;
	}
	.searchBtn {
		outline: none;
		padding: 10px;
		border: 2px solid #c7c7c7;
		border-radius: 5px;
		font-weight: 700;
		font-size: 18px;
	}
</style>