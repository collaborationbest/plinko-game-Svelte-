<script lang="ts">
  // import { Connection, PublicKey } from '@solana/web3.js';
	// import { walletStore } from '@svelte-on-solana/wallet-adapter-core';
	// import {
	// 	workSpace,
	// 	WalletProvider,
	// 	WalletMultiButton,
	// 	ConnectionProvider
	// } from '@svelte-on-solana/wallet-adapter-ui';
	// import { clusterApiUrl } from '@solana/web3.js';
	// import { PhantomWalletAdapter, SolflareWalletAdapter } from '@solana/wallet-adapter-wallets';
  // import {
  //   balance,
  // } from '$lib/stores/game';

	// const localStorageKey = 'walletAdapter';
	// const network = clusterApiUrl('devnet'); // localhost or mainnet

	// let wallets = [new PhantomWalletAdapter(), new SolflareWalletAdapter()];
import { createAppKit } from '@reown/appkit'
import { SolanaAdapter } from '@reown/appkit-adapter-solana'
import { solana, solanaTestnet, solanaDevnet } from '@reown/appkit/networks'
import { PhantomWalletAdapter, SolflareWalletAdapter } from '@solana/wallet-adapter-wallets'

const solanaWeb3JsAdapter = new SolanaAdapter({
  wallets: [new PhantomWalletAdapter(), new SolflareWalletAdapter()]
})

// 1. Get projectId from https://cloud.reown.com
const projectId = 'YOUR_PROJECT_ID'

// 2. Create a metadata object - optional
const metadata = {
  name: 'AppKit',
  description: 'AppKit Solana Example',
  url: 'https://example.com', // origin must match your domain & subdomain
  icons: ['https://avatars.githubusercontent.com/u/179229932']
}

// 3. Create modal
createAppKit({
  adapters: [solanaWeb3JsAdapter],
  networks: [solana, solanaTestnet, solanaDevnet],
  metadata: metadata,
  projectId,
  features: {
    analytics: true // Optional - defaults to your Cloud configuration
  }
})
  // $: {
  //   if ($walletStore?.connected) {
  //     const publicKey = $walletStore.publicKey;
  //     console.log(publicKey)
  //     const connection = new Connection(network, 'confirmed');

  //     connection.getBalance(publicKey).then((bal) => {
  //       $balance = bal / 1e9; // Convert lamports to SOL
  //       console.log(`Current balance: ${$balance} SOL`);
  //     }).catch((err) => {
  //       console.error('Error fetching balance:', err);
  //     });
  //   }
  // }

</script>

<appkit-button></appkit-button>

<!-- {#if $walletStore?.connected}
<div>My balance is {$balance}</div>
{/if} -->