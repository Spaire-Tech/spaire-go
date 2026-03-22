<!-- Start SDK Example Usage [usage] -->
```go
package main

import (
	"context"
	spairego "app.spairehq.com/go"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := spairego.New(
		spairego.WithSecurity(os.Getenv("SPAIRE_ACCESS_TOKEN")),
	)

	res, err := s.Organizations.List(ctx, nil, spairego.Pointer[int64](1), spairego.Pointer[int64](10), nil)
	if err != nil {
		log.Fatal(err)
	}
	if res.ListResourceOrganization != nil {
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
<!-- End SDK Example Usage [usage] -->