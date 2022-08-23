# SRC
## Spring
### framework
#### spring core

```mermaid
classDiagram
    AnimalApplicationContext --|> EnvironmentCapable
    AnimalApplicationContext --|> ListableBeanFactory
    AnimalApplicationContext --|> HierarchicalBeanFactory
    AnimalApplicationContext --|> MessageSource
    AnimalApplicationContext --|> ApplicationEventPublisher
    AnimalApplicationContext --|> ResourcePatternResolver
   
    ResourcePatternResolver --|> BeanFactory

```