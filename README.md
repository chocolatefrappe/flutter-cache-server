## About
This is a cache server for the Flutter SDK archive. It is designed to be deployed in a private network to cache Flutter SDK releases to reduce the load on the public servers and speed up the download process.

## Usage

The cache server listens on port `36081` by default. You can change the port by setting the `PORT` environment variable.

To run the cache server, you can use the following command:
```bash
docker run -p 36081:36081 -v /path/to/cache:/var/lib/flutter -d chocolatefrappe/flutter-cache-server:main
```

or via Docker Compose:

```yaml
services:
  flutter-cache-server:
    image: chocolatefrappe/flutter-cache-server:main
    ports:
      - mode: ingress
        target: 36081
        published: 36081
        protocol: tcp
    volumes:
      - type: volume
        source: flutter-cache
        target: /var/lib/flutter
    stop_grace_period: 1m
    restart: always
volumes:
  flutter-cache:
```
