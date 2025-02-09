# EIP7702 Goat

Intentionally flawed code with potential pitfalls in custom contracts for [EIP-7702](https://eips.ethereum.org/EIPS/eip-7702) delegate accounts.

Use this repository to learn about 7702 in a practical way. Tweak the contracts and tests, extend them, try out newer and more complex implementations. Whatever you want - except deploying them to prod.

## Overview

Contracts increase in complexity. They're meant to be studied sequentially.

- `DelegateContractV0`
    - Missing `receive` function => can't receive ETH
    - Lack of access controls in execute => anyone can execute calls
- `DelegateContractV1`
    - Deceiving `constructor`. Guardians are not set in the context of accounts delegating to `DelegateContractV1`.
- `DelegateContractV2`
    - Open initialization
    - Can be reinitialized
- `DelegateContractV3` and `DelegateContractV3_1`
    - Initialization signature too weak (e.g., replayable across contracts, chains)
- `DelegateContractV4`
    - Storage collision between `paused` and `init` if deployed as an upgrade of V3. Account may start paused and initialized.
- `DelegateContractV5`
    - Lack of nonce management allows signature replays => `oneTimeSend` can be used to drain the account.
- `DelegateContractV6`
    - Anything bad here?

## What else?

We might extend this repository with flawed cases of:

- Interactions with the [ERC4337 entrypoint](https://eips.ethereum.org/EIPS/eip-4337)
- New signature schemes (such as [WebAuthn](https://github.com/Vectorized/solady/blob/main/src/utils/WebAuthn.sol))
- Standard batch execution interfaces (like [EIP-7821](https://eips.ethereum.org/EIPS/eip-7821))

## Resources

- [EIP-7702: set EOA account code](https://eips.ethereum.org/EIPS/eip-7702)
- [EIP-7821: minimal batch executor interface](https://eips.ethereum.org/EIPS/eip-7821)
- [github.com/ithacaxyz/odyssey-examples](https://github.com/ithacaxyz/odyssey-examples)
- [EIP-7702: a technical deep dive by lightclient](https://www.youtube.com/watch?v=_k5fKlKBWV4)
- [ithaca.xyz/writings/exp-0001](https://www.ithaca.xyz/writings/exp-0001)
- [ithaca.xyz/writings/exp-0002](https://www.ithaca.xyz/writings/exp-0002)
- [github.com/ithacaxyz/account](https://github.com/ithacaxyz/account)
- [EIP-7702 with Scaffold-ETH 2](https://github.com/azf20/seven-seven-zero-two)
- [Basic EOA Batch Executor by @optimizoor](https://x.com/optimizoor/status/1878140195989819586)

## Disclaimer

All code in this repository is intentionally vulnerable and for educational purposes only. DO NOT USE IN PRODUCTION.
