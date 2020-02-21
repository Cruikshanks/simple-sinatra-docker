# Simple Sinatra Docker example

Created as part of getting myself back into (and hopefully sticking with!) Docker.

I wanted to create a very basic web app running in a Docker container before moving onto getting Rails running in Docker. So I created this using a mix of the instructions at <https://hub.docker.com/_/ruby> and stuff I found on the interwebs.

## Build

First you need to build the image

```bash
docker build -t simple-sinatra-docker .
```

Having run this on a machine clean of other Docker images running `docker images` will result in something like

```bash
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
simple-sinatra-docker   latest              08c61ac91c79        9 seconds ago       731MB
ruby                    2.4.2               2a867526d472        2 years ago         687MB
```

## Run

Now we have an image, we want to create and run a container from it

```bash
docker run -p 4567:4567 --name simple-sinatra-docker-running simple-sinatra-docker
```

Breaking down this command we have

- `docker run` first creates a writeable container layer over the specified image, and then starts it using the specified command
- `-p 4567:4567` bind port 4567 on the host to 4567 in the container <host:container>
- `simple-sinatra-docker-running` the name we give to the container
- `simple-sinatra-docker` the specified image to create and run the container from

Running in this way ensures we see any output from our app. Add the `-d` flag if you prefer the container to run as a daemon.

## Remove

Once you are finished with the container, even though its not running it still exists. If you want create it again (because you have updated the image) you first need to remove it

```bash
docker container rm --force simple-sinatra-docker-running
```

The `--force` command will mean even if its running it will still be removed. A shortcut is to add `--rm` to the run command. This will mean docker automatically removes the container when it exists.

## Contributing

If you think I'm doing something wrong and it pains you not to tell me, then by all means create an issue. But this seriously is just a small throwaway app!

## License

This information is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

> If you don't add a license it's neither free or open!
