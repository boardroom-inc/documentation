# Uniswap V2

Uniswap is a decentralized exchange protocol that allows users to swap tokens via an automated market maker. 

{% hint style="info" %}
Check out the Uniswap developer docs here: [https://uniswap.org/docs/v2/](https://uniswap.org/docs/v2/)
{% endhint %}

## Using The Uniswap V2 Adapter

As an example, Aave, like most popular protocols, has a large volume of liquidity in Uniswap V2. The token address for **$AAVE** is `0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9`:

* [https://etherscan.io/address/0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9](https://etherscan.io/address/0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9)

We can use Etherscan to query the contract to find that the ERC-20 `decimals` value is set to the semi-standard "18". We can use this information to instantiate a `UniswapV2Adapter` instance: 

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { UniswapV2Adapter } from '@boardroom/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'rarible',
    name: 'Aave',
    adapters: (adapters) => {
      const uniswap = new UniswapV2Adapter(
        '0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9', 'AAVE', 18);
      adapters.implement('token', uniswap);
      // ... other adapters 
    },
  });
};
```

The Uniswap V2 adapter only implements the [Token Adapter](../adapters/token-adapter.md), so we announce a single adapter implementation to the SDK.

