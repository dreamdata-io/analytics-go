# analytics-go

Dreamdata analytics client for Go.

## Installation

The package can be simply installed via go get, we recommend that you use a
package version management system like the Go vendor directory or a tool like
Godep to avoid issues related to API breaking changes introduced between major
versions of the library.

To install it in the GOPATH:
```
go get https://github.com/dreamdata-io/analytics-go
```

## Usage

```go
package main

import (
    "os"
	"golang.org/x/sync/errgroup"

    "github.com/dreamdata-io/analytics-go"
)

func main() {
    // Instantiates a client to send messages to the dreamdata API.
    client := analytics.New(os.Getenv("DREAMDATA_WRITE_KEY"))

	errGroup := new(errgroup.Group)

	errGroup.Go(c.Enqueue(analytics.Identify{
		UserId: "019mr8mf4r",
		Traits: map[string]interface{}{
			"email": "user@dreamdata.io",
			"name":  "user",
			"age":   25,
		},
	}))

	errGroup.Go(c.Enqueue(analytics.Track{
		UserId: "019mr8mf4r",
		Event:  "Song Played",
		Properties: map[string]interface{}{
			"name":   "My song",
			"artist": "My artist",
		},
	}))

	errGroup(c.Enqueue(analytics.Identify{
		UserId: "971mj8mk7p",
		Traits: map[string]interface{}{
			"email": "user2@dreamdata.io",
			"name":  "user2",
			"age":   26,
		},
	}))

	errGroup(c.Enqueue(analytics.Track{
		UserId: "971mj8mk7p",
		Event:  "Song Played",
		Properties: map[string]interface{}{
			"name":   "My song",
			"artist": "My artist",
		},
	}))

	if err := errGroup.Wait(); err == nil {
		fmt.Printf("Successfully enqueued messages")
	}

    // Flushes any queued messages and closes the client.
    client.Close()
}
```

## Disclaimer
Even though this repo is forked from [Segment repo](https://github.com/segmentio/analytics-go), it might not be compatible with Segment's latest version. We never want anyone to use this fork to attempt to talk to Segment, by mistake.


## License
The library is released under the [MIT license](License.md).
