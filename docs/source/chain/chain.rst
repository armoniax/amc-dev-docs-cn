APIs for chain
==============

1.  get_info

2.  get_activated_protocol_features

3.  get_block

4.  get_account

5.  get_code

6.  get_code_hash

7.  get_abi

8.  get_raw_code_and_abi

9.  get_raw_abi

10. get_table_rows

11. get_table_by_scope

12. get_currency_balance

13. get_currency_stats

14. get_producers

15. get_producer_schedule

16. get_scheduled_transactions

17. abi_json_to_bin

18. abi_bin_to_json

19. get_required_keys

20. get_transaction_id

21. push_block

22. push_transaction

23. push_transactions

24. send_transaction

.. code:: shell

   curl -X GET --url http://127.0.0.1:8888/v1/chain/get_info
   curl -X GET --url http://127.0.0.1:8888/v1/chain/get_activated_protocol_features
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_block -d '{"block_num_or_id":"100"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_account -d '{"account_name":"amax"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_code -d '{"account_name":"amax","code_as_wasm":true}' #must be true only
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_code_hash -d '{"account_name":"amax"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_abi -d '{"account_name":"amax"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_raw_code_and_abi -d '{"account_name":"amax"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_raw_abi -d '{"account_name":"amax"}'
   # command "amcli get scope amax.token" used to check contract tables and data scope
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_table_rows -d '{"code":"amax.token","table":"accounts","scope":"amax.stake"}'
   # code is the name of the contract to return table data for
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_table_by_scope -d '{"code":"amax.token"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_currency_balance -d '{"code":"amax.token","account":"amax","symbol":"AMAX"}'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_producers -d '{"limit":"21","lower_bound":"1"}'
   curl -X GET --url http://127.0.0.1:8888/v1/chain/get_producer_schedule
   curl -X GET --url http://127.0.0.1:8888/v1/chain/get_scheduled_transactions
   #after you sign the output below, you can push it.
   curl -X POST --url http://127.0.0.1:8888/v1/chain/abi_json_to_bin -d '{
     "code": "amax.token",
     "action":"transfer",
     "args": {"from":"amax","to":"producerman","quantity":"1000 AMAX","memo":"used for push transaction"}
   }'
   #decode binargs
   curl -X POST --url http://127.0.0.1:8888/v1/chain/abi_bin_to_json -d '{
     "code": "amax.token",
     "action":"transfer",
     "binargs": "0000000000d08d3400a69157219de8ade80300000000000000414d4158000000197573656420666f722070757368207472616e73616374696f6e"
   }'
   #extract required keys needed to sign a transaction from transaction
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_required_keys -d '{
   "transaction": {
             "expiration": "2022-04-14T14:24:46",
             "ref_block_num": 68,
             "ref_block_prefix": 3877461440,
             "max_net_usage_words": 0,
             "max_cpu_usage_ms": 0,
             "delay_sec": 0,
             "context_free_actions": [],
             "actions": [{
                 "account": "amax",
                 "name": "newaccount",
                 "authorization": [{
                     "actor": "amax",
                     "permission": "active"
                   }
                 ],
                 "data": "0000000000d08d340080822663d08d34010000000100034d5db3cdc19c42cf43efdab37f7088566d1726b1a199d9ab43eab75fd502353101000000010000000100034d5db3cdc19c42cf43efdab37f7088566d1726b1a199d9ab43eab75fd502353101000000"
               }
             ]
           },
       "available_keys": [
       "AM7RJjx45D9SRstBdgJS5ooop2YLGgwbQKgvpgCGugWfUNvn2VGx",
       "AM6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
       "AM6W6L85BmwoWx2Cv44LHd8yJFkEcwpWnAAnog64aaFvXLkKriLw"]
   }'
   or 2 parameters transaction type object available_keys array
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_required_keys -d '{
    "transaction": {
             "expiration": "2022-04-14T14:24:46",
             "ref_block_num": 68,
             "ref_block_prefix": 3877461440,
             "max_net_usage_words": 0,
             "max_cpu_usage_ms": 0,
             "delay_sec": 0,
             "context_free_actions": [],
             "actions": [{
                 "account": "amax",
                 "name": "newaccount",
                 "authorization": [{
                     "actor": "amax",
                     "permission": "active"
                   }
                 ],
                 "data": {
                   "creator": "amax",
                   "name": "amax.stake",
                   "owner": {
                     "threshold": 1,
                     "keys": [{
                         "key": "AM7RJjx45D9SRstBdgJS5ooop2YLGgwbQKgvpgCGugWfUNvn2VGx",
                         "weight": 1
                       }
                     ],
                     "accounts": [],
                     "waits": []
                   },
                   "active": {
                     "threshold": 1,
                     "keys": [{
                         "key": "AM7RJjx45D9SRstBdgJS5ooop2YLGgwbQKgvpgCGugWfUNvn2VGx",
                         "weight": 1
                       }
                     ],
                     "accounts": [],
                     "waits": []
                   }
                 },
                 "hex_data": "0000000000d08d340080822663d08d34010000000100034d5db3cdc19c42cf43efdab37f7088566d1726b1a199d9ab43eab75fd502353101000000010000000100034d5db3cdc19c42cf43efdab37f7088566d1726b1a199d9ab43eab75fd502353101000000"
               }
             ]
           },
       "available_keys": [
       "AM7RJjx45D9SRstBdgJS5ooop2YLGgwbQKgvpgCGugWfUNvn2VGx",
       "AM6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
       "AM6W6L85BmwoWx2Cv44LHd8yJFkEcwpWnAAnog64aaFvXLkKriLw"]
   }'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/get_transaction_id -d '{
    "transaction": {
             "expiration": "2022-04-14T14:24:46",
             "ref_block_num": 68,
             "ref_block_prefix": 3877461440,
             "max_net_usage_words": 0,
             "max_cpu_usage_ms": 0,
             "delay_sec": 0,
             "context_free_actions": [],
             "actions": [{
                 "account": "amax",
                 "name": "newaccount",
                 "authorization": [{
                     "actor": "amax",
                     "permission": "active"
                   }
                 ],
                 "data": {
                   "creator": "amax",
                   "name": "amax.stake",
                   "owner": {
                     "threshold": 1,
                     "keys": [{
                         "key": "AM7RJjx45D9SRstBdgJS5ooop2YLGgwbQKgvpgCGugWfUNvn2VGx",
                         "weight": 1
                       }
                     ],
                     "accounts": [],
                     "waits": []
                   },
                   "active": {
                     "threshold": 1,
                     "keys": [{
                         "key": "AM7RJjx45D9SRstBdgJS5ooop2YLGgwbQKgvpgCGugWfUNvn2VGx",
                         "weight": 1
                       }
                     ],
                     "accounts": [],
                     "waits": []
                   }
                 },
                 "hex_data": "0000000000d08d340080822663d08d34010000000100034d5db3cdc19c42cf43efdab37f7088566d1726b1a199d9ab43eab75fd502353101000000010000000100034d5db3cdc19c42cf43efdab37f7088566d1726b1a199d9ab43eab75fd502353101000000"
               }
             ]
           }
   }'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/push_block -d '{
     "block": {
     "timestamp": "2022-04-14T17:11:54.000",
     "producer": "producerman",
     "confirmed": 0,
     "previous": "0000270f5239d32acdec89a3db99c8151c6f4a59502df08230cc1e5cb0e5c2b4",
     "transaction_mroot": "0000000000000000000000000000000000000000000000000000000000000000",
     "action_mroot": "1fade41b29f958e556a8b0222da76a6d037dbb01967f06f91f24cb6173510a3c",
     "schedule_version": 1,
     "new_producers": null,
     "producer_signature": "SIG_K1_K1aBbbX2qj6i7cYNjfn9LN8eL61kDGAW2qMnKtCPuLJyzih4x8VSdeSZFZ2f9MEJ5PDqtEoBwryanwTWxmK5DxUpM9Gpcs",
     "transactions": [],
     "id": "0000271028b5a308b69da160d98d592df392c258ca5906d8eb6b27edf213eb29",
     "block_num": 10000,
     "ref_block_prefix": 1621204406
   }
   }'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/push_transaction -d '{
   "signatures": [   "SIG_K1_KA4Duu9UdXQqGFiAw8pGUWWUSkZuxcZHwikDRR4o51DG7SsNvCJiTPK5VmsNr9WFSHAX8j3DJMEmfhzd5cdm5EQR6ce8TV"],
   "compression": "none",
   "packed_context_free_data": "",
   "context_free_data": [],
   "packed_trx": "ac2e58624200c1ac8d5f00000000010000000000d08d3400409e9a2264b89a010000000000d08d3400000000a8ed3232660000000000d08d3400945ad25cd08d3401000000010003aecc021147501039c10d636e71f0f1ed5c50ccf63c942411baa9f285746af1190100000001000000010003aecc021147501039c10d636e71f0f1ed5c50ccf63c942411baa9f285746af1190100000000"
   }'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/push_transactions -d '[{
   }]'
   curl -X POST --url http://127.0.0.1:8888/v1/chain/send_transaction -d '{
   }'
