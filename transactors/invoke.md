---
html: invoke.html
parent: transaction-types.html
blurb: Trigger a hook.
labels:
  - HooksV3
---
# Import
[[Source]](https://github.com/ripple/rippled/blob/master/src/ripple/app/tx/impl/Invoke.cpp "Source")

_(Added by the [Hooks amendment][].)_

An Invoke transaction is used to trigger and interact with a hook.

## Example Import JSON

```json
{
  "TransactionType": "Invoke",
  "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
  "Destination" : "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo"
}
```


| Field            | JSON Type           | [Internal Type][] | Description     |
|:-----------------|:--------------------|:------------------|:----------------|
| `Blob`           | String              | Blob              | Hex value that can represent anything and be read in the hook. |
| `Destination`    | String              | AccountID         | (Optional) The unique address of the hook account that you want to invoke. |
| `DestinationTag` | String              | UInt32            | (Optional) Arbitrary tag that identifies the reason for the Invoke, or which recipient to interact with. |
| `InvoiceID`      | String              | Hash256           | (Optional) Arbitrary 256-bit hash representing a specific reason or identifier for this Invoke. |

## Error Cases

- If the `Blob` is not a hex value then the transaction fails with the result code `temMALFORMED`,
- If the `Blob` is larger than 128*1024 then the transaction fails with the result code `temMALFORMED`,
- If the `Destination` is the sender of the transaction, the transaction fails with the result code `temREDUNDANT`.
- If the `Destination` [account](accounts.html) does not exist in the ledger, the transaction fails with the result code `tecNO_DST`.
- If the `Destination` account has the `RequireDest` flag enabled but the transaction does not include a `DestinationTag` field, the transaction fails with the result code `tecDST_TAG_NEEDED`.

## Notes

- TicketSequence is not available on `Invoke`