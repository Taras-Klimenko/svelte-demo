<script>
	import { onMount } from 'svelte';

	let todos = [];
	let todoText = '';

	onMount(() => {
		const existingTodos = localStorage.getItem('todos');
		todos = JSON.parse(existingTodos) || [];
	});

	function addTodo() {
		todos = [...todos, todoText];
		localStorage.setItem('todos', JSON.stringify(todos));
		todoText = '';
	}
</script>

<main>
	<div class="container">
		<h2>TODOS</h2>
		<ul>
			{#each todos as todo}
				<li>{todo}</li>
			{/each}
		</ul>
		<form on:submit|preventDefault={addTodo}>
			<input bind:value={todoText} />
			<input type="submit" value="Навалить туду" />
		</form>
	</div>
</main>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode',
			Geneva, Verdana, sans-serif;
		font-size: 30px;
		background: linear-gradient(to bottom, #f5f5f5, #dfdfdf);
		height: 100vh;
		width: 100%;
	}

	ul {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		list-style: none;
	}

	li {
		width: 50%;
		background-color: lightblue;
		margin: 10px 0;
		padding: 10px;
		border: solid 2px gray;
		border-radius: 10px;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
		font-size: 25px;
		text-align: center;
	}
</style>
