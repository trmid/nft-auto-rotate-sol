# Experiment: Auto-Rotating NFT

[![Coverage Status](https://coveralls.io/repos/github/friends-of-pooly/nft-auto-rotate-sol/badge.svg?branch=master)](https://coveralls.io/github/friends-of-pooly/nft-auto-rotate-sol?branch=master)

![Tests](https://github.com/friends-of-pooly/nft-auto-rotate-sol/actions/workflows/main.yml/badge.svg)

# Overview

The Auto-Rotating NFT experiment will test rotating on-chain NFT metadata descriptors.

### Why

The Friends of Pooly recently had a PFP contest. Several artists contributed art to the FoP assets collection. It would be great to showcase artist with contributions with a Friends of Pooly NFT that automatically rotates to a new artist submission.

### How

NFT can generate item `metadata` completely on-chain; compared to the more commonly IPFS or centralized server approach to store the information.

By generating the NFT metadata on-chain it's possible to rotate the image using `blockNumber` or `timestamp`.

Using this approach new FoP artists submissions can be automatically featured without requiring a transaction to update the blockchain.

**Example**

```sol
function constructTokenURI(uint256 _tokenId) public view returns (string memory) {
  /// @dev A different image should be returned depending on the timestamp
  ///      An array of IPFS hashes (or encoded on-chain SVGs) is stored.
  string memory image = generateSVGImage(_tokenId, block.timestamp);

  return
    string(
      abi.encodePacked(
        "data:application/json;base64,",
        Base64.encode(
          bytes(
            abi.encodePacked(
              '{"name":"',
              params.name,
              '", "description":"',
              params.description,
              '", "image": "',
              image,
              '"}'
            )
          )
        )
      )
    );
}

```

# Installation

Install the repo and dependencies by running:
`yarn`

## Deployment

These contracts can be deployed to a network by running:
`yarn deploy <networkName>`

## Verification

These contracts can be verified on Etherscan, or an Etherscan clone, for example (Polygonscan) by running:
`yarn etherscan-verify <ethereum network name>` or `yarn etherscan-verify-polygon matic`

# Testing

Run the unit tests locally with:
`yarn test`

## Coverage

Generate the test coverage report with:
`yarn coverage`
