# Environments

Throughout the Abacus Code bases exist the concept of environments to facilitate the development and testing of changes, both of the Abacus core platform as well as applications building on top of Abacus. Environments also encode the set of domains/chains that are supported. This page outlines the purpose of each environment and how developers should think about them.

### Environment: "test"

The `test` environment is meant for local development. Application developers can use the `@abacus-network/hardhat` plugin's `TestAbacusDeploy` object to deploy a mocked Abacus core platform. By calling `processMessages()`, developers can simulate the processing of messages across domains without having to run any of the Agents.

The domains that are supported by the `sdk` are artificial chains `test1`, `test2`, and `test3` which are all deployed on the same hardhat-network node, either in unit tests setup by `hardhat` or a dedicated node that is run via `hardhat node`. Local end-to-end tests should be run in the `test` environment as well. Developers can use the `getMultiProviderFromConfigAndSigner` from `@abacus-network/deploy` to construct a `MultiProvider` that works for the `test` environment.

### Environment: "dev"

The `dev` environment is used by Abacus Works developers to test Agent changes. Developers are free to use this environment but should not expect any SLAs with respect to uptime.

The domains that are supported by the `sdk` are `alfajores` and `kovan`.

### Environment: "testnet"

The `testnet` environment is where developers should expect to make integration tests of their app. Analogous to traditional software engineering practices, `testnet` is Abacus' staging environment. It's where one can test deployment tooling to real remote networks, as well as UI and SDK integrations. Agents are run as close as possible to mainnet and the relayer will expect Interchain gas payments in order to process messages on the destination chain.

Developers can interact with `testnet` Abacus core deployment by calling

```typescript
import { AbacusCore } from '@abacus-network/sdk';

const core = AbacusCore.fromEnvironment(environment, multiProvider);
```

The domains that are supported are `alfajores`, `kovan`, `fuji`, `mumbai`, `bsctestnet`, `arbitrumrinkeby`, `optimismkovan`. You can find the contract addresses under the Contract Addresses section.

### Environment: "mainnet"&#x20;

TBD
