### Migration

- migration은 js 파일을 통해 실행한다.

- ``truffle migrate``를 실행하면 프로젝트에 위치한 모든 migration js 파일을 실행한다.
- migration은 deployment script들의 집합이다.
- local에서 테스트 하려면, migrate하기 전에 ganache와 같은 test blockchain을 실행해야 한다.
- migration js 파일은 numbering이 되어야 한다: ``1_initial_igration.js`` ``2_example_migration.js``

### artifacts.require()

- ``artifacts.require()``을 통해서 truffle에게 어떤 컨트랙트와 소통할지 알려준다. (Node의 ``require``와 유사)
- ``artifacts.require()``에는 파일의 이름이 아니라, 컨트랙트의 이름이 들어가야 한다. (1개의 파일에 여러 컨트랙트가 포함되어 있을 수도 있기 때문)
- 따라서 모든 컨트랙트에 대하여 하나씩 ``artifacts.require()``을 작성하여야 한다.

### module.export 

- 모든 migration은 ``module.export`` syntax를 통해 함수를 export해야 한다.
- 각각의 migration에 의해 export된 이 함수는 1번째 parameter로 ``deployer`` 객체를 받아야 한다.
- ``deployer``는 1) clear syntax 2) 배포의 추가적인 기능들 (배포된 artifact를 나중에 쓰기 위해서 저장하는 등)을 위한 편의를 제공한다.
- 실제로 ``truffle migrate``를 실행하면, 마지막에 "Saving artifacts" 라는 문구를 볼 수 있다.

### Test scenario

* ganache의 default port는 7545
* metamask의 localhost default port는 8545
* 바꾸는게 덜 귀찮은 ganache의 port를 변경

1. ``truffle migrate`` 
2. ``artifacts.require()``를 통해 모든 컨트랙트가 migrate되기 때문에 1번에서 이미 완료
3. migration이 성공적으로 완료되었다면, 토큰이 차감 (ganache와 일치)

```
yeonlee@ys-MacBookPro mock_uniswap % truffle migrate

Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.



Starting migrations...
======================
> Network name:    'development'
> Network id:      5777
> Block gas limit: 6721975 (0x6691b7)


1_initial_migration.js
======================

   Replacing 'Migrations'
   ----------------------
   > transaction hash:    0x7ac00b6b65dbef2a911d3893d9188efa6eb7b5336f06614a81a15b939499c85b
   > Blocks: 0            Seconds: 0
   > contract address:    0xEb1DC69bC94142029A34e2706D4c6f6343C18372
   > block number:        1
   > block timestamp:     1627059693
   > account:             0x3e3888402429480DfAA2901cA41D1cb58EE5BD5A
   > balance:             99.99626098
   > gas used:            186951 (0x2da47)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00373902 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00373902 ETH


2_deploy_contracts.js
=====================

   Replacing 'TK0'
   ---------------
   > transaction hash:    0x27eacae9f2d1fcfdfe6343bbc3f129a757c76583d26d99d075858486f9e566a7
   > Blocks: 0            Seconds: 0
   > contract address:    0x5D40eb795CFB66ed0D912108b60049600bAf2873
   > block number:        3
   > block timestamp:     1627059693
   > account:             0x3e3888402429480DfAA2901cA41D1cb58EE5BD5A
   > balance:             99.9543258
   > gas used:            2054424 (0x1f5918)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.04108848 ETH


   Replacing 'TK1'
   ---------------
   > transaction hash:    0xa8b6b0f1e6dfe055f22bbd227c952b400f9708af01067810460262bfa6e260c9
   > Blocks: 0            Seconds: 0
   > contract address:    0xabaA2817c45D99757d0CCbF59fd964c52F0F24d0
   > block number:        4
   > block timestamp:     1627059694
   > account:             0x3e3888402429480DfAA2901cA41D1cb58EE5BD5A
   > balance:             99.91323732
   > gas used:            2054424 (0x1f5918)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.04108848 ETH


   Replacing 'Exchange'
   --------------------
   > transaction hash:    0xf8bce83543ec357d28ee5b55fefd2884dd02149f7f0e92658b21deec40973145
   > Blocks: 0            Seconds: 0
   > contract address:    0x093C6397aa6Bc4FDbeD8FD19FD51CFA1f9E4Ee92
   > block number:        5
   > block timestamp:     1627059694
   > account:             0x3e3888402429480DfAA2901cA41D1cb58EE5BD5A
   > balance:             99.89487132
   > gas used:            918300 (0xe031c)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.018366 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.10054296 ETH


Summary
=======
> Total deployments:   4
> Final cost:          0.10428198 ETH

```

### Notes

1. ``deployer``를 구체적으로 어떻게 사용하는지
2. 저장된 artifacts는 어떻게 쓰이는지
3. ``truffle init``

