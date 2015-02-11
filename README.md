### Docker-ZNC

This image uses the ubuntu:vivid image which provides the latest znc, and therefore, all the updated libraries to work with building modules correctly. 

**Some info's:**

* I used vivid to make life easier. This image contains everything you need to not only run znc, but build your extra modules within it as well.

* Additionally, I install libotr to provide support for the http://wiki.znc.in/Otr plugin, which I personally use, and I hope you do too!

* We run znc as root. So be mindful not to --privilege this container! Also, this means you don't have to worry about the permissions of your znc_config directory:)

**Installation:**

1. Build a crane/fig etc.. service file which does similar to the following:

`docker run -d -p 8443:8443 -v ./znc_config:/znc_config --name znc inanimate/znc`

2. ????

3. Profit.

> If you do not already have a config directory (if you've been using znc, its `/home/username/<znc>`), take a look at run as it provides a basic config by providing some parameters.
