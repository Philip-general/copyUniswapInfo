# 실행과정

1. The Graph 접속해서 subgraph 생성해준다.
2. 현재 github repository와 연결한다.
3. 생성하면 시키는대로 graph protocol 설치 후 graph init 진행
4. graph init 하는데 uniswap v2를 그대로 실행시켜볼 것이기 때문에 factory adress 를 contract adress에 입력해준다.
5. abi fetching에 실패할 경우에 etherscan에 접속하여 직접 abi 파일을 긁어오자.
6. filepath를 입력해주면 그 경로의 abi를 토대로 빌드를 해준다.

7. graph auth <accesstoken> 실행
8. cd copyUniswapInfo
9. yarn deploy

deploy tutorial
https://thegraph.academy/developers/deploying-a-subgraph/
fork uniswap & create your own sushiswap
https://www.youtube.com/watch?v=U3fTTqHy7F4

---

# Uniswap V2 Subgraph

[Uniswap](https://uniswap.org/) is a decentralized protocol for automated token exchange on Ethereum.

This subgraph dynamically tracks any pair created by the uniswap factory. It tracks of the current state of Uniswap contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers
- historical data on Uniswap, pairs or tokens, aggregated by day

## Running Locally

Make sure to update package.json settings to point to your own graph account.

## Queries

Below are a few ways to show how to query the uniswap-subgraph for data. The queries show most of the information that is queryable, but there are many other filtering options that can be used, just check out the [querying api](https://thegraph.com/docs/graphql-api). These queries can be used locally or in The Graph Explorer playground.

## Key Entity Overviews

#### UniswapFactory

Contains data across all of Uniswap V2. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### Pair

Contains data on a specific pair.

#### Transaction

Every transaction on Uniswap is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying Aggregated Uniswap Data

This query fetches aggredated data from all uniswap pairs and tokens, to give a view into how much activity is happening within the whole protocol.

```graphql
{
  uniswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```
