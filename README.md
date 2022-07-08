# evm-chains-extended

Package to query chain data from [ethereum-lists/chains](https://github.com/ethereum-lists/chains) with extended data necessary for EIP3085.

Makes use of Pedro Gomes' [evm-chains](https://github.com/pedrouid/evm-chains) package for the initial data, then merges in the extended data.

Includes Block Explorer URLs and network logos for certain networks.

This package is meant as a holdover and may be deprecated in the future in favor of simply using `evm-chains`. That is dependent on EIPs such as: https://github.com/ethereum/EIPs/pull/3091

NOTE: This also makes use of a silent interface pattern where missing networks will be returned undefined instead of throwing.

## Install

```sh
npm install --save evm-chains-extended

#or

yarn add evm-chains-extended
```

## API

```typescript
function getAllChains(): IChainDataExtended[] | undefined;
function getChain(chainId: number): IChainDataExtended | undefined;
function getChainByChainId(chainId: number): IChainDataExtended | undefined;
function formatNetworkForAddEthereumChain(network: IChainDataExtended): IAddEthereumChainParameter;
```

## Logos

To use network logos import into your dapp:

```typescript
import EthLogo from '@simplicy/evm-chains-extended/dist/umd/images/ethereum-icon.png'
import BscLogo1 from '@simplicy/evm-chains-extended/dist/umd/images/bsc-icon-1.png'
import BscLogo2 from '@simplicy/evm-chains-extended/dist/umd/images/bsc-icon-2.png'
import OptimismLogo from '@simplicy/evm-chains-extended/dist/umd/images/optimism-icon.png'
import PoALogo from '@simplicy/evm-chains-extended/dist/umd/images/poa-icon.png'
import PolygonLogo from '@simplicy/evm-chains-extended/dist/umd/images/polygon-icon.png'
import XDaiLogo from '@simplicy/evm-chains-extended/dist/umd/images/xdai-logo.png'
```

```jsx
// then:
<img src={XDaiLogo} />
```

## Types

```typescript
interface IChainDataExtended {
  name: string;
  chainId: number;
  shortName: string;
  chain: string;
  network: string;
  networkId: number;
  nativeCurrency: {
    name: string;
    symbol: string;
    decimals: number;
  };
  rpc: string[];
  faucets: string[];
  infoURL: string;
  blockExplorerUrls: string[]
}

// format for EIP3085 wallet_addEthereumChain
interface IAddEthereumChainParameter {
  chainId: string; // A 0x-prefixed hexadecimal string
  chainName: string;
  nativeCurrency: {
    name: string;
    symbol: string; // 2-6 characters long
    decimals: number;
  };
  rpcUrls: string[];
  blockExplorerUrls?: string[];
  iconUrls?: string[]; // Currently ignored.
}
```

## Data Source

[https://github.com/ethereum-lists/chains](https://github.com/ethereum-lists/chains)
