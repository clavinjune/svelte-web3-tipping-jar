<script type="text/typescript">
	import { onMount } from 'svelte';
	import { defaultEvmStores, web3, selectedAccount } from 'svelte-web3';

	let tip = 0.000001;

	onMount(() => {
		defaultEvmStores.setProvider();
	});

	const handleClick = (e) => {
		e.preventDefault();

		$web3.eth.sendTransaction(
			{
				to: $selectedAccount, // should be changed to owner
				from: $selectedAccount,
				value: $web3.utils.toWei(`${tip}`, 'ether')
			},
			(err, trx) => {
				if (err) return alert(`Oh no! ${err.message}`);
				alert(`${trx}`);
			}
		);
	};
</script>

<input type="text" placeholder="Tip" bind:value={tip} />
<div class="tip-button" on:click={handleClick} />

<style type="text/scss">
	.tip-button {
		width: 304px;
		height: 89px;
		background-size: 100%;
		background-image: url('https://raw.githubusercontent.com/MetaMask/TipButton/master/images/1_pay_mm_off.png');
		cursor: pointer;
	}

	.tip-button:hover {
		background-image: url('https://raw.githubusercontent.com/MetaMask/TipButton/master/images/1_pay_mm_over.png');
	}

	.tip-button:active {
		background-image: url('https://raw.githubusercontent.com/MetaMask/TipButton/master/images/1_pay_mm_off.png');
	}
</style>
