Our Clean Code Architecture
Here is the markdown version of the clean architecture layers from the image:
Explanation of architecture is here :- [[Clean Code Architecture#Explanation of Platform Agent Architecture]]
```markdown
# CLEAN ARCHITECTURE LAYERS

## INFRASTRUCTURE
```

```
infrastructure/
├── adapters/
│   ├── http
│   ├── ws
│   ├── nats
│   ├── event-listeners/
│   │   ├── ...
├── mappers (mapping between domain models and external data formats)/
│   ├── ...
├── managers (any low level impl for infra other clients etc.)/
│   ├── mongodb-manager
│   ├── nats-manager (import cloud-nats client or create different managers)
├── data/
│   ├── models (flexible)/
│   │   ├── database
│   │   ├── rpc
│   ├── repo-impl
│   ├── sources/
│   │   ├── local
│   │   ├── remote
```

## PRESENTATION

```
application (this is the presentation layer)/
├── app.ts (**)
├── controllers (Maps use-cases to gateways with middlewares)/
│   ├── node-registration-controller.ts (**define folder structure here)
```

## DOMAIN

```
domain/
├── entities (interfaces and impl if needed)
├── repositories (interfaces)
├── use-cases
```

## META

### DI

```
di/  # Dependency Injection module
├── factories/  # Factory classes for complex object creation
│   ├── repository_factory.ts
│   ├── use_case_factory.ts
├── containers/  # DI containers/modules configuration
│   ├── application_container.ts
│   ├── infrastructure_container.ts
│   ├── presentation_container.ts
├── index.ts  # Main DI configuration and container export
```

## DEPLOYMENTS

```
deployments/
├── deployment-config
├── dev
├── prod
```


## Coding Guidelines

1. Can the code be made simpler? Will another developer be able to easily understand and use this code when they come across it in the future? Add comment if necessary.
    
2. Check the code for good engineering practices such as [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), [SOLID](https://en.wikipedia.org/wiki/SOLID), what are the [coupling](https://en.wikipedia.org/wiki/Coupling_(computer_programming)#:~:text=Coupling%20and%20cohesion%20are%20terms,within%20a%20single%20module%20are.) and [cohesion](https://www.geeksforgeeks.org/software-engineering-coupling-and-cohesion/) like.
    
3. Check if error handling have been done everywhere or not, with good amount of logging info? What does it expose to the users positively and negatively?
    
4. Introduce adequate amount of debugging and logging metrics?
    
5. What dependencies is the code taking on other systems/code? Are these dependencies required? Reasons for using a dependency ?
    
6.  Is the code adhering to good practices in secure/defensive coding? Are these secrets in the code?
    
7. Does the code actually do what it says it does? If necessary you can add some comment to exaplain in simple manner what does that code do? What testing has been carried out?

## Naming Conventions
1. Use camelCase for variable and function names
2. Use PascalCase for class and interface names
3. Use descriptive names for variables, functions, and classes
4. Avoid abbreviations unless widely recognized
5. Make use of Enums wherever necessary

### Enforcing standards in github pull request
