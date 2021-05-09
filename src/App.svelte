<script>
	import ContactCard from './ContactCard.svelte';

	let name ='max';
	let age = 30;
	let jobTitle = "";
	let description = "";
	let imageUrl = "";

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

	const nameInput = (event) => {
		const enteredValue = event.target.value;
		name = enteredValue;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {uppercaseName}!, my age is {age}</h1> <!-- podobně jak react jen nemusím označit přes this.state.name-->
<button on:click="{incrementAge}">Change Age</button>
<!-- <button on:click="{changeName}">Change name</button> -->
<!-- <input type="text" value="{name}" on:input="{nameInput}" /> když nastavím pouze value jedná se o oneWay databinding podbně jak Angular -->
<!--on:input zajistí twoWay databinding skrze klasicky event-->
<input type="text" bind:value="{name}" />
<input type="text" bind:value="{jobTitle}" />
<input type="text" bind:value="{imageUrl}" />

<textarea name="description" id="desc" bind:value="{description}" cols="30" rows="10"></textarea>
<!--to samé jako předchozí příklad avšak nepotřebuji vytvářen novou metudo a starat se o event. Svelte vše pořeší sám -->
<ContactCard 
userName="{name}" 
jobTitle="{jobTitle}" 
description="{description}" 
imageUrl="{imageUrl}" /> <!--další komponenta-->
<!--můžu zkrátit jen na {description} {jobTitle}-->