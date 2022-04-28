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

    "github.com/segmentio/analytics-go"
)

func main() {
    // Instantiates a client to send messages to the dreamdata API.
    client := analytics.New(os.Getenv("DREAMDATA_WRITE_KEY"))

    // Enqueues a track event that will be sent asynchronously.
    client.Enqueue(analytics.Track{
        UserId: "test-user",
        Event:  "test-snippet",
    })

    // Flushes any queued messages and closes the client.
    client.Close()
}
```

## License

The library is released under the [MIT license](License.md).
