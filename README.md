# Unofficial Anthropic SDK in Go

This project provides an unofficial Go SDK for Anthropic, a A next-generation AI assistant for your tasks, no matter the scale. The SDK makes it easy to interact with the Anthropic API in Go applications. For more information about Anthropic, including API documentation, visit the official [Anthropic documentation.](https://console.anthropic.com/docs)

[![GoDoc](https://godoc.org/github.com/madebywelch/anthropic-go?status.svg)](https://pkg.go.dev/github.com/madebywelch/anthropic-go)

## Installation

You can install the Anthropic SDK in Go using go get:

```go
go get github.com/madebywelch/anthropic-go
```

## Usage

To use the Anthropic SDK, you'll need to initialize a client and make requests to the Anthropic API. Here's an example of initializing a client and performing a search:

```go
import (
    "github.com/madebywelch/anthropic-go/pkg/anthropic"
    "fmt"
)

func main() {
	client, err := anthropic.NewClient(apiKey)

	if err != nil {
		panic(err)
	}

	response, err := client.Complete(&CompletionRequest{
		Prompt:            "Human: Hello, how are you?",
		Model:             anthropic.ClaudeV1,
		MaxTokensToSample: 100,
		StopSequences:     []string{"\r", "Human:"},
	})

    if err != nil {
        panic(err)
    }

    fmt.Printf("claude says: %v\n", response.Completion)
}
```

## Automatic Retries

This unofficial Anthropic API client SDK supports automatic retries for requests that fail or return unexpected status codes. By using the `WithMaxRetries` and `WithRetryDelay` options, you can configure the client to automatically retry failed requests up to a specified number of times with a specified delay between attempts. This can help improve the reliability of your API calls, particularly in case of temporary network issues or server-side errors.

**Example:**

```go
client, err := anthropic.NewClient(
	apiKey,
	clientID,
	anthropic.WithMaxRetries(5),               // Retry up to 5 times
	anthropic.WithRetryDelay(3 * time.Second), // 3-second delay between retries
)
```

## Contributing

Contributions to this project are welcome. To contribute, follow these steps:

- Fork this repository
- Create a new branch (`git checkout -b feature/my-new-feature`)
- Commit your changes (`git commit -am 'Add some feature'`)
- Push the branch (`git push origin feature/my-new-feature`)
- Create a new pull request

## License

This project is licensed under the Apache License, Version 2.0 - see the [LICENSE](LICENSE) file for details.