# drone-rsync

[![Build Status](http://beta.drone.io/api/badges/drone-plugins/drone-rsync/status.svg)](http://beta.drone.io/drone-plugins/drone-rsync)
[![Coverage Status](https://aircover.co/badges/drone-plugins/drone-rsync/coverage.svg)](https://aircover.co/drone-plugins/drone-rsync)
[![](https://badge.imagelayers.io/plugins/drone-rsync:latest.svg)](https://imagelayers.io/?images=plugins/drone-rsync:latest 'Get your own badge on imagelayers.io')

Drone plugin to deploy or update a project via Rsync. For the usage information and a listing of the available options please take a look at [the docs](DOCS.md).

Use the rsync plugin to deploy files to a server using rsync over ssh. The following parameters are used to configure this plugin:

* `hosts` - connects to this host address
* `user` - connects as this user
* `port` - connects to this host port
* `key` - SSH RSA privete key for remote host 
* `source` - source path from which files are copied , if you want skip rsync ,set source null or comment it `source: `
* `target` - target path to which files are copied `target: /docker/proj/`
* `chmod` - chmod remote target after finish rsync `chmod: 0644`
* `chown` - chown remote target after finish rsync `chown: "33:33"`
* `delete` - delete extraneous files from the target dir `delete: true`
* `include` - include files matching the specified pattern
* `exclude` - exclude files matching the specified pattern
* `filter` - include or exclude files according to filtering rules
* `export` - export ENV used for script in remote machine by ssh 
* `script` - execute commands on the remote host after files are copied

Sample configuration in the `.drone.yml` file:

```yaml
deploy:
  rsync:
    user: root
    host: 127.0.0.1
    port: 22
    source: copy/files/from
    target: send/files/to
    delete: false
    exclude:
      - "exclude/this/pattern/*"
      - "or/this/one"
    script:
      - service nginx restart
```

## Keys

The plugin authenticates to your server using a per-repository SSH key generated by Drone. You can find the public key in your repository settings in Drone. You will need to copy / paste this key into your `~/.ssh/authorized_keys` file on your remote machine.

