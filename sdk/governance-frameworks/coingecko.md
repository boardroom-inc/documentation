# CoinGecko

CoinGecko is a crypto market analysis platform. It provides a public API that can be used to fetch token information and market stats for several popular protocols. 

{% hint style="info" %}
Check out the CoinGecko API here: [https://www.coingecko.com/en/api](https://www.coingecko.com/en/api)
{% endhint %}

## Using The CoinGecko Adapter

As an example, Rarible is listed on CoinGecko : [https://www.coingecko.com/en/coins/rarible](https://www.coingecko.com/en/coins/rarible)

We can see the `rarible` slug in the URL, this is the "Token ID" that CoinGecko needs to fetch information for it. This is all that is required when setting up a new CoinGecko adapter:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { CoinGeckoAdapter } from '@boardroom/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'rarible',
    name: 'Rarible',
    adapters: (adapters) => {
      const coingecko = new CoinGeckoAdapter('rarible', transports);
      adapters.implement('token', coingecko);
      adapters.implement('icons', coingecko);
      // ... other adapters 
    },
  });
};
```

We call `adapters.implement` for both the [Token Adapter](../adapters/token-adapter.md) as well as the [Icons Adapter](../adapters/icon-adapter.md) interfaces, since the CoinGecko adapter implements both [adapter](../adapters/) interfaces.

