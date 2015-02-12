### Docker-ZNC

This image uses the ubuntu:vivid image which provides the latest znc, and therefore, all the updated libraries to work with building modules correctly. 

**Some info's:**

* I used ubuntu:vivid to make life easier. This image contains everything you need to not only run znc, but *build your extra modules* within it as well.

* Additionally, I install libotr5 to provide support for the http://wiki.znc.in/Otr plugin, which I personally use, and I hope you do too!

* We run the init script, `/znc-run`, as root. That subsequently runs znc as a user `znc`. So be mindful **not** to --privilege this container! Also, this means you don't have to worry about the permissions of your znc_config since the `znc-run` script will chown everything for the znc user:)

**Installation:**

1. Build a crane/fig etc.. service file which does similar to the following:

        docker run -d -p 8443:8443 -v ~/.znc:/znc_config --name znc inanimate/znc

2. ????

3. Profit.

4. Want to build a module? Just use nsenter (docker-enter) and do eit!! Be mindful if your module relies on external libraries and whatnot. A good example of this is the otr plugin I talk about above, which won't even work with znc-buildmod; I had to build it right out of its git repo.


> If you do not already have a config directory (if you've been using znc, its `/home/username/.znc`), take a look at `/znc-run` as it provides a basic config by providing some parameters.


#### Example crane config:

```
containers:
    znc:
        image: inanimate/znc
        run:
            restart: always
            publish: ["0.0.0.0:8443:8443"]
            volume: ["./znc_config:/znc_config"]
            hostname: znc
            detach: true
```
