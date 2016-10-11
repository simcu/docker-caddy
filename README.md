
# docker-caddy

[Caddy](https://caddyserver.com/) in a docker container, configurable via a [simple web UI](https://github.com/jpillora/webproc)

[![Docker Pulls](https://img.shields.io/docker/pulls/jpillora/caddy.svg)][dockerhub]
[![Image Size](https://images.microbadger.com/badges/image/jpillora/caddy.svg)][dockerhub]

[dockerhub]: https://hub.docker.com/r/jpillora/caddy/

### Usage

1. Create a [`/opt/Caddyfile`](https://caddyserver.com/docs/caddyfile) file on the Docker host

	``` ini
	# Caddy config, for a more information, see:
	#  https://caddyserver.com/docs/caddyfile
	http://localhost:80 {
	    gzip
	    log stdout
	    proxy / example.com
	}
	```

1. Run the container

	```
	$ docker run \
		--name caddy \
		-d \
		-p 58080:8080 \
		-p 80:80 -p 443:443 \
		-v /opt/Caddyfile:/etc/Caddyfile \
		-v /opt/caddy:/root/.caddy \
		--log-opt "max-size=100m" \
		-e "USER=foo" \
		-e "PASS=bar" \
		jpillora/caddy
	```

1. Visit `http://<docker-host-ip>:58080`, authenticate with `foo/bar` and you should see

	SCREENSHOT TODO

1. You now have an HTTP web server running at `http://<your-hostname>`

1. Bind `<docker-host-ip>` to `<your-hostname>` using your DNS provider

1. Change `http://localhost:80` to `https://<your-hostname>:443`, below the `proxy` line - add `tls <your-email>` and **Restart**

1. You now have an HTTPS web server running at `https://<your-hostname>`

#### MIT License

Copyright &copy; 2016 Jaime Pillora &lt;dev@jpillora.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
