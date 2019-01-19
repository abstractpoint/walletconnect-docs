# For Dapps (Browser SDK)

1.  Install

```bash
yarn add walletconnect

# OR

npm install --save walletconnect
```

2.  Example

```js
import WalletConnect from "walletconnect";
import WalletConnectQRCodeModal from "walletconnect-qrcode-modal";

/**
 *  Create a webConnector
 */
const webConnector = new WalletConnect({
  bridgeUrl: "https://test-bridge.walletconnect.org", // Required
  dappName: "INSERT_DAPP_NAME" // Required
});

/**
 *  Initiate WalletConnect session
 */
await webConnector.initSession();

/**
 *  Check if connection is already established
 */
if (webConnector.isConnected) {
  // If yes, get accounts
  const accounts = webConnector.accounts;
} else {
  // If not, prompt the user to scan the QR code
  const uri = webConnector.uri;

  // Listen for session confirmation from wallet
  await webConnector.listenSessionStatus();

  // Get accounts after session status is resolved
  accounts = webConnector.accounts;
}

/**
 *  Draft transaction
 */
const tx = {
  from: "0xbc28ea04101f03ea7a94c1379bc3ab32e65e62d3",
  to: "0x0",
  nonce: 1,
  gas: 100000,
  value: 0,
  data: "0x0"
};

/**
 *  Send transaction
 */
try {
  // Submitted Transaction Hash
  const result = await webConnector.sendTransaction(tx);
} catch (error) {
  // Rejected Transaction
  console.error(error);
}

/**
 *  Draft Message Parameters
 */
const msgParams = [
  "0xbc28ea04101f03ea7a94c1379bc3ab32e65e62d3",
  "My email is john@doe.com - 1537836206101"
];

/**
 *  Sign message
 */
try {
  // Signed message
  const result = await webConnector.signMessage(msgParams);
} catch (error) {
  // Rejected signing
  console.error(error);
}

/**
 *  Draft Typed Data
 */
const msgParams = [
  "0xbc28ea04101f03ea7a94c1379bc3ab32e65e62d3",
  {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "chainId", type: "uint256" },
        { name: "verifyingContract", type: "address" }
      ],
      Person: [
        { name: "name", type: "string" },
        { name: "account", type: "address" }
      ],
      Mail: [
        { name: "from", type: "Person" },
        { name: "to", type: "Person" },
        { name: "contents", type: "string" }
      ]
    },
    primaryType: "Mail",
    domain: {
      name: "Example Dapp",
      version: "0.7.0",
      chainId: 1,
      verifyingContract: "0x0000000000000000000000000000000000000000"
    },
    message: {
      from: {
        name: "Alice",
        account: "0xaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
      },
      to: {
        name: "Bob",
        account: "0xbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb"
      },
      contents: "Hey, Bob!"
    }
  }
];

/**
 *  Sign Typed Data
 */
try {
  // Signed typed data
  const result = await webConnector.signTypedData(msgParams);
} catch (error) {
  // Rejected signing
  console.error(error);
}
```

## For Dapps using Web3 Provider (web3.js)

1.  Install

```bash
/**
 *  Install NPM Package
 */

yarn add web3 walletconnect-web3-provider

# OR

npm install --save web3 walletconnect-web3-provider
```

2.  Example

```js
import Web3 from 'web3'
import WalletConnectProvider from 'walletconnect-web3-provider'

/**
 *  Create WalletConnect Provider
 */
const provider = new WalletConnectProvider({
  bridgeUrl: 'https://test-bridge.walletconnect.org',   // Required
  dappName: 'INSERT_DAPP_NAME',                   // Required
  rpcUrl: 'http://localhost:8545'                 // Required
}

/**
 *  Create Web3
 */
const web3 = new Web3(provider)

/**
 *  Initiate WalletConnect Session
 */
const session = await web3.currentProvider.walletconnect.initSession()

/**
 *  Get Accounts
 */
const accounts = await web3.eth.getAccounts()

if (!accounts.length) {
  // Display QR Code URI
  const uri = web3.currentProvider.walletconnect.uri

  // Listen for session status
  await  web3.currentProvider.walletconnect.listenSessionStatus()

  // Get Accounts Again
  accounts = await web3.eth.getAccounts()
}

/**
 * Send Transaction
 */
const txHash = await web3.eth.sendTransaction(tx)

/**
 * Sign Transaction
 */
const signedTx = await web3.eth.signTransaction(tx)

/**
 * Sign Message
 */
const signedMessage = await web3.eth.sign(msg)

/**
 * Sign Typed Data
 */
const signedTypedData = await web3.eth.signTypedData(msg)
```