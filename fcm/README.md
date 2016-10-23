# FCM

A Firebase Cloud Messaging client written in Go. For more information checkout
[their docs](https://firebase.google.com/docs/cloud-messaging/).

## Installation

```bash
go get -u github.com/zabawaba99/firego/fcm
```

## Usage

```go
package main

import (
	"log"

	"github.com/zabawaba99/firego/fcm"
)

func main() {
	client := fcm.New("my-api-key", nil)

	msg := fcm.Message{
		RegistrationIDs: []string{"foo", "bar"},
		Data: &fcm.Data{
			"hello": "world",
		},
	}
	resp, err := client.Send(msg)
	if err != nil {
		log.Fatalf("Error sending msg %s", err)
	}

	if resp.Failure != 0 {
		log.Fatal("All these reuslts failed to send %s", resp.Failures())
	}
}
```