# For Wallets (React-Native SDK)

1.  Install

```bash
/**
 *  Install NPM Package
 */

yarn add rn-walletconnect-wallet

# OR

npm install --save rn-walletconnect-wallet

/**
 *  Nodify 'crypto' package for cryptography
 */

# install "crypto" shims and run package-specific hacks
rn-nodeify --install "crypto" --hack
```

2.  Example

```js
import RNWalletConnect from 'rn-walletconnect-wallet'

/**
 *  Create WalletConnector
 */
const walletConnector = new RNWalletConnect({
  uri: 'ethereum:wc-8a5e5bdc-a0e4-47...TJRNmhWJmoxdFo6UDk2WlhaOyQ5N0U=',
  push: {
    type: 'fcm',
    token: 'cSgGd8BWURk:APA91bGXsLd_...YdFbutyfc8pScl0Qe8-',
    webhook: 'https://push.walletconnect.org/notification/new',
  }
})

/**
 *  Approve Session
 */
await walletConnector.approveSession({
  accounts: [
    '0x4292...931B3',
    '0xa4a7...784E8',
    ...
  ]
})

/**
 *  Reject Session
 */
await walletConnector.rejectSession()


/**
 *  Kill Session
 */
await walletConnector.killSession()


/**
 *  Handle push notification events & get call data
 */
FCM.on(FCMEvent.Notification, event => {
  const { sessionId, callId } = event;

  const callData = await walletConnector.getCallRequest(callId);

  // example callData
  {
    method: 'eth_sendTransaction',
    data: {
      from: '0xbc28ea04101f03ea7a94c1379bc3ab32e65e62d3',
      to: '0x0',
      nonce: 1,
      gas: 100000,
      value: 0,
      data: '0x0'
    }
  }
});

/**
 *  Get all calls from bridge
 */
const allCalls = await walletConnector.getAllCallRequests();

/**
 *  Approve and share call result
 */
walletConnector.approveCallRequest(
  callId,
  {
    result: '0xabcd...873'
  }
)

/**
 *  Reject call request
 */
walletConnector.rejectCallRequest(
  callId
)
```