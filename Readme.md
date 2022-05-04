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

## Batches
Every method you call does not result in an HTTP request, but is queued in memory instead. Messages are then flushed in batch in the background, which allows for much faster operation.

By default, our library will flush:

- Every 20 messages (controlled by `Config.BatchSize`).
- If 5 seconds has passed since the last flush (controlled by `Config.Interval`)
- There is a maximum of 500KB per batch request and 32KB per call.

If you don’t want to batch messages, you can turn batching off by setting the BatchSize option to 1, like so:
```go
c, err := analytics.NewWithConfig(os.Getenv("DREAMDATA_WRITE_KEY"), analytics.Config{BatchSize: 1})
```

## Disclaimer
Even though this repo is forked from [Segment repo](https://github.com/segmentio/analytics-go), it might not be compatible with Segment's latest version. We never want anyone to use this fork to attempt to talk to Segment, by mistake.


## License
The library is released under the [MIT license](License.md).
