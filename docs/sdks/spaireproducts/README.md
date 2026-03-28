# Products.Products

## Overview

### Available Operations

* [PreviewTax](#previewtax) - Preview Tax

## PreviewTax

Estimate tax for a product price given a customer location and quantity.
Uses the configured tax provider (Stripe Tax) to calculate applicable taxes.

**Scopes**: `products:read` `products:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="products:products:preview_tax" method="post" path="/v1/products/tax-preview" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"app.spairehq.com/go/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.Products.Products.PreviewTax(ctx, components.ProductTaxPreviewRequest{
        Amount: 428098,
        Currency: "Kina",
        Country: "Guatemala",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ProductTaxPreviewResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                  | Type                                                                                       | Required                                                                                   | Description                                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `ctx`                                                                                      | [context.Context](https://pkg.go.dev/context#Context)                                      | :heavy_check_mark:                                                                         | The context to use for the request.                                                        |
| `request`                                                                                  | [components.ProductTaxPreviewRequest](../../models/components/producttaxpreviewrequest.md) | :heavy_check_mark:                                                                         | The request object to use for the request.                                                 |
| `opts`                                                                                     | [][operations.Option](../../models/operations/option.md)                                   | :heavy_minus_sign:                                                                         | The options for this request.                                                              |

### Response

**[*operations.ProductsProductsPreviewTaxResponse](../../models/operations/productsproductspreviewtaxresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |