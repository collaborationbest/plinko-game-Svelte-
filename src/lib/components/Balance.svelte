<script lang="ts">
  import { Connection, PublicKey } from '@solana/web3.js';
	import { walletStore } from '@svelte-on-solana/wallet-adapter-core';
	import {
		workSpace,
		WalletProvider,
		WalletMultiButton,
		ConnectionProvider
	} from '@svelte-on-solana/wallet-adapter-ui';
	import { clusterApiUrl } from '@solana/web3.js';
	import { PhantomWalletAdapter, SolflareWalletAdapter } from '@solana/wallet-adapter-wallets';

	const localStorageKey = 'walletAdapter';
	const network = clusterApiUrl('devnet'); // localhost or mainnet

	let wallets = [new PhantomWalletAdapter(), new SolflareWalletAdapter()];

  let balance = 0;

  $: {
    if ($walletStore?.connected) {
      const publicKey = $walletStore.publicKey;
      console.log(publicKey)
      const connection = new Connection(network, 'confirmed');

      connection.getBalance(publicKey).then((bal) => {
        balance = bal / 1e9; // Convert lamports to SOL
        console.log(`Current balance: ${balance} SOL`);
      }).catch((err) => {
        console.error('Error fetching balance:', err);
      });
    }
  }

</script>

<WalletProvider {localStorageKey} {wallets} autoConnect />
<ConnectionProvider {network} />
<WalletMultiButton />

{#if $walletStore?.connected}
<div>My balance is {balance}</div>
{/if}