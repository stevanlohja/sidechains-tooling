<a name="readme-top"></a>
<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/input-output-hk/sidechains-tooling">
    <span style="font-size: 2em;">⛓️</span>
  </a>

<h3 align="center">Cardano Sidechains Tooling</h3>

  <p align="center">
    Helpful tools for sidechain builders.
    <br />
    <br />
    <a href="https://docs.cardano.org/cardano-sidechains/basics/introduction-sidechains">Read the Docs</a>
    ·
    <a href="https://github.com/input-output-hk/sidechains-tooling/issues">Report Bug</a>
    ·
    <a href="https://github.com/input-output-hk/sidechains-tooling/issues">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<!-- Use markdown all-in one vs-code extension to automate table of contents generation. -->
<details>
  <summary>Table of Contents</summary>
  
- [About](#about)
- [Getting Started](#getting-started)
  - [Installation](#installation)
- [Usage](#usage)
  - [Reference](#reference)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

</details>

<!-- ABOUT THE PROJECT -->
## About
This project contains helpful tools for Cardano sidechain builders.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->
## Getting Started

The project hosts CLI tooling to assist sidechain builders with common tasks. If you're new to Cardano sidechains, then go ahead and visit the documentation linked above to learn more.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Installation

1. Download the packaged binaries for `sc-evm-cli`, `sidechain-cli` and `trustless-sidechain-cli` on the *releases* page
   [>>>](https://github.com/input-output-hk/sidechains-tooling/releases)

2. Extract the packages using your preferred `tar` and `zip` utility.

3. Add binaries to your shell's path for greater convenience.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- USAGE EXAMPLES -->
## Usage

```shell
./sc-evm-cli <subcommand> <arguments...>
```

```shell
./sidechain-cli <subcommand> <arguments...>
```

```shell
node <trustless-sidechain-ctl-directory>/main.js <subcommand> <arguments>
```
## Note for macOS users
When you execute a command for the first time, you will get a warning pop-up complaining that the ABI cannot be executed because the developer cannot be verified.  
The workaround is this:
1. Press cancel on the pop-up
2. Stop the CLI process with command-C
2. Go to System settings → Privacy & Security tab to allow the app
3. Click Allow anyway
4. Repeat for one more library.

### Reference

`sc-evm-cli` reference guide [>>>](SC_EVM_CLI_Reference.md) 

`sidechain-cli` reference guide [>>>](SC_CLI_Reference.md)

`trustless-sidechain-cli` reference guide [>>>](Trustless_Sidechain_CTL_Reference.md) 

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated. See [CONTRIBUTING.md](CONTRIBUTING.md) for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- LICENSE -->
## License

Distributed under the Apache 2.0 License. See [LICENSE.md](LICENSE.md) for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTACT -->
## Contact

See "Communication channels" in [CONTRIBUTING.md](CONTRIBUTING.md). 

<p align="right">(<a href="#readme-top">back to top</a>)</p>