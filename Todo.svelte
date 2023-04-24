<!-- Js goes here -->
<script>
	let todos = [{done:false, text: 'Clean the house',},{done:false, text: 'Clean the house'}];
	const add = () => {todos = todos.concat({done:false, text:''})}
	const clear = () => {todos = todos.filter(t => !t.done)}
	$:remaining = todos.filter(t => !t.done).length;
	$:done = todos.filter(t => t.done).length;
	$: total = todos.length;
	let saved = localStorage.setItem('todo', todos);
	let getTodo = localStorage.getItem('todo');
	console.log(getTodo);
</script>

<!-- Markup goes here -->
<body>
	<p>Simple Todo App SVELTE</p>
{#each todos as todo}
<div class:done={todo.done}>
	<input type="checkbox" bind:checked={todo.done}/>
	<input type="text" bind:value={todo.text}>
</div>
{/each}
	<div>
	{remaining}/{total} remaining
	</div>
	<br>
	<div>
	{done}/{total} done
	</div>
	<p>{getTodo} todo</p>
	<br>
	<button on:click={add}>Add</button>
	<button on:click={clear}>Clear done</button>
</body>
<style>	
	.done{opacity:0.4;}
	input[type='checkbox'] {
    	width:20px;
		height:20px;
		background:white;
		border-radius:5px;
		border:2px solid #555;
	}
	button{
		padding:2rem; 
		width:10rem;
	}
	button:hover{
		transform:scale(1.1)
	}
	input[type="text"]{
			font-size:20px;
			outline:none;
			border:none;
			backdrop-filter: blur(16px) saturate(180%);
			-webkit-backdrop-filter: blur(16px) saturate(180%);
			background-color: rgba(17, 25, 40, 0.75);
			border-radius: 12px;
			border: 1px solid rgba(255, 255, 255, 0.125);
			color:white;
			padding:1.2rem;
	}

input[type='checkbox']:checked {background: #abd;}
</style>
