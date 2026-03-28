# ClientInvoiceLineItemSchema


## Fields

| Field                                      | Type                                       | Required                                   | Description                                |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| `ID`                                       | `string`                                   | :heavy_check_mark:                         | The ID of the object.                      |
| `CreatedAt`                                | [time.Time](https://pkg.go.dev/time#Time)  | :heavy_check_mark:                         | Creation timestamp of the object.          |
| `ModifiedAt`                               | [*time.Time](https://pkg.go.dev/time#Time) | :heavy_check_mark:                         | Last modification timestamp of the object. |
| `ClientInvoiceID`                          | `string`                                   | :heavy_check_mark:                         | N/A                                        |
| `StripeInvoiceItemID`                      | `*string`                                  | :heavy_check_mark:                         | N/A                                        |
| `Description`                              | `string`                                   | :heavy_check_mark:                         | N/A                                        |
| `Quantity`                                 | `int64`                                    | :heavy_check_mark:                         | N/A                                        |
| `UnitAmount`                               | `int64`                                    | :heavy_check_mark:                         | N/A                                        |
| `Currency`                                 | `string`                                   | :heavy_check_mark:                         | N/A                                        |
| `Amount`                                   | `int64`                                    | :heavy_check_mark:                         | N/A                                        |
| `TaxAmount`                                | `int64`                                    | :heavy_check_mark:                         | N/A                                        |