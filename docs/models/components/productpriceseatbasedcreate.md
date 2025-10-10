# ProductPriceSeatBasedCreate

Schema to create a seat-based price.


## Fields

| Field                                             | Type                                              | Required                                          | Description                                       |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| `AmountType`                                      | *string*                                          | :heavy_check_mark:                                | N/A                                               |
| `PriceCurrency`                                   | **string*                                         | :heavy_minus_sign:                                | The currency. Currently, only `usd` is supported. |
| `PricePerSeat`                                    | *int64*                                           | :heavy_check_mark:                                | The price per seat in cents.                      |