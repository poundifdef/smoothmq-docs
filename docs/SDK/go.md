# Go

``` go 
package main

import (
    "context"

    "github.com/aws/aws-sdk-go-v2/aws"
    "github.com/aws/aws-sdk-go-v2/config"
    "github.com/aws/aws-sdk-go-v2/service/sqs"
)

func main() {
    cfg, err := config.LoadDefaultConfig(context.TODO())
    sqsClient := sqs.NewFromConfig(cfg, func(o *sqs.Options) {
        o.BaseEndpoint = aws.String("http://localhost:3001")
    })
}

```