<script>
	let name ='max';
	let age = 30;

	$: uppercaseName = name.toUpperCase(); //labeled statement je to vanila JS nemusí být $ ale Svelte rozerná jen $
	// vytvoření dynamické proměnné nemusím jí nikde deklarovat Svelte pořeší ale můžu
	//vždy jak se změní name proměnná tak se "přepočte" uppercaseName

	$: console.log(name); // vypíše name vždy jak je změna proměnné name

	$: if (name === "Maximilian") {
		age = 33; // změna age nespustí znovu tento if statement protože reaguje pouze na změnu proměnné name
	}

	const incrementAge = () => {
		age++; // nepotřebuji this.setState() Svelte má interně odkaz na kontext
	}

	const changeName = () => name = "Maximilian"; // změním proměnnou name čímž spustím "přepočet" všech dynamických proměnných které používají name
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {uppercaseName}!, my age is {age}</h1> <!-- podobně jak react jen nemusím označit přes this.state.name-->
<button on:click="{incrementAge}">Change Age</button>
<button on:click="{changeName}">Change name</button>