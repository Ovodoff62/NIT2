# Step 1. Clone repository
Execute command

    git clone https://github.com/NibiruChain/cw-nibiru

# Step 2. Upload contract on chain
Execute command (Change your wallet name if needed)

    nibid tx wasm store $HOME/cw-nibiru/artifacts-cw-plus/cw20_base.wasm --from wallet --gas-adjustment 1.2 --gas auto  --fees 80000unibi  -y

Copy txhash and paste-search it in Explorer. In LOGS find code_id. Copy that and put it into variable with command (Put your Code_id instead of YOUR_CODE_ID):

    id=YOUR_CODE_ID

[OPTIONAL] Check Wasm contract 

    nibid query wasm code-info $id


# Step 3. Instantiate Contract:
Setup variable $init (Change name, symbol. Instead of YOUR_WALLET_ADDRESS write your wallet address)

    init='{"name":"Ovodoff","symbol":"OFFC","decimals":2,"initial_balances":[{"address":"YOUR_WALLET_ADDRESS","amount":"100000"}],"mint":{"minter":"YOUR_WALLET_ADDRESS"},"marketing":{}}'

sending tx ( Change  label and wallet name if needed)

    nibid tx wasm instantiate $id $init --from wallet --label "YOUR_LABEL_NAME" --gas-adjustment 1.2 --gas auto  --fees 100000unibi --no-admin -y


Copy txhash and paste-search it in Explorer. In LOGS find Instantiate Contract Address. Copy that and put it into variable with command (Put your Contract Address instead of YOUR_CONTRACT_ADDRESS):

    contract=YOUR_CONTRACT_ADDRESS


# [OPTIONAL] STEP 4. Check Token balance in your Wallet

Create Variable $BALANCE_QUERY (Set your wallet address instead of YOUR_WALLET_ADDRESS)

    BALANCE_QUERY='{"balance": {"address": "YOUR_WALLET_ADDRESS"}}'

Execute tx:

    nibid query wasm contract-state smart $contract "$BALANCE_QUERY" --output json

You should see the amount of tokens that you minted


# STEP 5. Broadcasting {ExecuteContract}
Here we gonna send some tokens to another wallet (Receiver wallet)
Create $transfer variable (Change RECEIVER_WALLET_ADRESS to your receiver wallet address)

    transfer='{"transfer":{"recipient":"RECEIVER_WALLET_ADRESS","amount":"100"}}'

Execute tx:

    nibid tx wasm execute $contract $transfer --gas-adjustment 1.2 --gas auto --fees 10000unibi --from wallet -y

# [OPTIONAL] STEP 6. Check Token balance in Receiver Wallet
Rewrite Variable $BALANCE_QUERY (Set receiver wallet address instead of RECEIVER_WALLET_ADDRESS)

    BALANCE_QUERY='{"balance": {"address": "RECEIVER_WALLET_ADDRESS"}}'

Execute tx:
    nibid query wasm contract-state smart $contract "$BALANCE_QUERY" --output json

# Video version of the guide:
[<iframe width="640" height="360" src="https://www.youtube.com/embed/dKt3AdahyW4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>](https://www.youtube.com/watch?v=dKt3AdahyW4)
