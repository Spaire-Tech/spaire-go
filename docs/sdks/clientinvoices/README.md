# ClientInvoices

## Overview

### Available Operations

* [ListClientInvoices](#listclientinvoices) - List Client Invoices
* [CreateClientInvoice](#createclientinvoice) - Create Client Invoice
* [PreviewClientInvoicePdf](#previewclientinvoicepdf) - Preview Client Invoice PDF
* [GetClientInvoice](#getclientinvoice) - Get Client Invoice
* [DownloadClientInvoicePdf](#downloadclientinvoicepdf) - Download Client Invoice PDF
* [FinalizeClientInvoice](#finalizeclientinvoice) - Finalize Client Invoice
* [SendClientInvoice](#sendclientinvoice) - Send Client Invoice
* [MarkClientInvoicePaid](#markclientinvoicepaid) - Mark Client Invoice as Paid
* [VoidClientInvoice](#voidclientinvoice) - Void Client Invoice

## ListClientInvoices

List client invoices for the authenticated organization.

**Scopes**: `client_invoices:read`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:list_client_invoices" method="get" path="/v1/client-invoices/" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.ListClientInvoices(ctx, spairego.Pointer[int64](1), spairego.Pointer[int64](10), nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListResourceClientInvoiceSchema != nil {
        for {
            // handle items

            res, err = res.Next()

            if err != nil {
                // handle error
            }

            if res == nil {
                break
            }
        }
    }
}
```

### Parameters

| Parameter                                                                                                                                                               | Type                                                                                                                                                                    | Required                                                                                                                                                                | Description                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                                                                                   | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                   | :heavy_check_mark:                                                                                                                                                      | The context to use for the request.                                                                                                                                     |
| `page`                                                                                                                                                                  | `*int64`                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                      | Page number, defaults to 1.                                                                                                                                             |
| `limit`                                                                                                                                                                 | `*int64`                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                      | Size of a page, defaults to 10. Maximum is 100.                                                                                                                         |
| `sorting`                                                                                                                                                               | [][components.ClientInvoiceSortProperty](../../models/components/clientinvoicesortproperty.md)                                                                          | :heavy_minus_sign:                                                                                                                                                      | Sorting criterion. Several criteria can be used simultaneously and will be applied in order. Add a minus sign `-` before the criteria name to sort by descending order. |
| `opts`                                                                                                                                                                  | [][operations.Option](../../models/operations/option.md)                                                                                                                | :heavy_minus_sign:                                                                                                                                                      | The options for this request.                                                                                                                                           |

### Response

**[*operations.ClientInvoicesListClientInvoicesResponse](../../models/operations/clientinvoiceslistclientinvoicesresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## CreateClientInvoice

Create a new draft client invoice. Tax is calculated automatically.

**Scopes**: `client_invoices:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:create_client_invoice" method="post" path="/v1/client-invoices/" -->
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

    res, err := s.ClientInvoices.CreateClientInvoice(ctx, components.ClientInvoiceCreate{
        CustomerID: "<value>",
        Currency: "Gibraltar Pound",
        LineItems: []components.ClientInvoiceLineItemCreate{},
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ClientInvoiceSchema != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [components.ClientInvoiceCreate](../../models/components/clientinvoicecreate.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.ClientInvoicesCreateClientInvoiceResponse](../../models/operations/clientinvoicescreateclientinvoiceresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## PreviewClientInvoicePdf

Generate a real PDF preview from form data without creating anything.

**Scopes**: `client_invoices:read`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:preview_client_invoice_pdf" method="post" path="/v1/client-invoices/preview-pdf" -->
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

    res, err := s.ClientInvoices.PreviewClientInvoicePdf(ctx, components.ClientInvoicePreviewRequest{
        OrganizationID: "<value>",
        Currency: "Baht",
        LineItems: []components.ClientInvoiceLineItemPreview{},
    })
    if err != nil {
        log.Fatal(err)
    }
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                            | [context.Context](https://pkg.go.dev/context#Context)                                            | :heavy_check_mark:                                                                               | The context to use for the request.                                                              |
| `request`                                                                                        | [components.ClientInvoicePreviewRequest](../../models/components/clientinvoicepreviewrequest.md) | :heavy_check_mark:                                                                               | The request object to use for the request.                                                       |
| `opts`                                                                                           | [][operations.Option](../../models/operations/option.md)                                         | :heavy_minus_sign:                                                                               | The options for this request.                                                                    |

### Response

**[*operations.ClientInvoicesPreviewClientInvoicePdfResponse](../../models/operations/clientinvoicespreviewclientinvoicepdfresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## GetClientInvoice

Get a client invoice by ID.

**Scopes**: `client_invoices:read`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:get_client_invoice" method="get" path="/v1/client-invoices/{id}" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.GetClientInvoice(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.ClientInvoiceSchema != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ClientInvoicesGetClientInvoiceResponse](../../models/operations/clientinvoicesgetclientinvoiceresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## DownloadClientInvoicePdf

Generate and download a PDF for the given client invoice.

**Scopes**: `client_invoices:read`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:download_client_invoice_pdf" method="get" path="/v1/client-invoices/{id}/pdf" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.DownloadClientInvoicePdf(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ClientInvoicesDownloadClientInvoicePdfResponse](../../models/operations/clientinvoicesdownloadclientinvoicepdfresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## FinalizeClientInvoice

Finalize a draft invoice (generates PDF) without sending the email.
Status moves from draft → open. Use this to preview the invoice before sending.

**Scopes**: `client_invoices:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:finalize_client_invoice" method="post" path="/v1/client-invoices/{id}/finalize" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.FinalizeClientInvoice(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.ClientInvoiceSchema != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ClientInvoicesFinalizeClientInvoiceResponse](../../models/operations/clientinvoicesfinalizeclientinvoiceresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## SendClientInvoice

Finalize and send a draft invoice to the customer via Stripe.

**Scopes**: `client_invoices:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:send_client_invoice" method="post" path="/v1/client-invoices/{id}/send" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.SendClientInvoice(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.ClientInvoiceSchema != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ClientInvoicesSendClientInvoiceResponse](../../models/operations/clientinvoicessendclientinvoiceresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## MarkClientInvoicePaid

Mark a draft or open invoice as paid manually without going through Stripe.

**Scopes**: `client_invoices:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:mark_client_invoice_paid" method="post" path="/v1/client-invoices/{id}/mark-paid" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.MarkClientInvoicePaid(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.ClientInvoiceSchema != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ClientInvoicesMarkClientInvoicePaidResponse](../../models/operations/clientinvoicesmarkclientinvoicepaidresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## VoidClientInvoice

Void a draft or open invoice.

**Scopes**: `client_invoices:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="client_invoices:void_client_invoice" method="post" path="/v1/client-invoices/{id}/void" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.ClientInvoices.VoidClientInvoice(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.ClientInvoiceSchema != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `id`                                                     | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ClientInvoicesVoidClientInvoiceResponse](../../models/operations/clientinvoicesvoidclientinvoiceresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |