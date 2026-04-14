How to use this smart contract on CNHO Stables? Check it out.

 ./cnho_stables init admin --chain-id cnho_stables --home=.  

 ./cnho_stables keys add alice --keyring-backend test --home=.

 ./cnho_stables add-genesis-account $( ./cnho_stables keys show alice -a --keyring-backend test --home=.) 100000000stake,100000000000ucnho --home=.

 ./cnho_stables gentx alice 80000000stake --chain-id cnho_stables --keyring-backend test --home=.


 ./cnho_stables collect-gentxs --home=.         

 ./cnho_stables start --home=.    


 ./cnho_stables tx gov submit-proposal proposal.json --from alice --chain-id cnho_stables  --gas auto --fees 1000stake -y --home=. --keyring-backend test --broadcast-mode block

 ./cnho_stables tx gov submit-proposal proposal.json --from alice --chain-id cnho_stables --gas auto --fees 1000stake -y --home=. --keyring-backend test


 ./cnho_stables tx gov vote 1 yes  --from alice --chain-id cnho_stables --fees 1000stake -y --home=. --keyring-backend test


 ./cnho_stables q gov votes 1 --home=.   

 ./cnho_stables q gov proposals --home=.   


 ./cnho_stables q gov params --home=.

./cnho_stable tx tokenfactory create-denom MINE --from alice --chain-id cnho_stables --keyring-backend test --fees 1000stake --broadcast-mode block --home=.

 ./cnho_stable keys add admin --recover --home=. --keyring-backend test

./cnho_stable tx bank send alice  cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4 100000stake --chain-id cnho_stables --keyring-backend test --fees 1000stake --broadcast-mode block --home=. -y
./cnho_stable tx bank send alice  cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4 10000000ucnho --chain-id cnho_stables --keyring-backend test --fees 1000stake --broadcast-mode block --home=. -y

 MINE --from admin --chain-id cnho_stables --keyring-backend test --fees 1000stake --broadcast-mode block --home=. -y
 ./cnho_stable query tokenfactory denoms-from-creator cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4
./cnho_stable query bank denom-metadata

 ./cnho_stable tx tokenfactory mint 100000factory/cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4/MINE --from admin --chain-id cnho_stables --keyring-backend test --fees 1000stake --broadcast-mode block --home=. -y


./cnho_stable query bank balances cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4
./cnho_stable query bank balances cnho1537p58jx7j52uqwr2emshd04e3s56a5450qkan

./cnho_stable tx bank send cnho1g6mesf2lhm5e32jsff9v37z8kypz8ue8mkphlp cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4 100000stake --chain-id cnho_stables --keyring-backend test --fees 1000stake --broadcast-mode block --home=. -y

./cnho_stable tx bank send cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4 cnho1537p58jx7j52uqwr2emshd04e3s56a5450qkan 100000factory/cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4/MINE --chain-id cnho_stables --from admin --keyring-backend test --fees 1000stake --broadcast-mode block --home=. -y

factory.wasm   1
pair.wasm  2
pair_stable.wasm  3
router.wasm  4
token.wasm  5 
whitelist.wasm 6
generator.wasm 7
staking.wasm 8
maker.wasm 9
native_coin_registry.wasm  10
vesting.wasm  11
oracle.wasm  12
pair_concentrated.wasm  13

 ./cnho_stable query wasm codes


 ./cnho_stable tx wasm store pair_concentrated.wasm   --from alice --chain-id cnho_stables --gas auto --fees 1000stake -y --keyring-backend test --home=. --broadcast-mode block

 ./cnho_stable tx wasm instantiate 10 '{
"owner": "cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4"
}' \
--from admin \
--label "coin-registry" \
--no-admin \
--gas auto --fees 1000stake \
--chain-id cnho_stables \
--broadcast-mode block \
-y \
--home=. \
--keyring-backend test\

./cnho_stable tx wasm execute cnho1jn8qmdda5m6f6fqu9qv46rt7ajhklg40ukpqchkejcvy8x7w26cqqyhkln '{
  "add": {
    "native_coins": [
      ["ucnho", 6],
      ["stake", 6],
      ["factory/cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4/MINE", 6]
    ]
  }
}' \
--from admin \
--chain-id cnho_stables \
--gas auto --fees 2000stake \
--broadcast-mode block \
-y --home=. --keyring-backend test

./cnho_stable query wasm contract-state smart cnho1jn8qmdda5m6f6fqu9qv46rt7ajhklg40ukpqchkejcvy8x7w26cqqyhkln '{
  "native_tokens": {}
}'


./cnho_stable tx wasm instantiate 1 '{
  "owner": "cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4",
  "pair_configs": [
    {
      "code_id": 2,
      "pair_type": { "xyk": {} },
      "total_fee_bps": 30,
      "maker_fee_bps": 5,
      "is_disabled": false,
      "is_generator_disabled": true
    }
  ],
  "token_code_id": 5,
  "fee_address": "cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4",
  "generator_address": null,
  "whitelist_code_id": 6,
  "coin_registry_address": "cnho1jn8qmdda5m6f6fqu9qv46rt7ajhklg40ukpqchkejcvy8x7w26cqqyhkln"
}' \
--from admin \
--label "astroport-factory" \
--no-admin \
--gas 2000000 \
--fees 2000stake \
--chain-id cnho_stables \
--broadcast-mode block \
-y \
--home=. \
--keyring-backend test

cnho1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrsdx5lfr

