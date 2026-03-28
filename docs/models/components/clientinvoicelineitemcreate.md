# ClientInvoiceLineItemCreate


## Fields

| Field                                                  | Type                                                   | Required                                               | Description                                            |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| `Description`                                          | `string`                                               | :heavy_check_mark:                                     | Line item description shown on the invoice.            |
| `Quantity`                                             | `*int64`                                               | :heavy_minus_sign:                                     | Quantity.                                              |
| `UnitAmount`                                           | `int64`                                                | :heavy_check_mark:                                     | Unit price in the smallest currency unit (e.g. cents). |