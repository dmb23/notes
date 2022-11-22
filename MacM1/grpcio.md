# Install ``grpcio` on a M1

I require the flags

```
export GRPC_PYTHON_BUILD_SYSTEM_OPENSSL=1
export GRPC_PYTHON_BUILD_SYSTEM_ZLIB=1

CFLAGS="-I/opt/homebrew/opt/openssl/include"
LDFLAGS="-L/opt/homebrew/opt/openssl/lib"
```

to build grpcio on my Mac. In addition that probably requires that I installed openssl via brew.
