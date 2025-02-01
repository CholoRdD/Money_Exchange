<script lang="ts">
    import CurrencyList from './CurrencyList.svelte';
	import Header from './Header.svelte';
	import Output from './Output.svelte';

	let apiKey = 'cfa119cbaabf69fb4a42fdc1';
	let api = `https://v6.exchangerate-api.com/v6/${apiKey}/latest/`;


    let {name}:{
    	    name: string;
    } = $props();


    let input = $state({
        value:``, //valueInput
		from: ``, //fromConvert
		to: ``, //toConvert
    });

	let show = $state({
input: "",

	})

</script>

<script>
	// import CurrencyList from './CurrencyList.svelte';
	// import Header from './Header.svelte';
	// import Output from './Output.svelte';

	// let apiKey = 'cfa119cbaabf69fb4a42fdc1';
	// let api = `https://v6.exchangerate-api.com/v6/${apiKey}/latest/`;

//	let valueInput;
	let showInput;
//	let fromConvert = ``;
//	let toConvert = ``;
	let showFrom = ``;
	let showTo = ``;
	let exchangeOut = 0;
	let outputStatus = false;

	async function Convert() {
		if (isFinite(valueInput) && valueInput > 0 && fromConvert && toConvert) {
			try {
				const response = await fetch(`${api}${fromConvert}`);
				const data = await response.json();
				if (data.conversion_rates) {
					let fromExchange = data.conversion_rates[fromConvert];
					let toExchange = data.conversion_rates[toConvert];
					exchangeOut = (valueInput / fromExchange) * toExchange;
					outputStatus = true;
					showFrom = fromConvert;
					showTo = toConvert;
					showInput = valueInput;
				}
			} catch (error) {
				alert('Error fetching exchange rates:', error);
			}
		} else {
			alert('Invalid input or currency selection.');
		}
	}
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>
