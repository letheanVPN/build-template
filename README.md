# Lethean builder (currenlty just a base image)

Create a file called `Dockerfile` or edit the one you have.

```dockerfile
FROM registry.gitlab.com/lethean.io/sdk/builder as builder
# Change to the mapped mount 
WORKDIR /home/lthn/build
# Copy in the files from the supplied build context
# the space between the dots is important (source) (destination)
COPY . . 
# Do some stuff here
RUN make
# Ok, this Copy of Ubuntu is Full of nasty dev libs! 
# make a new image from now one
FROM ubuntu:16:04 as image
# ok, none of the files we made are here, time to copy into this namespace
COPY --from=builder /home/lthn/build/release/bin /usr/local/bin 

# Enjoy
```

