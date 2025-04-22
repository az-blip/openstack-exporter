# Builder stage
FROM golang:1.22 AS builder
WORKDIR /
COPY . .
RUN go mod download && CGO_ENABLED=0 go build -o /openstack-exporter .

# Final image
FROM gcr.io/distroless/base:nonroot as openstack-exporter
COPY --from=builder /app/openstack-exporter .
COPY --from=build /openstack-exporter /bin/openstack-exporter
EXPOSE 9180
ENTRYPOINT ["openstack-exporter"]
