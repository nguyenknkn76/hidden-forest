> ref: 
> Domain Driven Design (DDD) - Understanding Main Concept: https://dev.to/jhonifaber/domain-driven-designddd-understanding-main-concepts-11p3

## Main concept: 
### DDD: 
- form of software design that focuses on understading and reflecting the business in code. 
- layerd separation, the domain is at the center (domain layer doesn't depend on anything external)

### Domain
- is the business problem that we are solving. 

### Entities and Value Objects
- Entities: are defined by their unique identity and not by their attributes. (Even if their properties change, they are still the same entity)
- Value objects: are defined by their attributes and have no unique identity.

### Agregates and Aggregate Roots
- An aggregate: a group of related domain objects that should be treated as a single unit (have a look at the image below for a better understading) → consistency and capsulate business rules.
- The aggregate root: is the primary entity that controls acess to other objects within the aggregate. (The aggregate root is always an entity and never a value object.)

### Domain Services
### Domain Events
### Bounded Contexts
### Conclusion