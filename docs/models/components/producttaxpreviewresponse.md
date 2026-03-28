# ProductTaxPreviewResponse

Tax preview result for a product price.


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `Subtotal`                                                              | `int64`                                                                 | :heavy_check_mark:                                                      | N/A                                                                     |
| `TaxAmount`                                                             | `int64`                                                                 | :heavy_check_mark:                                                      | N/A                                                                     |
| `Total`                                                                 | `int64`                                                                 | :heavy_check_mark:                                                      | N/A                                                                     |
| `Currency`                                                              | `string`                                                                | :heavy_check_mark:                                                      | N/A                                                                     |
| `Quantity`                                                              | `int64`                                                                 | :heavy_check_mark:                                                      | N/A                                                                     |
| `TaxRate`                                                               | [*components.TaxRatePreview](../../models/components/taxratepreview.md) | :heavy_minus_sign:                                                      | N/A                                                                     |
| `TaxabilityReason`                                                      | `*string`                                                               | :heavy_minus_sign:                                                      | N/A                                                                     |