# designing_elixir_systems_with_otp
### Chapter 1: Build Your Project in Layers

A high-level overview highlighting layer-focused design principles, the roots of robust and scalable software. In Elixir, that will frequently involve the OTP standard library.

Presents the well-known (at least in Elixir circles) **D**o **F**un **T**hings with **L**oud **W**orkerbees:
**Data** - Domain modeling
**Functional Core** - Business logic
**Testing** - Behavioral contracts and validation
**Lifecycle** - Supervision
**Workers** - Pools and dependencies

#### Data
```
"When the data structure is right, the functions holding the algorithms that do things can seem to write themselves. Get them wrong and it doesn't really matter how good a programmer you are; your functions will feel clumsy and awkward."
```
The datatypes we construct will later on guide the structure we of the components of our applications and the govern the way our functions interact with each other.

#### Functional Core
```
"Building our core allows us to isolate the inherent complexity of our domain from the complexity of the machinery we need to manage processes, handle side effects, and the like."
```

Inner layer (functional core) should:
- not care about any boundary-related operations;
- also, it should not preserve state;
- as well as minimal side effects;
- and is made up of functions.

#### Testing
```
"One of the benefits of structuring your project into core and boundary layers is that our coding organization will simplify testing. With a basic API layer that does most of the business logic, you'll be able to write tests to thoroughly exercise your business logic should you choose to do so."
```

Keeping the functional core isolated from external conditions drastically reduces testing complexity.

#### Lifecycle
```
"Supervisors are about startying and stopping cleanly, whether you have a single server or a bunch of them. Once you can start cleanly and detect failure,  you can get failover almost for free"
```

OTP is the built-in mechanism for supervision in Erlang/Elixir:
- Supervision is not about handling failure;
- rather it is about isolating processes and managing their lifecycles;
- This means supervision is more about lifecycles than it is about handling failure;
- and if you get the lifecycle right you will also have a higher likelihood of good recovery as a result;
- meaning that Elixir's primary mechanism for handling failure is supervision-based lifecycle management.

#### Workers
```
The workers are the different processes in your component. Generally, you'll start with a flat design having a single worker and decide where you need to be more sophisticated.

As your design evolves you will possibly see places that you need to add workers, for cleaning up lifecycles or for concurrently dividing work. Connection pools are workers; tasks and agents can be as well.
```
- Various constructs that provide concurrency
- Adjacent to the *boundary* and *lifecycle* layers but is its own *worker* lifecycle
