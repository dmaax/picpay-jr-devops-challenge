FROM golang:1.16
WORKDIR /go/src/github.com/PicPay/picpay-jr-devops-challenge/services/go
ADD . /go/src/github.com/PicPay/picpay-jr-devops-challenge/services/go

EXPOSE 8080

# Download dependencies
RUN ["go","mod","init"]
RUN ["go","get","github.com/go-redis/redis"]
RUN ["go","get","github.com/rs/cors"]

CMD ["go","run","main.go"]