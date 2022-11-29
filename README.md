# Table of Contents
---
- [Table of Contents](#table-of-contents)
- [Background](#background)
- [Install](#install)
- [Architecture](#architecture)
- [Usage](#usage)
- [Maintainers](#maintainers)
- [Acknowledgment](#acknowledgment)
- [Reference](#reference)
---

# Background
This project builds a simple prototype of publish-subscribe system using `Go`. 

- Server: mainly implemented with `Bully Algorithm` for leader election.
- Client: mainly works in `subscribe/publish/unsubscribe` from the server.

The servers are able to communicate with each other, and the clients as well. Server may store the topic and any relevant content of the topic. Clients is able to subscribe or unsubsribe the topic. If a client is the follower of a specific topic. Then he/she is able to publish the content. Once the content is updated, the rest of all the client who subsribes this topic, will be informed as well.

From the server side, if the topic is being updated, the leader should broadcast this update to all the follower. If it is the follower who got this message, it will firstly report this update to the leader, then the leader will repeat the broadcast process.

# Install
Before you clone or download the project via git or other methods manually. Make sure the version of `Go` in your local machine is consistent with `Go.mod`

# Architecture
```yaml
- pub-sub
    - client
        - index.go
    - server
        - index.go
        - peer-conn.go
        - peer-mgr.go
        - server.go
        - subscription-mgr.go
    - domain
        - message.go
    - go.mod
    - main.go
    - README.md
```

1. `client` only works in `pub/sub` process。
2. `server` defines how the server should work. Their communication between the servers will be manged by `peer-mgr` and `peer-conn`.
3. `domain` defines how the meesage format should be like. It is similar to a self-defined protocol
4. `go.mod` defines the version of `Go`.
5. `main.go`, the entrance of the whole program.

# Usage
Once you have make it available on your local machine. It is the time to make it run and play with it. The commands are slightly different for `server` and `client`, let's read it one by one:

- Server:`go run main.go [-server-addr ip:port_number]`

> The server-addr is not required. If you do not specify the ip address with port number, it uses the default one (127.0.0.1:8000)
> > To initialize multiple server, you **MUST** given different **port number** or OS would not allow it.

We recommend you use the *local host* as the IP address `127.0.0.1` for local testing

- Client: `go run main.go -mode client`
> To run a client, you must specify the `-mode` as client or it runs in `server mode` by default
> > The `server address` and `port number` are not required. It uses local host as IP address and port number are randomly assigned.

After you run the command successfully in the terminal. You may see the following interface:
```terminal
Supported Commands:
-> Subsribe: s <topic>
-> Publish: p <topic> <content>
-> Unsubscribe: u <topic>
```

Based on the hint previously, we do a sample for demonstrate:
- Subscribe a topic named `Music`
`s Music`
- Publish a content `Love Story` under topic `Music`
`p Music Love Story`
- Unsubsribe from `Music`
`u Music`

# Maintainers
- [@Eyjan-Huang](https://github.com/Eyjan-Huang)
- [@Jingyi96](https://github.com/Jingyi96)
- [@Jenny](https://github.com/Jenny-Zhen-Wang)

# Acknowledgment
We all sincerely appreciate the academic materials provided by Prof. Moazzeni. Also we acclaim the help provided by [@ninomiyx](https://github.com/ninomiyx) for providing us a general framework of how pub/sub system work. We honestly acclaim how complicated when implementing such system in programming language.

# Reference
1. [What is Pub/Sub?](https://cloud.google.com/pubsub/docs/overview)
2. [Publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)
3. [python-pubsub](https://github.com/googleapis/python-pubsub)


