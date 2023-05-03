# zkBlocks
Interoperability and composability - paving the way for the future of blockchain with direct rollup communication with Zero-Knowledge


## Based on code from OpenZeppelin - Cairo-contracts
### Contributing to OpenZeppelin Contracts for Cairo 


# OpenZeppelin Contracts for Cairo

[![Tests and linter](https://github.com/OpenZeppelin/cairo-contracts/actions/workflows/coverage.yml/badge.svg)](https://github.com/OpenZeppelin/cairo-contracts/actions/workflows/coverage.yml)
[![codecov](https://codecov.io/github/OpenZeppelin/cairo-contracts/branch/main/graph/badge.svg?token=LFSZH8RPOL)](https://codecov.io/github/OpenZeppelin/cairo-contracts)

**A library for secure smart contract development** written in Cairo for [Starknet](https://starkware.co/product/starknet/), a decentralized ZK Rollup.

## Usage

> ## ⚠️ WARNING! ⚠️
>
> This repo contains highly experimental code.
> Expect rapid iteration.
> **Using at my own risk.**

### Getting Started?

Before installing Cairo on your machine, you need to install `gmp`:

```bash
sudo apt install -y libgmp3-dev # linux
brew install gmp # mac
```

> If you have any troubles installing gmp on your Apple M1 computer, [here’s a list of potential solutions](https://github.com/OpenZeppelin/nile/issues/22).

### Set up your project

Create a directory for your project, then `cd` into it and create a Python virtual environment.

```bash
mkdir zkBlocks
cd zkBlocks
python3 -m venv zkBlocks
source zkBlocks/bin/activate
```

Install the [Nile](https://github.com/OpenZeppelin/nile) development environment and then run `init` to kickstart a new project. Nile will create the project directory structure and install [the Cairo language](https://www.cairo-lang.org/docs/quickstart.html), a [local network](https://github.com/Shard-Labs/starknet-devnet/), and a [testing framework](https://docs.pytest.org/en/6.2.x/).

```bash
pip install cairo-nile
nile init
```

### Install the library

```bash
pip install openzeppelin-cairo-contracts
```

> ⚠️ Warning! ⚠️  
Installing directly the `main` branch may contain incomplete or breaking implementations, download [official releases](https://github.com/OpenZeppelin/cairo-contracts/releases/) only.

### Use a basic preset

Presets are ready-to-use contracts that you can deploy right away. They also serve as examples of how to use library modules. [Read more about presets](https://docs.openzeppelin.com/contracts-cairo/0.6.1/extensibility#presets).

```cairo
// contracts/MyToken.cairo

%lang starknet

from openzeppelin.token.erc20.presets.ERC20 import (
    constructor,
    name,
    symbol,
    totalSupply,
    decimals,
    balanceOf,
    allowance,
    transfer,
    transferFrom,
    approve,
    increaseAllowance,
    decreaseAllowance
)
```

Compile and deploy it right away:

```bash
nile compile

nile deploy MyToken <name> <symbol> <decimals> <initial_supply> <recipient> --alias my_token
```

> Note that `<initial_supply>` is expected to be two integers i.e. `1` `0`. See [Uint256](https://docs.openzeppelin.com/contracts-cairo/0.6.1/utilities#uint256) for more information.

### Write a custom contract using library modules

[Read more about libraries](https://docs.openzeppelin.com/contracts-cairo/0.6.1/extensibility#libraries).

```cairo
%lang starknet

from starkware.cairo.common.cairo_builtins import HashBuiltin
from starkware.cairo.common.uint256 import Uint256
from openzeppelin.security.pausable.library import Pausable
from openzeppelin.token.erc20.library import ERC20

(...)

@external
func transfer{syscall_ptr: felt*, pedersen_ptr: HashBuiltin*, range_check_ptr}(
    recipient: felt, amount: Uint256
) -> (success: felt) {
    Pausable.assert_not_paused();
    return ERC20.transfer(recipient, amount);
}
```

## Learn

### Documentation

Check out the [full documentation site](https://docs.openzeppelin.com/contracts-cairo)! Featuring:

- [Accounts](https://docs.openzeppelin.com/contracts-cairo/0.6.1/accounts)
- [ERC20](https://docs.openzeppelin.com/contracts-cairo/0.6.1/erc20)
- [ERC721](https://docs.openzeppelin.com/contracts-cairo/0.6.1/erc721)
- [ERC1155](https://docs.openzeppelin.com/contracts-cairo/0.6.1/erc1155)
- [Contract extensibility pattern](https://docs.openzeppelin.com/contracts-cairo/0.6.1/extensibility)
- [Proxies and upgrades](https://docs.openzeppelin.com/contracts-cairo/0.6.1/proxies)
- [Security](https://docs.openzeppelin.com/contracts-cairo/0.6.1/security)
- [Utilities](https://docs.openzeppelin.com/contracts-cairo/0.6.1/utilities)

### Cairo

- [Starknet official documentation](https://www.cairo-lang.org/docs/hello_starknet/index.html#hello-starknet)
- [Cairo language documentation](https://www.cairo-lang.org/docs/hello_cairo/index.html#hello-cairo)
- Perama's [Cairo by example](https://perama-v.github.io/cairo/by-example/)
- [Cairo 101 workshops](https://www.youtube.com/playlist?list=PLcIyXLwiPilV5RBZj43AX1FY4FJMWHFTY)

### Nile

- [Getting started with Starknet using Nile](https://medium.com/coinmonks/starknet-tutorial-for-beginners-using-nile-6af9c2270c15)
- [How to manage smart contract deployments with Nile](https://medium.com/@martriay/manage-your-starknet-deployments-with-nile-%EF%B8%8F-e849d40546dd)


## License

OpenZeppelin Contracts for Cairo is released under the [MIT License](LICENSE).


