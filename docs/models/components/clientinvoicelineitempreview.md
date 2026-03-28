# ClientInvoiceLineItemPreview

Relaxed line item for preview — allows zero amounts for in-progress editing.


## Fields

| Field                                        | Type                                         | Required                                     | Description                                  |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| `Description`                                | `*string`                                    | :heavy_minus_sign:                           | Line item description.                       |
| `Quantity`                                   | `*int64`                                     | :heavy_minus_sign:                           | Quantity.                                    |
| `UnitAmount`                                 | `*int64`                                     | :heavy_minus_sign:                           | Unit price in cents (0 allowed for preview). |