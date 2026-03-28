# Benefits

## Overview

### Available Operations

* [List](#list) - List Benefits
* [Create](#create) - Create Benefit
* [Get](#get) - Get Benefit
* [Delete](#delete) - Delete Benefit
* [Update](#update) - Update Benefit
* [Grants](#grants) - List Benefit Grants

## List

List benefits.

**Scopes**: `benefits:read` `benefits:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="benefits:list" method="get" path="/v1/benefits/" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"app.spairehq.com/go/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.Benefits.List(ctx, operations.BenefitsListRequest{
        OrganizationID: spairego.Pointer(operations.CreateQueryParamOrganizationIDFilterStr(
            "1dbfc517-0bbf-4301-9ba8-555ca42b9737",
        )),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListResourceBenefit != nil {
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

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [operations.BenefitsListRequest](../../models/operations/benefitslistrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.BenefitsListResponse](../../models/operations/benefitslistresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## Create

Create a benefit.

**Scopes**: `benefits:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="benefits:create" method="post" path="/v1/benefits/" -->
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

    res, err := s.Benefits.Create(ctx, components.CreateBenefitCreateLicenseKeys(
        components.BenefitLicenseKeysCreate{
            Description: "mature emergent at outside arrogantly gadzooks zealous equatorial notwithstanding",
            OrganizationID: spairego.Pointer("1dbfc517-0bbf-4301-9ba8-555ca42b9737"),
            Properties: components.BenefitLicenseKeysCreateProperties{},
        },
    ))
    if err != nil {
        log.Fatal(err)
    }
    if res.Benefit != nil {
        switch res.Benefit.Type {
            case components.BenefitUnionTypeBenefitCustom:
                // res.Benefit.BenefitCustom is populated
            case components.BenefitUnionTypeBenefitDiscord:
                // res.Benefit.BenefitDiscord is populated
            case components.BenefitUnionTypeBenefitGitHubRepository:
                // res.Benefit.BenefitGitHubRepository is populated
            case components.BenefitUnionTypeBenefitDownloadables:
                // res.Benefit.BenefitDownloadables is populated
            case components.BenefitUnionTypeBenefitLicenseKeys:
                // res.Benefit.BenefitLicenseKeys is populated
            case components.BenefitUnionTypeBenefitMeterCredit:
                // res.Benefit.BenefitMeterCredit is populated
        }

    }
}
```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `ctx`                                                                | [context.Context](https://pkg.go.dev/context#Context)                | :heavy_check_mark:                                                   | The context to use for the request.                                  |
| `request`                                                            | [components.BenefitCreate](../../models/components/benefitcreate.md) | :heavy_check_mark:                                                   | The request object to use for the request.                           |
| `opts`                                                               | [][operations.Option](../../models/operations/option.md)             | :heavy_minus_sign:                                                   | The options for this request.                                        |

### Response

**[*operations.BenefitsCreateResponse](../../models/operations/benefitscreateresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## Get

Get a benefit by ID.

**Scopes**: `benefits:read` `benefits:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="benefits:get" method="get" path="/v1/benefits/{id}" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"log"
	"app.spairehq.com/go/models/components"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.Benefits.Get(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.Benefit != nil {
        switch res.Benefit.Type {
            case components.BenefitUnionTypeBenefitCustom:
                // res.Benefit.BenefitCustom is populated
            case components.BenefitUnionTypeBenefitDiscord:
                // res.Benefit.BenefitDiscord is populated
            case components.BenefitUnionTypeBenefitGitHubRepository:
                // res.Benefit.BenefitGitHubRepository is populated
            case components.BenefitUnionTypeBenefitDownloadables:
                // res.Benefit.BenefitDownloadables is populated
            case components.BenefitUnionTypeBenefitLicenseKeys:
                // res.Benefit.BenefitLicenseKeys is populated
            case components.BenefitUnionTypeBenefitMeterCredit:
                // res.Benefit.BenefitMeterCredit is populated
        }

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

**[*operations.BenefitsGetResponse](../../models/operations/benefitsgetresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.ResourceNotFound    | 404                           | application/json              |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## Delete

Delete a benefit.

> [!WARNING]
> Every grants associated with the benefit will be revoked.
> Users will lose access to the benefit.

**Scopes**: `benefits:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="benefits:delete" method="delete" path="/v1/benefits/{id}" -->
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

    res, err := s.Benefits.Delete(ctx, "<value>")
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

**[*operations.BenefitsDeleteResponse](../../models/operations/benefitsdeleteresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.NotPermitted        | 403                           | application/json              |
| apierrors.ResourceNotFound    | 404                           | application/json              |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## Update

Update a benefit.

**Scopes**: `benefits:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="benefits:update" method="patch" path="/v1/benefits/{id}" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"app.spairehq.com/go/models/components"
	"app.spairehq.com/go/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.Benefits.Update(ctx, "<value>", operations.CreateBenefitsUpdateBenefitUpdateBenefitCustomUpdate(
        components.BenefitCustomUpdate{},
    ))
    if err != nil {
        log.Fatal(err)
    }
    if res.Benefit != nil {
        switch res.Benefit.Type {
            case components.BenefitUnionTypeBenefitCustom:
                // res.Benefit.BenefitCustom is populated
            case components.BenefitUnionTypeBenefitDiscord:
                // res.Benefit.BenefitDiscord is populated
            case components.BenefitUnionTypeBenefitGitHubRepository:
                // res.Benefit.BenefitGitHubRepository is populated
            case components.BenefitUnionTypeBenefitDownloadables:
                // res.Benefit.BenefitDownloadables is populated
            case components.BenefitUnionTypeBenefitLicenseKeys:
                // res.Benefit.BenefitLicenseKeys is populated
            case components.BenefitUnionTypeBenefitMeterCredit:
                // res.Benefit.BenefitMeterCredit is populated
        }

    }
}
```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                            | [context.Context](https://pkg.go.dev/context#Context)                                            | :heavy_check_mark:                                                                               | The context to use for the request.                                                              |
| `id`                                                                                             | `string`                                                                                         | :heavy_check_mark:                                                                               | N/A                                                                                              |
| `requestBody`                                                                                    | [operations.BenefitsUpdateBenefitUpdate](../../models/operations/benefitsupdatebenefitupdate.md) | :heavy_check_mark:                                                                               | N/A                                                                                              |
| `opts`                                                                                           | [][operations.Option](../../models/operations/option.md)                                         | :heavy_minus_sign:                                                                               | The options for this request.                                                                    |

### Response

**[*operations.BenefitsUpdateResponse](../../models/operations/benefitsupdateresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.ResourceNotFound    | 404                           | application/json              |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |

## Grants

List the individual grants for a benefit.

It's especially useful to check if a user has been granted a benefit.

**Scopes**: `benefits:read` `benefits:write`

### Example Usage

<!-- UsageSnippet language="go" operationID="benefits:grants" method="get" path="/v1/benefits/{id}/grants" -->
```go
package main

import(
	"context"
	"os"
	spairego "app.spairehq.com/go"
	"app.spairehq.com/go/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := spairego.New(
        spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
    )

    res, err := s.Benefits.Grants(ctx, operations.BenefitsGrantsRequest{
        ID: "<value>",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListResourceBenefitGrant != nil {
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

| Parameter                                                                            | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `ctx`                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                | :heavy_check_mark:                                                                   | The context to use for the request.                                                  |
| `request`                                                                            | [operations.BenefitsGrantsRequest](../../models/operations/benefitsgrantsrequest.md) | :heavy_check_mark:                                                                   | The request object to use for the request.                                           |
| `opts`                                                                               | [][operations.Option](../../models/operations/option.md)                             | :heavy_minus_sign:                                                                   | The options for this request.                                                        |

### Response

**[*operations.BenefitsGrantsResponse](../../models/operations/benefitsgrantsresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.ResourceNotFound    | 404                           | application/json              |
| apierrors.HTTPValidationError | 422                           | application/json              |
| apierrors.APIError            | 4XX, 5XX                      | \*/\*                         |