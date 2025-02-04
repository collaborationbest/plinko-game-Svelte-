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
import { mainnet, arbitrum } from '@reown/appkit/networks'
import { WagmiAdapter } from '@reown/appkit-adapter-wagmi'

// 1. Get a project ID at https://cloud.reown.com
const projectId = '553f000f274814b119da5df8651e7ecd'

export const networks = [mainnet, arbitrum]

// 2. Set up Wagmi adapter
const wagmiAdapter = new WagmiAdapter({
  projectId,
  networks
})

// 3. Configure the metadata
const metadata = {
  name: 'AppKit',
  description: 'AppKit Example',
  url: 'https://example.com', // origin must match your domain & subdomain
  icons: ['https://avatars.githubusercontent.com/u/179229932']
}

// 3. Create the modal
const modal = createAppKit({
  adapters: [wagmiAdapter],
  networks: [mainnet, arbitrum],
  metadata,
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