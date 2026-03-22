# set up a base image
FROM golang:1.22-alpine AS build

# set up workdir
WORKDIR /usr/src/app

COPY . .
# run the commands that you would run locally on machine
RUN go mod download

# compile the application
RUN go build -o product-catalog .


# ====================================
# set up minimal base image like alpine with no shared libraries minimizing the security threats
FROM alpine AS release

# copy the resources needed
WORKDIR /usr/src/app

COPY ./products ./products

# copy the binary from build
COPY --from=build /usr/src/app/product-catalog .

# expose ports 
# set environmental variables
ENV PRODUCT_CATALOG_PORT=8088

# set cmd or entry point to run the final command
ENTRYPOINT ["./product-catalog"]
