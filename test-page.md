# Test page

```http
wc:{topic...}@{version...}?bridge={url...}&key={key...}
```

| Required parts | Notes |
| :--- | :--- |
| wc: | Wallet Connect protocol defined in [EIP-1328](https://eips.ethereum.org/EIPS/eip-1328) |
| _topic_ | String |
| _version_ | Number \(eg. 1.9.0\) |
| _bridge_ | Bridge URL \(URL Encoded\) |
| _key_ | Symmetric key hex string |

Other query string parameters are all optional.

```http
// Example URL
wc:8a5e5bdc-a0e4-4702-ba63-8f1a5655744f@1?bridge=https%3A%2F%2Fbridge.walletconnect.org&key=41791102999c339c844880b23950704cc43aa840f3739e365323cda4dfa89e7a
```

