---
html: import.html
parent: transaction-types.html
blurb: Initialize accounts and key management.
labels:
  - HooksV3
---
# Import
[[Source]](https://github.com/ripple/rippled/blob/master/src/ripple/app/tx/impl/Import.cpp "Source")

_(Added by the [Import amendment][].)_

Import is a new transaction which accepts an XPOP from the Ripple testnet chain (network_id=1) and provides account synchronisation.

## Example Import JSON

```json
{
  "TransactionType": "Import",
  "Sequence": 0,
  "Fee": "0",
  "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
  "Blob" : "DEADBEEF"
}
```


| Field            | JSON Type           | [Internal Type][] | Description     |
|:-----------------|:--------------------|:------------------|:----------------|
| `Blob`           | String              | Blob              | Hex value representing an XPOP |
| `Issuer`         | String              | AccountID         | (Optional) Address that can be used inside the Hook. |
| `Destination`    | String              | AccountID         | (Optional) Address that can be used inside the Hook. |

## Error Cases

- If the account is Non Activated then the `Sequence` must be 0 and the `Fee` must also be 0
- If the account is Activated then the `Sequence` and the `Fee` are calculated the standard method.
- If the `Issuer` field is present then the `Fee` must be calculated using the standard method.

## Notes

- If the inner transaction is `AccountSet` no existing or transaction flags will be transfered to the network.
- If the inner transaction is `SetRegularKey` and the `RegularKey` field is omitted, then the `lsfDisableMaster` will be set on the account.
- If the inner transaction is `SetRegularKey` then the `lsfPasswordSpent` will be set on the account.
- If the inner transaction is `SignersListSet` and the signers are not active on the network, the transaction will still result in `tesSUCCESS` and the `Fee` will still be minted however the signers list will NOT be set.