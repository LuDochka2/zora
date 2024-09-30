# zoraconst Web3 = require('web3');

// Connect to an Ethereum node (e.g., Infura, Alchemy, or local node)
const web3 = new Web3('https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID');

// Zora Market contract address on Ethereum mainnet
const ZORA_MARKET_CONTRACT_ADDRESS = '0xabEFBc9fD2F806065b4f3C237d4b59D9A97Bcac7';

// ABI for Zora Market contract (simplified for demo)
const ZORA_MARKET_ABI = [
  {
    "constant": true,
    "inputs": [{ "name": "_tokenId", "type": "uint256" }],
    "name": "fetchMedia",
    "outputs": [
      { "name": "creator", "type": "address" },
      { "name": "currentOwner", "type": "address" },
      { "name": "contentHash", "type": "bytes32" }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  }
];

// Instantiate Zora Market contract
const zoraMarket = new web3.eth.Contract(ZORA_MARKET_ABI, ZORA_MARKET_CONTRACT_ADDRESS);

// Fetch data for a specific token ID
async function getZoraNFTData(tokenId) {
  try {
    const mediaData = await zoraMarket.methods.fetchMedia(tokenId).call();
    
    console.log(`Creator: ${mediaData.creator}`);
    console.log(`Current Owner: ${mediaData.currentOwner}`);
    console.log(`Content Hash: ${mediaData.contentHash}`);
  } catch (error) {
    console.error('Error fetching media data:', error);
  }
}

// Example token ID (replace with an actual Zora NFT token ID)
const TOKEN_ID = 1;

// Call the function to get NFT data
getZoraNFTData(TOKEN_ID);
