# JSON

<pre class="language-sql"><code class="lang-sql"><strong>SELECT * FROM ethereum.core.fact_transactions 
</strong>WHERE tx_hash = '0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3'</code></pre>

Or, specifically:

```sql
SELECT tx_json FROM ethereum.core.fact_transactions 
WHERE tx_hash = '0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3'
```

<details>

<summary><code>tx_json</code>, in all its glory</summary>

{% code lineNumbers="true" %}
```json
{
  "block_hash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
  "block_number": 15347344,
  "chain_id": "0x1",
  "condition": null,
  "creates": null,
  "from": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
  "gas": 216462,
  "gas_price": 20104768496,
  "hash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
  "input": "0x5ae401dc0000000000000000000000000000000000000000000000000000000062fa89f4000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000014000000000000000000000000000000000000000000000000000000000000000c44659a4940000000000000000000000006b175474e89094c44da98b954eedeac495271d0f00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000062fa8e8f000000000000000000000000000000000000000000000000000000000000001c60bbdc441be9dd60a7733f03ab506f792a02d5faca90a5cc2aed83d44b37b42a447b8ab992b168865a36074418c8b3e3d28699a03ac38e1a1f788c71887e408d0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e404e45aaf0000000000000000000000006b175474e89094c44da98b954eedeac495271d0f000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc200000000000000000000000000000000000000000000000000000000000001f400000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325000000000000000000000000000000000000000000000002b5e3af16b1880000000000000000000000000000000000000000000000000000005c463bbbce28ee000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "max_fee_per_gas": 22667295396,
  "max_priority_fee_per_gas": 1500000000,
  "nonce": "0x47",
  "public_key": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
  "r": "0x4c952208248e1905d5b8753ace7823931c2972c637b4a7404d755b9926309712",
  "receipt": {
    "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
    "blockNumber": "0xea2e90",
    "cumulativeGasUsed": "0xb82802",
    "effectiveGasPrice": "0x4ae566bf0",
    "from": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
    "gasUsed": "0x2a09b",
    "logs": [
      {
        "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
        "blockNumber": "0xea2e90",
        "data": "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "decoded": {
          "contractName": "Dai",
          "eventName": "Approval",
          "inputs": {
            "owner": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
            "spender": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
            "value": "115792089237316195423570985008687907853269984665640564039457584007913129639935"
          },
          "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:0"
        },
        "logIndex": "0x214",
        "removed": false,
        "topics": [
          "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
          "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325",
          "0x00000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc45"
        ],
        "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
        "transactionIndex": "0x70"
      },
      {
        "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
        "blockNumber": "0xea2e90",
        "data": "0x000000000000000000000000000000000000000000000000005ce7f12faf2cf3",
        "decoded": {
          "contractName": "WETH9",
          "eventName": "Transfer",
          "inputs": {
            "from": "0x60594a405d53811d3bc4766596efd80fd545a270",
            "to": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
            "value": "26150720930524403"
          },
          "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:1"
        },
        "logIndex": "0x215",
        "removed": false,
        "topics": [
          "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
          "0x00000000000000000000000060594a405d53811d3bc4766596efd80fd545a270",
          "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325"
        ],
        "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
        "transactionIndex": "0x70"
      },
      {
        "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
        "blockNumber": "0xea2e90",
        "data": "0x000000000000000000000000000000000000000000000002b5e3af16b1880000",
        "decoded": {
          "contractName": "Dai",
          "eventName": "Transfer",
          "inputs": {
            "from": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
            "to": "0x60594a405d53811d3bc4766596efd80fd545a270",
            "value": "50000000000000000000"
          },
          "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:2"
        },
        "logIndex": "0x216",
        "removed": false,
        "topics": [
          "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
          "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325",
          "0x00000000000000000000000060594a405d53811d3bc4766596efd80fd545a270"
        ],
        "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
        "transactionIndex": "0x70"
      },
      {
        "address": "0x60594a405d53811d3bc4766596efd80fd545a270",
        "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
        "blockNumber": "0xea2e90",
        "data": "0x000000000000000000000000000000000000000000000002b5e3af16b1880000ffffffffffffffffffffffffffffffffffffffffffffffffffa3180ed050d30d000000000000000000000000000000000000000005db234f5c90909b6c4e4cde000000000000000000000000000000000000000000000df1a18577ae80815c37fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffed8da",
        "decoded": {
          "eventName": "Swap",
          "inputs": {
            "amount0": "50000000000000000000",
            "amount1": "-26150720930524403",
            "liquidity": "65848068439472762608695",
            "recipient": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
            "sender": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
            "sqrtPriceX96": "1812346550392001438868720862",
            "tick": "-75558"
          },
          "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:3"
        },
        "logIndex": "0x217",
        "removed": false,
        "topics": [
          "0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67",
          "0x00000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc45",
          "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325"
        ],
        "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
        "transactionIndex": "0x70"
      }
    ],
    "logsBloom": "0x00000000000000000000000020000000000000000000000000000040000000000000000000000000000000000000000002000020080020000000000000200000000000000000000800000008000000000000000100000000000000000000000010000000000000000000080000000000000000000000002000000010000800000000000000000008000800000000000000000000000000000000000000000000020000000000000000000000000000000000080000000000000000000000000000000002000000020000000000000000000002000000000000000100000000000010200000000000000000000000080000000000000000000000000000000000",
    "status": "0x1",
    "to": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
    "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
    "transactionIndex": "0x70",
    "type": "0x2"
  },
  "s": "0x7f1e05aea5f8da9da5a64d07b9635b06ad99fcb86cdfb47aa7ca5e8d8f0a0911",
  "standard_v": null,
  "to": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
  "transaction_index": 112,
  "v": "0x1",
  "value": 0
}
```
{% endcode %}

