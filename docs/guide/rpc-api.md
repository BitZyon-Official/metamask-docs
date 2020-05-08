# The Ethereum RPC API

MetaMask uses the `ethereum.request()` method to wrap an RPC API which is based on an interface exposed by all Ethereum clients, with some extra methods that are provided by MetaMask, as a key-holding signer. You can look up how to pass these methods to the `window.ethereum` object [here](./ethereum-provider.html).

For the full API, please see [EIP 1474](https://eips.ethereum.org/EIPS/eip-1474).

#### RPC Protocols

Multiple RPC protocols may be available. For examples, see:

- [EIP 1474](https://eips.ethereum.org/EIPS/eip-1474), the Ethereum JSON-RPC API

### eth_requestAccounts

Requests that the user provides one or more Ethereum addresses to be identified by.
Returns a Promise that resolves to an array of hex-prefixed ethereum address strings.
See [EIP 1102](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1102.md) for more details.

You should only request the user's accounts in response to user action, such as a button click.
Otherwise, you will spam the user with a pop-up they didn't ask for.
If you can't retrieve the user's account(s), you should encourage the user to initiate an account request.

#### Example

```javascript
document.getElementById('connectButton', connect)

function connect () {
  ethereum.request({ method: 'eth_requestAccounts' })
    .then(handleAccountsChanged)
    .catch(err => {
      if (err.code === 4001) { // EIP 1193 userRejectedRequest error
        console.log('Please connect to MetaMask.')
      } else {
        console.error(err)
      }
    })
}
```
