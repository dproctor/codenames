# codenames

[![GoDoc](https://godoc.org/github.com/jbowens/codenames?status.svg)](https://godoc.org/github.com/jbowens/codenames)

Codenames implements a web app for generating and displaying boards for the <a href="https://en.wikipedia.org/wiki/Codenames_(board_game)">Codenames</a> board game. Generated boards are shareable and will update as words are revealed. The board can be viewed either as a spymaster or an ordinary player.

A hosted version of the app is available at [www.horsepaste.com](https://www.horsepaste.com).

![Spymaster view of board](https://raw.githubusercontent.com/jbowens/codenames/master/screenshot.png)

### Hosting on GCP

To create the GCP instance
```
docker-machine create \
    --driver google \
    --google-machine-type f1-micro \
    --google-project $GOOGLE_PROJECT \
    google-micro
```

Make sure that GCP firewall rules are set up to allow all ingress to tcp:9091.
Once the instance is created, make sure to add `codenames` network tag to apply
the rule.

connect to remote docker host
```
eval $(docker-machine env google-micro)
```

and run the service
```
docker run --name codenames_server --rm -p 9091:9091 -d devonproctor/codenames
```

The (ephemeral) external IP is visible under `VM instances`, and the game is served on port
9091.

After completing the game, don't forget to turn down the server

```
docker-machine stop google-micro
```

and, optionally remove the instance to avoid charges for the persistent disk.
```
docker-machine rm google-micro
```
