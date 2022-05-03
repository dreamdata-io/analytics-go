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

	var err error

	err = c.Enqueue(analytics.Identify{
		UserId: "019mr8mf4r",
		Traits: analytics.NewTraits().
			SetEmail("user@dreamdata.io").
			SetName("user").
			SetAge(25),
	})
	if err != nil {
		// do something with your err
	}

	err = c.Enqueue(analytics.Track{
		UserId: "019mr8mf4r",
		Event:  "Song Played",
		Properties: analytics.NewProperties().
			SetName("My song").
			Set("artist", "My artist"),
	})
	if err != nil {
		// do something with your err
	}

	err = c.Enqueue(analytics.Identify{
		UserId: "971mj8mk7p",
		Traits: analytics.NewTraits().
			SetEmail("user2@dreamdata.io").
			SetName("user2").
			SetAge(26),
	})
	if err != nil {
		// do something with your err
	}

	err = c.Enqueue(analytics.Track{
		UserId: "971mj8mk7p",
		Event:  "Song Played",
		Properties: analytics.NewProperties().
			SetName("My song").
			Set("artist", "My artist"),
	})
	if err != nil {
		// do something with your err
	}

    // Flushes any queued messages and closes the client.
    client.Close()
}
```

## Disclaimer
Even though this repo is forked from [Segment repo](https://github.com/segmentio/analytics-go), it might not be compatible with Segment's latest version. We never want anyone to use this fork to attempt to talk to Segment, by mistake.


## License
The library is released under the [MIT license](License.md).
