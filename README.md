# SQLMap Docker image

**Run [SQLMap](http://sqlmap.org/) inside Docker.**


## Usage

``` bash
$ docker pull sagikazarmark/sqlmap
$ docker run --rm -it -v $HOME:/var/sqlmap sagikazarmark/sqlmap [your params here]
```

## Shell integration

Typing the `docker run...` command every time (even with shell history) is long and a waste of time.
There must be a better way...

There is! Add the following to your `.bashrc` or `.zshrc`:

``` bash
sqlmap() {
    tty=
    tty -s && tty=--tty
    docker run \
        $tty \
        --interactive \
        --rm \
        --user $(id -u):$(id -g) \
        --volume $HOME/.sqlmap:/var/sqlmap \
        sagikazarmark/sqlmap "$@"
}
```

Note: Since on macOS the containers are not accessible directly using their IP addresses,
you have to use port mapping to reach them. However, this does not work with other (unlink) containers well.
For example if your target application is available at `localhost:8080`, but the original port is `80`
then you have to find the IP address of the container using `docker inspect` and use that instead.


## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.
