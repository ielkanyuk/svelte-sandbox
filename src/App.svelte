<script>
	export let name;
	let inputValue = "";
	let counter = 0;
	$: counterClass = counter % 2 === 0 ? 'red': 'blue';
	const htmlString = '<b>This is strong text</b> with <em>italic text</em>';
	let pos = {
	  x: 0,
	  y: 0,
	}

	$: upperName = name.toUpperCase();

	$: {
	  console.log('Name: ', name);
	  console.log('Counter: ', counter);
	}

	function changeGreetingHandler() {
	  name = "Svelte";
	}

	function mousemoveHandler(event) {
	  pos.x = event.x;
	  pos.y = event.y;
	}

	function submitHandler() {
	  console.log(inputValue);
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<h2>...and UPPER {upperName}!</h2>
	<p>{@html htmlString}</p>
	<button on:click={changeGreetingHandler}>Change greeting text</button>

	<h3 class={counterClass}>Counter {counter}</h3>
	<button on:click={() => counter++}>Add 1 to counter</button>

	<div class="playground" on:mousemove={mousemoveHandler}>
	  <h2>Pos X: {pos.x}, pos Y: {pos.y}</h2>
  </div>

  <form on:submit|preventDefault={submitHandler}>
  <input type="text" on:input={event => (inputValue = event.target.value)} />
  <button type="submit">Submit form</button>
</form>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	.playground {
    width: 400px;
    height: 400px;
    padding: 1rem;
    margin-bottom: 1rem;
    border: 1px solid black;
	}

	.blue {
	  color: blue;
	}

	.red {
  	  color: red;
  	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
