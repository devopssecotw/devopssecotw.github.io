
```mermaid
classDiagram
    SpringBootApplication --> SpringBootConfiguration
    SpringBootApplication --> EnableAutoConfiguration


    EnableAutoConfiguration --> AutoConfigurationImportSelector


    AutoConfigurationImportSelector --|> DeferredImportSelector
    AutoConfigurationImportSelector --|> BeanClassLoaderAware
    AutoConfigurationImportSelector --|> ResourceLoaderAware
    AutoConfigurationImportSelector --|> BeanFactoryAware
    AutoConfigurationImportSelector --|> EnvironmentAware
    AutoConfigurationImportSelector --|> Ordered 



    DeferredImportSelector --|> ImportSelector
    Group --DeferredImportSelector


    BeanClassLoaderAware --|> Aware

    ResourceLoaderAware --|> Aware

    BeanFactoryAware --|> Aware

    EnvironmentAware --|> Aware
```