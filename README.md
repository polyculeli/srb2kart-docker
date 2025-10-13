# Sonic Robo Blast 2 Kart Docker

This is a docker container for [SRB2Kart](https://mb.srb2.org/addons/srb2kart.2435/) for ease of setting up a server. It automatically downloads and builds the source code from the public [SRB2Kart releases](https://github.com/STJr/Kart-Public/releases).

## Docker Tags

The tags for this container will be in varying granularities. As a basis you have the following tags:

- `latest`: Always the latest major and minor version.
- `<major_version>`: E.g. `alicianibbles/srb2kart:1`. This is the latest docker image in that major version. This might update minor versions on the go as well as dependencies being updated.
- `<major_version>.<minor_version>`: E.g. `alicianibbles/srb2kart:1.6`. This is the latest docker image with the respective major and minor version. This might still update dependencies on the fly while keeping a constant major and minor version.
- `<major_version>.<minor_version>.<build_number>`: This one is a specific major and minor version pinned to a specific build. This one won't have any parts updated and will be a completely stable image.

## Environment Variables

- `PASSWORD`: Sets the password to [log in](https://wiki.srb2.org/wiki/Console/Commands#login) as an administrator on the server within the game.
- `BANDWIDTH`: Sets the bandwidth in bytes per second. Default is 30000 bytes per second, minimum allowed value is 1000 bytes per second.
- `EXTRATIC`: Specifies up to how many extra previous tics to send to the client per server tic.
- `IPV6`: Listens to incoming IPv6 connections. Warning, this is untested.
- `PACKETSIZE`: Changes the size of UDP packets sent.
- `USEUPNP`: Turns on Universal Plug and Play support. This feature is untested.
- `WARP`: Sets what map to warp to at the beginning of the game.

For more information see the official documentation on [Command-line parameters](https://wiki.srb2.org/wiki/Command_line_parameters) since the environment variables for the docker container mirror those. You can also pass them as command-line arguments, but environment variables are recommended. Those might not necessarily work since the wiki is focused on srb2, not srb2kart.

## Persistent Data

You might want to persist some of the data the SRB2Kart server uses on your host system through volumes.

### Addons

This folder is mapped as a volume at `/addons` and should be used to store addons for the game, which will automatically be loaded into the server. The files in here must not contain any spaces in their filenames.

### Data

This folder is mapped as a volume at `/data` and holds general game data, and configuration files. Some notable files are:

- `.srb2kart/kartserv.cfg`: A [console script](https://wiki.srb2.org/wiki/Console_script) file that automatically gets loaded when starting the dedicated server. For example setting general game configuration, [console variables](https://wiki.srb2.org/wiki/Console/Variables), or a nice [colored server name](https://mb.srb2.org/threads/colored-server-name-tutorial-chat-text-transparency.25474/).


## Running With Docker

To run the server normally with docker, just execute

```sh
docker run -it --name srb2kart -v /path/on/host/addons:/addons -v /path/on/host/data:/data -e ROOM_ID=33 -p 5029:5029/udp alicianibbles/srb2kart:latest
```

## Running With Docker Compose

TBD