</details>

The `tx_json` data item, or object, is the meat of the transaction. It contains the output data from the activity we just performed on Uniswap. This ugly mess is a goldmine of information.

The primary thing to notice is the structure of this block (which is much easier to read when formatted properly. Copy the contents of the column over to something like[ https://jsonformatter.org/](https://jsonformatter.org/) for sanity's sake.)

## Dictionary Structure

i.e. it is a data structure made up of key-value pairs, separated by commas. We can see, right away, something familiar in `"block_number": 15347344` where the **key** = block number and **value** = 15347344.

If we want to _get_ this data, we can select it using the key in one of the following ways, using the **key**:

* `tx_json['block_number']` or `tx_json:block_number`

```sql
SELECT
  tx_json:block_number as block_number,
  tx_json['block_number'] as also_block_number
FROM ethereum.core.fact_transactions 
LIMIT 1;
```

Objects can hold other objects, thus the value of one key can be a key-value pair itself. (This is another reason to use a formatter, as nested objects will be easy to spot due to the extra indentation.)

```json
{
  "key1": "value1",
  "key2": {
    "nested_key": "nested_value"
  }
}
```

So, if the above was the value for `tx_json`, then&#x20;

`tx_json:key1` = `value1`&#x20;

while `tx_json:key2` = `{"nested_key": "nested_value"}`,&#x20;

and, ultimately, `tx_json:key2:nested_key` = `"nested_value"`.

So, back to the goal at hand - getting to logs.

Refer back to the json above, or in your editor in another window. On line 24, we see the word logs. It's quite indented, so we can tell that logs is within receipts, which is within the `tx_json` itself. To access and return just the logs part of the full `tx_json`, we simple need to ask for it by name:`tx_json:receipt:logs`.

```sql
SELECT
  tx_json:receipt:logs
FROM ethereum.core.fact_transactions 
WHERE tx_hash = '0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3';
```

<details>

<summary>logs, up close</summary>

```json
[
  {
    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
    "blockNumber": "0xea2e90",
    "data": "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
    "decoded": {
      "contractName": "Dai",
      "eventName": "Approval",
      "inputs": {
        "owner": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "spender": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
        "value": "115792089237316195423570985008687907853269984665640564039457584007913129639935"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:0"
    },
    "logIndex": "0x214",
    "removed": false,
    "topics": [
      "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
      "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325",
      "0x00000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc45"
    ],
    "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
    "transactionIndex": "0x70"
  },
  {
    "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
    "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
    "blockNumber": "0xea2e90",
    "data": "0x000000000000000000000000000000000000000000000000005ce7f12faf2cf3",
    "decoded": {
      "contractName": "WETH9",
      "eventName": "Transfer",
      "inputs": {
        "from": "0x60594a405d53811d3bc4766596efd80fd545a270",
        "to": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "value": "26150720930524403"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:1"
    },
    "logIndex": "0x215",
    "removed": false,
    "topics": [
      "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
      "0x00000000000000000000000060594a405d53811d3bc4766596efd80fd545a270",
      "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325"
    ],
    "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
    "transactionIndex": "0x70"
  },
  {
    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
    "blockNumber": "0xea2e90",
    "data": "0x000000000000000000000000000000000000000000000002b5e3af16b1880000",
    "decoded": {
      "contractName": "Dai",
      "eventName": "Transfer",
      "inputs": {
        "from": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "to": "0x60594a405d53811d3bc4766596efd80fd545a270",
        "value": "50000000000000000000"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:2"
    },
    "logIndex": "0x216",
    "removed": false,
    "topics": [
      "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
      "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325",
      "0x00000000000000000000000060594a405d53811d3bc4766596efd80fd545a270"
    ],
    "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
    "transactionIndex": "0x70"
  },
  {
    "address": "0x60594a405d53811d3bc4766596efd80fd545a270",
    "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
    "blockNumber": "0xea2e90",
    "data": "0x000000000000000000000000000000000000000000000002b5e3af16b1880000ffffffffffffffffffffffffffffffffffffffffffffffffffa3180ed050d30d000000000000000000000000000000000000000005db234f5c90909b6c4e4cde000000000000000000000000000000000000000000000df1a18577ae80815c37fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffed8da",
    "decoded": {
      "eventName": "Swap",
      "inputs": {
        "amount0": "50000000000000000000",
        "amount1": "-26150720930524403",
        "liquidity": "65848068439472762608695",
        "recipient": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "sender": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
        "sqrtPriceX96": "1812346550392001438868720862",
        "tick": "-75558"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:3"
    },
    "logIndex": "0x217",
    "removed": false,
    "topics": [
      "0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67",
      "0x00000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc45",
      "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325"
    ],
    "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
    "transactionIndex": "0x70"
  }
]
```

</details>

Looking closely, there's a slightly different syntax here, looks like logs is using `[` instead of `{` - does that matter?

Yes, absolutely.

## Arrays

Take a look at the logs [on Etherscan](https://etherscan.io/tx/0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3#eventlog). Notice there are multiple (4) logs for this lone transaction. So, to represent these events, they are stored in a list - also known as an **array**.

Arrays are denoted with square brackets, and contain _0 or more_ pieces of data (yes, they can be empty).

`a = ["the", "fat", "cat"]` is an array `a` full of 3 strings. We can access each of these elements by their [index](https://docs.snowflake.com/en/sql-reference/data-types-semistructured.html#accessing-elements-of-an-array-by-index-or-by-slice), which starts at **0**. How do we index into the array? With more square brackets.

\-> `a[0] = "the"`, `a[1] = "fat"`

So, going back to our `logs`, to access each log we simply index the array. Looking at either the full JSON or at Etherscan, we can see that, within logs, there's a `decoded` object containing an `eventName` "Swap" - as we're looking to identify Uniswap v3 swap actions, this is probably a good place to look.

<details>

<summary>The Swap Log</summary>

{% code lineNumbers="true" %}
```json
tx_json:receipt:logs[3] = 
  {
    "address": "0x60594a405d53811d3bc4766596efd80fd545a270",
    "blockHash": "0xb82ff1bb63c41f68f84400329912dff52f3167b5eb2a41c7d7f962fc1eeefe70",
    "blockNumber": "0xea2e90",
    "data": "0x000000000000000000000000000000000000000000000002b5e3af16b1880000ffffffffffffffffffffffffffffffffffffffffffffffffffa3180ed050d30d000000000000000000000000000000000000000005db234f5c90909b6c4e4cde000000000000000000000000000000000000000000000df1a18577ae80815c37fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffed8da",
    "decoded": {
      "eventName": "Swap",
      "inputs": {
        "amount0": "50000000000000000000",
        "amount1": "-26150720930524403",
        "liquidity": "65848068439472762608695",
        "recipient": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "sender": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
        "sqrtPriceX96": "1812346550392001438868720862",
        "tick": "-75558"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:3"
    },
    "logIndex": "0x217",
    "removed": false,
    "topics": [
      "0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67",
      "0x00000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc45",
      "0x00000000000000000000000004ae8c108743167c7457073ba8c1571fd5d56325"
    ],
    "transactionHash": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3",
    "transactionIndex": "0x70"
  }
```
{% endcode %}

</details>

Now, we can't assume that the 4th (index 3) log is _always_ the `Swap` event and, further, we might want information, like token info, in the other logs. There is a way to flatten a list, like logs, and easily access each piece of the array. However, there's an even easier way to get to each log and the decoded information within.

Remember `ethereum.core.fact_event_logs`?

## fact\_event\_logs

```sql
SELECT * FROM ethereum.core.fact_event_logs 
WHERE tx_hash = '0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3'
ORDER BY event_index;
```

Here we have the 4 logs from our swap, easily cleaned up and in order. So, why did we waste time learning about dictionaries and arrays? JSON is a very prevalent data format and knowing how to traverse the nested structure is absolutely essential. Even in the flattened `fact_event_logs` we have a column, `event_inputs`, with JSON data that needs extracting to be useful.

Take a look at the `event_inputs` from the Swap log (aka `WHERE event_name = 'Swap'`):

```json
{
  "amount0": "50000000000000000000",
  "amount1": "-26150720930524403",
  "liquidity": "65848068439472762608695",
  "recipient": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
  "sender": "0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45",
  "sqrtPriceX96": "1812346550392001438868720862",
  "tick": "-75558"
}
```

If we want to build up some metrics or analysis on Uniswap v3 pools, we need to be able to access this data.

Looking in depth at the logs, we can start to build answers to questions like: How do we identify the tokens in this swap and which one is `amount0` vs `amount1`? Which pool is the address using? And once we can do this on an individual level, it's a breeze to compute over a large set.

Recall, in the raw `logs` there were other pieces of interest. In the `Transfer` events, Dai and WETH are identified and we can match the amounts with `amount0` and `amount1` in the swap.

Curious about the pool info? As they say, _follow the money._ Let's take a look at a piece of the two `Transfer` logs, up close.

```json
[
  {
    ...
    "decoded": {
      "contractName": "WETH9",
      "eventName": "Transfer",
      "inputs": {
        "from": "0x60594a405d53811d3bc4766596efd80fd545a270",
        "to": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "value": "26150720930524403"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:1"
  },
    ...
  {
    "decoded": {
      "contractName": "Dai",
      "eventName": "Transfer",
      "inputs": {
        "from": "0x04ae8c108743167c7457073ba8c1571fd5d56325",
        "to": "0x60594a405d53811d3bc4766596efd80fd545a270",
        "value": "50000000000000000000"
      },
      "logKey": "0x32844e66c41bf08a8c3d249d1dd53a404831bc486e094342dc4b79ae9c7aa8d3:2"
    },
  ...
  }
}
```

Recall this was a swap of 50 DAI to .02615 WETH and we see that reflected in the logs with the respective `to` / `from` addresses. DAI is leaving the swapper's wallet in the direction of the pool, while WETH is being transferred in the opposite direction. We can confirm, or identify, the pool by checking Etherscan or the labels table.

```sql
SELECT * FROM ethereum.core.dim_labels
WHERE address = '0x60594a405d53811d3bc4766596efd80fd545a270';
```

Now that we know how to access the data nested in these JSON objects, the only thing left to do is apply the data transforming techniques learned in the previous SQL lessons! We can use CTEs to build temporary result sets from the logs, aggregate activity over a long period of time, and bring in identifying info from contracts and labels tables with joins.

Using all of these ideas and techniques together takes time and practice! Fortunately, there's some prompts to try this all out on the next page.

## Dive Deeper

{% embed url="https://docs.snowflake.com/en/sql-reference/data-types-semistructured.html" %}
