

```mermaid
classDiagram
    class SpringApplication
    SpringApplication :+String BANNER_LOCATION_PROPERTY_VALUE
    SpringApplication :+String BANNER_LOCATION_PROPERTY
    SpringApplication :+SpringApplicationShutdownHook shutdownHook
    SpringApplication :-Set<Class<?>> primarySources
    SpringApplication :-Set<String> sources
    SpringApplication :-Class<?> mainApplicationClass
    SpringApplication :-Banner.Mode bannerMode
    SpringApplication :-boolean logStartupInfo
    SpringApplication :-boolean addCommandLineProperties
    SpringApplication :-boolean addConversionService
    SpringApplication :-Banner banner
    SpringApplication :-ResourceLoader resourceLoader
    SpringApplication :-BeanNameGenerator beanNameGenerator
    SpringApplication :-ConfigurableEnvironment environment
    SpringApplication :-WebApplicationType webApplicationType
    SpringApplication :-boolean headless
    SpringApplication :-boolean registerShutdownHook
    SpringApplication :-ApplicationContextInitializer<?>[] initializers
    SpringApplication :-ApplicationListener<?>[] listeners
    SpringApplication :-Map<String, Object> defaultProperties
    SpringApplication :-List<BootstrapRegistryInitializer> bootstrapRegistryInitializers
    SpringApplication :-Set<String> additionalProfiles
    SpringApplication :-boolean allowBeanDefinitionOverriding
    SpringApplication :-boolean allowCircularReferences
    SpringApplication :-boolean isCustomEnvironment
    SpringApplication :-boolean lazyInitialization
    SpringApplication :-String environmentPrefix
    SpringApplication :-ApplicationContextFactory applicationContextFactory

    SpringApplication -- SpringApplicationBannerPrinter 
    SpringApplication -- SpringApplicationShutdownHook
    SpringApplication -- ApplicationContextFactory

```
---
```mermaid
classDiagram
    class ApplicationContextFactory
    ApplicationContextFactory :+DEFAULT()

    ApplicationContextFactory -- SpringFactoriesLoader
    ApplicationContextFactory -- ConfigurableApplicationContext
    ApplicationContextFactory -- AnnotationConfigApplicationContext
```


```mermaid
classDiagram
    class SpringFactoriesLoader
    SpringFactoriesLoader :+String FACTORIES_RESOURCE_LOCATION
    SpringFactoriesLoader :-Log logger
    SpringFactoriesLoader :+Map<ClassLoader, Map<String, List<String>>> cache

    SpringFactoriesLoader -- ConcurrentReferenceHashMap
```    

---

```mermaid
classDiagram
    class SpringApplicationBannerPrinter
    SpringApplicationBannerPrinter :+String BANNER_LOCATION_PROPERTY
    SpringApplicationBannerPrinter :+String BANNER_IMAGE_LOCATION_PROPERTY
    SpringApplicationBannerPrinter :+String DEFAULT_BANNER_LOCATION
    SpringApplicationBannerPrinter :+String[] IMAGE_EXTENSION
    SpringApplicationBannerPrinter :-Banner DEFAULT_BANNER
    SpringApplicationBannerPrinter :-ResourceLoader resourceLoader
    SpringApplicationBannerPrinter :-Banner fallbackBanner

```
---
    
 ```mermaid
classDiagram
    Runnable <-- SpringApplicationShutdownHook

    class SpringApplicationShutdownHook
    SpringApplicationShutdownHook :-int SLEEP
    SpringApplicationShutdownHook :-long TIMEOUT
    SpringApplicationShutdownHook :-Log logger
    SpringApplicationShutdownHook :-Handlers handlers
    SpringApplicationShutdownHook :-Set<ConfigurableApplicationContext> contexts
    SpringApplicationShutdownHook :-Set<ConfigurableApplicationContext> closedContexts
    SpringApplicationShutdownHook :-ApplicationContextClosedListener contextCloseListener
    SpringApplicationShutdownHook :-AtomicBoolean shutdownHookAdded
    SpringApplicationShutdownHook :-boolean inProgress
    SpringApplicationShutdownHook :+void run()

 ```


---
---

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

    AutoConfigurationEntry -- AutoConfigurationImportSelector

    class AutoConfigurationImportSelector
   AutoConfigurationImportSelector :-AutoConfigurationEntry EMPTY_ENTRY 
   AutoConfigurationImportSelector :-String[] NO_IMPORTS
    AutoConfigurationImportSelector :-ConfigurableListableBeanFactory beanFactory
    AutoConfigurationImportSelector :-Environment environment
    AutoConfigurationImportSelector :-ClassLoader beanClassLoader
    AutoConfigurationImportSelector :-ResourceLoader resourceLoader
    AutoConfigurationImportSelector :-ConfigurationClassFilter configurationClassFilter


    DeferredImportSelector --|> ImportSelector
    Group --DeferredImportSelector


    BeanClassLoaderAware --|> Aware

    ResourceLoaderAware --|> Aware

    BeanFactoryAware --|> Aware

    EnvironmentAware --|> Aware

```

```mermaid
classDiagram

    class AutoConfigurationImportSelector
   AutoConfigurationImportSelector :-AutoConfigurationEntry EMPTY_ENTRY 
   AutoConfigurationImportSelector :-String[] NO_IMPORTS
    AutoConfigurationImportSelector :-ConfigurableListableBeanFactory beanFactory
    AutoConfigurationImportSelector :-Environment environment
    AutoConfigurationImportSelector :-ClassLoader beanClassLoader
    AutoConfigurationImportSelector :-ResourceLoader resourceLoader
    AutoConfigurationImportSelector :-ConfigurationClassFilter configurationClassFilter
```


``` mermaid
classDiagram
    class AutoConfigurationEntry
    AutoConfigurationEntry :-List<String> configurations
    AutoConfigurationEntry :-Set<String> exclusions
```