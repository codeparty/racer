# Racer

Racer is an **experimental** library for Node.js that provides realtime synchronization of an application model.

## Disclaimer

Racer is not ready for use, so **please do not report bugs or contribute pull requests yet**. Lots of the code is being actively rewritten, and the API is likely to change substantially.

If you have feedback, ideas, or suggestions, feel free to leave them on the [wiki](https://github.com/codeparty/racer/wiki). However, your suggestions and issues are unlikely to be addressed until after the initially planned work is completed. If you are interested in contributing, please reach out to [Brian](https://github.com/bnoguchi) and [Nate](https://github.com/nateps) first.

## Demos

There are currently two demos, which are included under the examples directory.

### Letters

http://letters.racerjs.com/lobby

The letters game allows for multiple players to drag around refrigerator magnet style letters in realtime. It supports multiple rooms, where the room name is the URL path.

Letters demonstrates how applications can use Racer to provide application specific conflict resolution. Try using Firefox's Work Offline feature to move some letters while you move the same letters in another browser that is still connected. Then, disable offline mode and reconnect. Note that conflicting moves are shown along with the new moves that were successfully made. It is then possible to accept or override the moves that were already made.

### Todos

http://todos.racerjs.com/racer

Todos is a classic todo list demo that demonstrates the use of Racer's array methods in a more realistic application. The application code does not handle conflicts, so conflicting changes simply fail to be applied.

## Features

  * **Realtime updates** &ndash; Model methods automatically propagate changes among browser clients and Node servers in realtime. Clients may subscribe to a limited set of information relevant to the current session.

  * **Immediate interaction** &ndash; Model methods appear to take effect immediately. Meanwhile, Racer sends updates to the server and checks for conflicts. If the updates are successful, they are stored and broadcast to other clients.

  * **Conflict resolution** &ndash; When multiple clients attempt to change data in an inconsistent manner, Racer updates the models and notifies clients of conflicts. Model methods have callbacks that allow for application specific behavior.

  * **Offline** &ndash; Since model methods are applied immediately, clients continue to work offline. Any changes to the local client or the global state automatically sync upon reconnecting.

  * **Unified server and client interface** &ndash; The same model interface can be used on the server for initial page rendering and on the client for synchronization and user interaction.

## Future features

  * **Persistent storage** &ndash; Racer will optionally provide automatic storage of data in popular NoSQL document stores and MySQL. Racer will also support extension to support other persistent storage solutions.

  * **Browser local storage** &ndash; Browser models will also sync to HTML5 localStorage for persistent offline usage.

  * **Connect middleware** &ndash; Connect middleware will provide support for easy integration with Express and Connect sessions.

  * **Validation and access control** &ndash; An implementation of schema-based validation and authorization is planned.

  * **Alternative Realtime Strategies** &ndash; In addition to STM, Racer may provide Operational Transformation (OT) and Diff-Match-Patch algorithms to mix and match, depending on the realtime characteristics of the target app.

## Installation

The heart of Racer's conflict detection is a Software Transactional Memory (STM) built on top of Redis. It uses Redis Lua scripting, which is not part of the current stable Redis release, but [should be added](http://antirez.com/post/everything-about-redis-24) in the fall with Redis 2.6. For now, you can install the [Redis 2.2-scripting branch](https://github.com/antirez/redis/tree/2.2-scripting).

After Redis with scripting support is installed, simply add racer to your package.json dependencies and run

```
$ npm install
```

or install Racer for use in multiple node projects with

```
$ npm install racer -g
```

## Tests

The tests will flush Redis and MongoDB databases available via the default configurations, so don't run them in a production environment. The full suite currently requires a running Redis and MongoDB server to complete. Run the tests with

```
$ make test
```
