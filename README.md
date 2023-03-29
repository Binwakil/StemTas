# STEM NFT AUCTION SYSTEM

Welcome to STEM TAS 

Brief Description about STEM TAS

STEM TAS is a cutting-edge blockchain solution that has been designed to facilitate the exchange of tokens via an English auction for STEM educational resources. The platform enables users, including sellers and bidders, to engage in a transparent and efficient process of exchanging tokens for high-quality STEM education resources.

STEM TAS operates on a decentralized blockchain network that ensures the security and immutability of all transactions conducted on the platform. The use of blockchain technology also ensures that all parties involved in the token auction are verified and can be trusted.

STEM TAS is particularly useful for educators, students, and anyone interested in STEM education, as it provides a transparent and fair platform for exchanging tokens for valuable educational resources. With STEM TAS, users can be confident in the authenticity of the educational resources they purchase, as they are all vetted and verified before being listed on the platform.

Overall, STEM TAS represents a groundbreaking solution in the field of STEM education, providing an innovative way for users to exchange tokens for valuable educational resources.
In addition to the features mentioned above, STEM TAS also includes the following functionalities:

Tokens are sold to the highest bidder: STEM TAS operates on a traditional English auction model, where the token is sold to the highest bidder at the end of the auction period.
A reserve price, set by the seller, must be met: The seller can set a reserve price for the token, which is the minimum price at which they are willing to sell the token.
Bids below the reserve price are not allowed: Bids that are below the reserve price will be rejected by the platform.
Bids are disclosed: All bids are transparent and visible to all users of the platform.
The names of the seller and bidders are disclosed for each token auction: The identity of both the seller and bidders are disclosed for each auction, adding transparency and accountability to the process.
Anonymous bidding is not permitted: All bidders must disclose their identity to participate in the auction.
Auctions close 15 minutes after the first bid is received: Once the first bid is received, the auction period begins, and all bids must be submitted within a specified timeframe. The auction period lasts for 15 minutes, and if no further bids are received, the highest bidder wins the token.
On-chain auction history (optional): The STEM TAS platform also provides the option for users to view on-chain auction history, allowing them to track previous auctions and analyze market trends.
Overall, STEM TAS offers a robust and transparent token auction platform for STEM educational resources, providing an efficient and secure way for buyers and sellers to exchange tokens for valuable resources



# Quick-Start 

If you want to see the full completed contract go ahead and clone and build this repo using 
```=bash
git clone https://github.com/Binwakil/nft-archiverse.git 
yarn build
```
Now that you've cloned and built the contract we can try a few things. 

## Mint An NFT

Once you've created your near wallet go ahead and login to your wallet with your cli and follow the on-screen prompts

```=bash
near login
```

Once your logged in you have to deploy the contract. Make a subaccount with the name of your choosing 

```=bash 
near create-account nft-example.your-account.testnet --masterAccount your-account.testnet --initialBalance 10
near create-account market-example.your-account.testnet --masterAccount your-account.testnet --initialBalance 10
```

After you've created your sub account deploy the contract to that sub account, set this variable to your sub account name

```=bash
NFT_CONTRACT_ID=nft-example.your-account.testnet
MARKET_CONTRACT_ID=nft-example.your-account.testnet
MAIN_ACCOUNT=your-account.testnet
```

Verify your new variable has the correct value
```=bash
echo $NFT_CONTRACT_ID
echo $MARKET_CONTRACT_ID
echo $MAIN_ACCOUNT
```


### Deploy Your Contract
```=bash
near deploy --accountId $NFT_CONTRACT_ID --wasmFile out/main.wasm
near deploy --accountId $MARKET_CONTRACT_ID --wasmFile out/market.wasm
```

### Initialize Your Contract 

```=bash
near call $NFT_CONTRACT_ID new_default_meta '{"owner_id": "'$NFT_CONTRACT_ID'"}' --accountId $NFT_CONTRACT_ID
```

### View Contracts Meta Data

```=bash
near view $NFT_CONTRACT_ID nft_metadata
```
### Minting Token

```bash=
near call $NFT_CONTRACT_ID nft_mint '{"token_id": "token-1", "metadata": {"title": "My Non Fungible Team Token", "description": "The Team Most Certainly Goes :)", "media": "https://bafybeiftczwrtyr3k7a2k4vutd3amkwsmaqyhrdzlhvpt33dyjivufqusq.ipfs.dweb.link/goteam-gif.gif"}, "receiver_id": "'$MAIN_ACCOUNT'"}' --accountId $MAIN_ACCOUNT --amount 0.1
```

After you've minted the token go to wallet.testnet.near.org to `your-account.testnet` and look in the collections tab and check out your new sample NFT! 



## View NFT Information

After you've minted your NFT you can make a view call to get a response containing the `token_id` `owner_id` and the `metadata`

```bash=
near view $NFT_CONTRACT_ID nft_token '{"token_id": "token-1"}'
```

## Transfering NFTs

To transfer an NFT go ahead and make another [testnet wallet account](https://wallet.testnet.near.org).

Then run the following
```bash=
MAIN_ACCOUNT_2=your-second-wallet-account.testnet
```

Verify the correct variable names with this

```=bash
echo $NFT_CONTRACT_ID

echo $MAIN_ACCOUNT

echo $MAIN_ACCOUNT_2
```

To initiate the transfer..

```bash=
near call $NFT_CONTRACT_ID nft_transfer '{"receiver_id": "$MAIN_ACCOUNT_2", "token_id": "token-1", "memo": "Go Team :)"}' --accountId $MAIN_ACCOUNT --depositYocto 1
```

In this call you are depositing 1 yoctoNEAR for security and so that the user will be redirected to the NEAR wallet.
