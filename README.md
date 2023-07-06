# NFTarf

NFTarf is a Solidity smart contract that implements an ERC721-compliant non-fungible token (NFT) with random metadata generation using Chainlink VRF.

## Contracts

### NFTarf.sol

NFTarf.sol is the main contract that represents the NFT. It inherits from ERC721, ERC721Enumerable, ERC721URIStorage, and Ownable contracts from the OpenZeppelin library. It also uses the VRFv2Consumer contract.

#### Functions

- `setVrf(address vrfAddr) external`: Sets the address of the VRF contract.
- `safeMint() public`: Mints a new NFT for the caller with a random tokenURI.
- `randomMint(uint256 randomNumber, uint256 requestId) external`: Called by the VRF contract to set the tokenURI based on the random number generated.
- `_beforeTokenTransfer(address from, address to, uint256 tokenId, uint256 batchSize)`: Overrides the function from ERC721Enumerable.
- `_burn(uint256 tokenId) internal`: Overrides the function from ERC721URIStorage.
- `tokenURI(uint256 tokenId) public view`: Overrides the function from ERC721URIStorage.
- `supportsInterface(bytes4 interfaceId) public view`: Overrides the function from ERC721URIStorage.

### VRFv2Consumer.sol

VRFv2Consumer.sol is a contract that represents a consumer of Chainlink VRF. It inherits from VRFConsumerBaseV2 and ConfirmedOwner contracts. It interacts with the NFTarf contract to fulfill random word requests.

#### Functions

- `setNft(address nftAddr) external`: Sets the address of the NFTarf contract.
- `requestRandomWords() external returns (uint256 requestId)`: Requests random words from the Chainlink VRF.
- `fulfillRandomWords(uint256 _requestId, uint256[] memory _randomWords) internal override`: Callback function called by Chainlink VRF when random words are generated.
- `getRequestStatus(uint256 _requestId) external view returns (bool fulfilled, uint256[] memory randomWords)`: Retrieves the status of a previous request.

## Installation

To use these contracts, follow these steps:

1. Clone the repository.
2. Install the dependencies by running `npm install`.
3. Deploy the contracts to your preferred network.
4. Interact with the contracts using the provided functions.

## Remix Default Workspace

Remix default workspace is present when:

i. Remix loads for the very first time
ii. A new workspace is created with the 'Default' template
iii. There are no files existing in the File Explorer

This workspace contains 3 directories:

1. 'contracts': Holds three contracts with increasing levels of complexity.
2. 'scripts': Contains four typescript files to deploy a contract. It is explained below.
3. 'tests': Contains one Solidity test file for the 'Ballot' contract & one JS test file for the 'Storage' contract.

### Scripts

The 'scripts' folder has four TypeScript files which help to deploy the 'Storage' contract using the 'web3.js' and 'ethers.js' libraries.

For the deployment of any other contract, just update the contract's name from 'Storage' to the desired contract and provide constructor arguments accordingly in the file `deploy_with_ethers.ts` or `deploy_with_web3.ts`.

In the 'tests' folder, there is a script containing Mocha-Chai unit tests for the 'Storage' contract.

To run a script, right-click on the file name in the file explorer and click 'Run'. Remember, the Solidity file must already be compiled.
The output from the script will appear in the Remix terminal.

Please note, `require`/`import` is supported in a limited manner for Remix-supported modules.
For now, modules supported by Remix are ethers, web3, swarmgw

## License

The NFTarf contracts are licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.

