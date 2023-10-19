# Event-Driven and Microkernel Architecture Comparison

## Purpose:

This paper serves to compare and contrast the difference between the Event Driven and MicroKernel Architecture.

## Assumptions:

- Reader has elementary understanding of both architectures.
- Reader has the background necessary to understand basic computer science and programming paradigms.

# The Event Driven Architecture

### Strengths

| Attribute   | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Portability | Generally platform independent as the trigger mechanism can be modified without needing to change functionality. |
| Scalability | As-Needed use of computing resources due to invocation being associated with some sort of stimuli. This allows for better resource consumption and less bottlenecks. |
| Modularity  | Application can be easily extended, regardless of underlying implementation. |

### Ideal Application Characteristics

- Asynchronicity is required.
- Underlying compute resources are finite or associated with some sort of cost.

### Exemplary Applications

- Responsive webpages:  we can see this in front-end oriented languages such as the use of the event attribute for Javascript invocation within HTML elements.
- REST API: application remains dormant until invoked by some sort of stimuli.

## Superpower

Perhaps the greatest strength of the event driven architecture is its  decoupling between stimuli and response. The act of listening, polling, or otherwise querying for some sort of information and then reacting to it is a very natural and easy to understand behavior.

### Weaknesses

- It can be difficult to comprehensively test every part of an Event Driven Architecture, thus increasing the chances for bugs to appear in production.
- Error handling is generally more complex. If some piece of functionality fails, the underlying core component(s) running it must be able to gracefully handle that failure.
- Overall system complexity will increase if the events have highly diverse needs  Therefore, it can be very difficult design the system robustly. 

### Unsuitable Application Characteristics

- Due to the complexity associated with their testing, Event Driven Architectures are less suitable for safety-critical applications.
- Application with algorithms that transform data. Mainly, execution is comprised of a series of steps that must be executed in a specific order (something the data scientist gives you to implement).

## The MicroKernel Architecture

### Strengths

| Attribute      | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| Maintainability | Once released, complex parts of the core implementation can remain untouched but the application can still be updated. |
| Extensibility  | Plugins can easily be modified to introduce new functionality. |
| Encapsulation  | Plugins can be developed without needing to disclose the internal workings of the core system. |
| Deployability  | Changes are isolated to specific components. It is more likely that the internal components will change as opposed to the infrastructure. |

### Ideal Application Characteristics

- The maximum amount of compute resource utilization is known and constant.
- The application would derive benefit from utilization of a distributed infrastructure.
- Applications where the [Facade Pattern](https://refactoring.guru/design-patterns/facade) is preferred.

### Exemplary Applications

- Data-Driven: a core algorithm that needs to be capable of ingesting and returning some sort of uniformly-served data from diverse sources.
- Poweruser interface: a high degree of customization (is required) on top of functionality that will not change.

### Weaknesses

- It is often difficult to determine where the core ends and the plugin begins. 
- Applications utilizing this Architecture are difficult to scale up as all requests shall pass through the core system
- Modification to the MicroKernel that necessitates a change to the plugin contract can be difficult to impossible after launch.

### Unsuitable Application Characteristics

- Applications where the system boundaries change constantly.
- Applications where execution must be $< O(N)$

## Kata

- As it is based on some sort of external stimuli, the submission workflow would be well suited for the event driven architecture.

## MicroKernel/Event Driven Architecture Hybrid

#### Is there a difference?

It depends on the level of abstraction you are viewing the system through as well as the problem that the system is trying to solve. That said, there are 2 main drawbacks to consider when implenting this architecture:

- All events would have to pass through the core system. Therefore, substituting events for plugins would decrease overall scalability of the system
- Testability of the system would decrease as comprehensive testing of event driven architectures is difficult to ensure.

## Addendum

I went into this assignment thinking about using the Linux Kernel as an example of a MicroKernel. After learning about the [Tanenbaum Torvalds Debate](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate) I have learned that this is NOT the case. While Linux is [slowly moving toward a MicroKernel Architecture](https://unix.stackexchange.com/a/6458) it is still largely monolithic, scenarios where kernel panic occur align more closely with the Monolithic Kernel Architecture, showing a high degree of coupling between plugins and core.
