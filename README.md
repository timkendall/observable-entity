# Observable Entity

The *Observable Entity* design pattern is an experimental design pattern for architecting front-end (UI) applications. It is based largely on the [Repository Design Pattern](http://martinfowler.com/eaaCatalog/repository.html) popularized by the [Hanami](http://hanamirb.org/) framework. The goals and best use-cases of this pattern are listed below.

## Key Concepts

- **Entities** are observable, unique, and long-lived
- **Repositories** interact with remote and local data-persistence layers
- **Organizers** are responsible for calling repository methods and constructing instances of entities

### Entities

- Dumb (no knowledge of either their repositories or related organizers)
- Whitelist acceptable data
- Can have lazily computed values
- Handle serialization and deserialization of external representations of the data
- Should only ever be one instance in memory for one unique `id`
- Only removed from memory if remote representation is deleted

### Repositories

- Interact with remote and local data persistence layers (examples: HTTP, WebSockets, client-storage)
- Static classes (or classes with Static methods)
- Can emit udates about data

### Organizers 

- Single instance
- Initialze application state by calling methods on repositories to instantiate entities
- Keeps local entities in sync with remote data
- May have knowledge of other Organizers
- UI has direct knowledge of them 

*Organizers are essentially a mix of Redux-styles stores and traditional Controllers*

## FAQ

### Why would I use this over something like Redux (i.e Event Sourcing)?

Event Sourcing is an amazing design pattern and honestly preferable if your team has the time and talent. It makes sure your application is completely deterministic (as long as you follow the [rules]()!). Howerver it does come with a higher intelectual cost and more boilerplate to manage. 

Observable Entity can give you close to the same determinism by using something like [MobX](https://github.com/mobxjs/mobx) and with significantly less cognitive load and boilerplate. This makes it better suited for less-experienced developers and  applications involving many domains of data.
