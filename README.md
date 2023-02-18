# FCC Launchpad: A Solana launchpad focused on security, reliability, and speed 

The Fat Cats Capital Launchpad is a world class Solana NFT launchpad designed to help launch nft collections and ensure a flawless mint day for new projects. It is built on top of Metaplex's Candy Machine V2 (used for majority of Solana NFTs) and retains all of the functionality of CMV2 plus much more. 


# Security

The FCC Launchpad has been built with a security first mindset using the best technology available today. The core source code of the launchpad has had a full security audit completed by top security researches at OtterSec. The contents of that audit can be viewed here : https://docsend.com/view/is7963h8tbbvp2g9. There were no Major findings and 5 out of the 6 low priority findings have since been fixed and fixes deployed by the FCC development team/author's of this launchpad. Having launchpad's audited is not a standard practice in this industry because of the high associated cost. However, having the FCC launchpad was a no-brainer as we wanted every user of this launchpad to have no doubts about the superior security provided by using a highly reviewed, well tested, and highly secure launchpad.


# Speed

Given that multiple studies have demonstrated that site speed affects conversion rate, the FCC launchpad has been designed and architected to be as fast as possible using the latest and greatest techonolgies available today. 


lightning fast, production


# Reliability

The FCC launchpad is highly fault tolerant, and is built with an architecture that has a near zero chance of downtime even during peak traffic. It can easily handle millions of concurrent users with no issues and has built in security mechanisms to defend against DDOS and other sophisticated attacks.
* multiple RPC endpoints




# Features

* Automated deployment of NFT smart contracts to Solana testnet and Mainnet networks
* Automated uloading of NFT assets / metadata to multiple configurable environments including aws and arweave
* Automated validation of metadata to ensure proper formatting
* Random/Unpredictable Mint Index (This eliminates the possibility of gaming the system and minting rarer items)
* NFTs can be deployed with multiple configuration options
* Emergency Captcha (Will force captcha usage when bots are detected)
* Uses latest LTS version(22.04) for ubuntu and has been fully tested with this version
* Accept solana and other spl tokens as payment

# Configuration Options

* Whitelist
* Presale
* Accept solana and other spl tokens as payment
* Optional captcha for bot detection
* Configurable go live date and countdown timer
* Mutable/Immutable NFTs
* End Mint Settings (date vs mint amount)
* Royalty/Treasury address






The core code of the launchpad has been audited by OtterSec. security of the launchpad https://docsend.com/view/is7963h8tbbvp2g9

This is a helper repo containing bash scripts for setting up the sugar CLI (https://docs.metaplex.com/tools/sugar/) and deploying a candy machine on the solana network. This Repo is set to work with ubuntu 22.04 (LTS) and has not been tested to run on any other OS. You will need to have an `assets` directory set up with all of the NFT images and configs. The assets directory should also contain a collection image (collection.png) and a collection config(collection.json). You will also need a `config.json` file in the root directory containing the candy machine's config file.

# Sugar/Solana Install Script
The first script to run is the installation script for the sugar and solana CLI

> ```bash
> bash 1-install-sugar-solana-bash
> ```

The first thing this script will do is install the sugar CLI. It will also update the openssl/libssl package to fix a packaging issue in ubuntu 22.04 (https://stackoverflow.com/questions/72378647/spl-token-error-while-loading-shared-libraries-libssl-so-1-1-cannot-open-shar)

After sugar is succesfully installed and the packages updated, the script will install the latest stable version of the solana CLI. The script will then update the PATH variable and print out the version of Solana that was installed.

# Solana Wallet Setup Script:

There are two scripts for the set up of the solana wallet and setting the config that will be used for deploying the candy machine. One is for devnet and one is for mainnet.

devnet:
> ```bash
> bash 2-setup-devnet.bash
> ```

mainnet:
> ```bash
> bash 2-setup-mainnet.bash
> ```

# Deploy Candy Machine Script:

This is the script that deploys the candy machine. The first step is that it will run the validate command which will check that all files in the assets folder are in the correct format. The next thing this script will do is run the upload command which uploadss assets to the specified storage (bundlr arweave) and creates the cache file for the Candy Machine. The script will then deploy the candy machine and verify that all items in the cache file have been successfully written on-chain. Finally the script will run the show command which displays the on-chain config of an existing candy machine.

> ```bash
> bash 3-deploy-candy-machine.bash
> ```

# Update Candy Machine Script:

The update script will be used for making changes to the live candy machine. You will simply need to update the config.json to the desired config and then run the update bash script.

> ```bash
> bash 4-update-candy-machine.bash

# Withdraw Rent and Destroy Candy Machine Script:

The withdraw and destroy script will first withdraw all of the solana that is reserved for paying rent from the candy machine. It will then delete the cache.json file so that a new candy machine can be deployed.

> ```bash
> bash 5-withdraw-rent-and-destroy-candy-machine.bash