./cnho_stable tx wasm execute cnho1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrsdx5lfr '{
  "create_pair": {             
    "pair_type": { "xyk": {} },
    "asset_infos": [                           
      { "native_token": { "denom": "stake" } },
      { "native_token": { "denom": "ucnho" } }
    ],                 
    "init_params": null
  } 
}' --from alice --gas auto --fees 2000stake --chain-id cnho_stables -y --home=. --keyring-backend test --broadcast-mode block

./cnho_stable query wasm contract-state smart cnho1xr3rq8yvd7qplsw5yx90ftsr2zdhg4e9z60h5duusgxpv72hud3sjpj5dw '{
  "pair": {}
}'

    contract_addr: cnho1xr3rq8yvd7qplsw5yx90ftsr2zdhg4e9z60h5duusgxpv72hud3sjpj5dw
    liquidity_token: cnho1436kxs0w2es6xlqpp9rd35e3d0cjnw4sv8j3a7483sgks29jqwgs35efza

    contract_addr: cnho1hulx7cgvpfcvg83wk5h96sedqgn72n026w6nl47uht554xhvj9nswm4l0g
    liquidity_token: cnho1j08452mqwadp8xu25kn9rleyl2gufgfjnv0sn8dvynynakkjukcqjg2cfs

./cnho_stable tx wasm execute cnho1xr3rq8yvd7qplsw5yx90ftsr2zdhg4e9z60h5duusgxpv72hud3sjpj5dw '{
"provide_liquidity": {
"assets": [
{
"info": { "native_token": { "denom": "stake" } },
"amount": "1000000"
},
{
"info": { "native_token": { "denom": "ucnho" } },
"amount": "1000000"
}
],
"slippage_tolerance": "0.01",
"auto_stake": false,
"receiver": null
}
}' --amount 1000000stake,1000000ucnho --from alice --gas auto --fees 2000stake --chain-id cnho_stables -y --home=. --keyring-backend test --broadcast-mode block

./cnho_stable tx wasm execute cnho1hulx7cgvpfcvg83wk5h96sedqgn72n026w6nl47uht554xhvj9nswm4l0g '{
"provide_liquidity": {
"assets": [
{
"info": { "native_token": { "denom": "factory/cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4/MINE" } },
"amount": "100000"
},
{
"info": { "native_token": { "denom": "ucnho" } },
"amount": "1000000"
}
],
"slippage_tolerance": "0.01",
"auto_stake": false,
"receiver": null
}
}' --amount 100000factory/cnho18x42dnqv4z2mxdw6pq5p4h5aj49vnqytq6k0h4/MINE,1000000ucnho --from alice --gas auto --fees 2000stake --chain-id cnho_stables -y --home=. --keyring-backend test --broadcast-mode block

./cnho_stable query wasm contract-state smart cnho1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrsdx5lfr '{ "pairs": {} }'

./cnho_stable query wasm contract-state smart cnho1xr3rq8yvd7qplsw5yx90ftsr2zdhg4e9z60h5duusgxpv72hud3sjpj5dw '{
  "simulation": {
    "offer_asset": {
      "info": { "native_token": { "denom": "stake" } },
      "amount": "10000"
    }
  }
}'

./cnho_stable query wasm contract-state smart cnho1hulx7cgvpfcvg83wk5h96sedqgn72n026w6nl47uht554xhvj9nswm4l0g '{
  "simulation": {
    "offer_asset": {
      "info": { "native_token": { "denom": "ucnho" } },
      "amount": "10000"
    }
  }
}'


./cnho_stable tx wasm execute cnho1xr3rq8yvd7qplsw5yx90ftsr2zdhg4e9z60h5duusgxpv72hud3sjpj5dw '{
  "swap": {
    "offer_asset": {
      "info": { "native_token": { "denom": "stake" } },
      "amount": "10000"
    },
    "max_spread": "0.5"
  }
}' \
--amount 10000stake \
--from alice \
--gas auto --fees 2000stake \
--chain-id cnho_stables \
--broadcast-mode block \
-y --home=. --keyring-backend test

./cnho_stable tx wasm execute cnho1hulx7cgvpfcvg83wk5h96sedqgn72n026w6nl47uht554xhvj9nswm4l0g '{
  "swap": {
    "offer_asset": {
      "info": { "native_token": { "denom": “ucnho” } },
      "amount": "10000"
    },
    "max_spread": "0.5"
  }
}' \
--amount 10000ucnho \
--from alice \
--gas auto --fees 2000stake \
--chain-id cnho_stables \
--broadcast-mode block \
-y --home=. --keyring-backend test



./cnho_stable query wasm contract-state smart cnho1pvrwmjuusn9wh34j7y520g8gumuy9xtl3gvprlljfdpwju3x7ucs56mp49 '{
  "all_accounts": {}
}'

./cnho_stable query wasm contract-state smart cnho1j08452mqwadp8xu25kn9rleyl2gufgfjnv0sn8dvynynakkjukcqjg2cfs '{
"balance": {
"address": "cnho1537p58jx7j52uqwr2emshd04e3s56a5450qkan"
}
}'



./cnho_stable tx wasm execute cnho1j08452mqwadp8xu25kn9rleyl2gufgfjnv0sn8dvynynakkjukcqjg2cfs '{
"send": {
"contract": "cnho1hulx7cgvpfcvg83wk5h96sedqgn72n026w6nl47uht554xhvj9nswm4l0g",
"amount": "2162",
"msg": "eyJ3aXRoZHJhd19saXF1aWRpdHkiOnt9fQ=="
}
}' \
--from alice \
--gas auto \
--fees 2000stake \
--chain-id cnho_stables \
--broadcast-mode block \
-y \
--home=. \
--keyring-backend test



