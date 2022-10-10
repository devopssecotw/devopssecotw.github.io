
```mermaid
classDiagram
```


```text
sb4
su3
ju3
sc3
jl1
SpringApplication sb1-6

```
```mermaid
graph TD
  subgraph SpringApplication
        sb1[SpringApplication] --Springdemo1Application.class, args--> sb1-2[run]
        sb1-2 -- new -->sb1-3[SpringApplication]
        sb1-3 --deduceFromClasspath --> sb2[WebApplicationType] --> sb2-1[WebApplicationType.deduceFromClasspath]
        sb1-3 --BootstrapRegistryInitializer-->sb1-5[getSpringFactoriesInstances]
        sb1-5 --> sb1-6[getClassLoader]

        sb1-6 --type, classLoader--> sb3[SpringFactoriesLoader] --> sb3-1[loadFactoryNames] --ClassLoader classLoader-->sb3-2[SpringFactoriesLoader.loadSpringFactories] --FACTORIES_RESOURCE_LOCATION--> ja1[ClassLoader.getResources]--url-->sc1[UrlResource]--resource-->sc2[PropertiesLoaderUtils]--UrlResource-->sc2-1[loadProperties] -->su1[StringUtils] --String-->su1-1[commaDelimitedListToStringArray]-->ju1[HashMap]-->ju1-1[computeIfAbsent]-->ju1-2[replaceAll]-->ju2[Collectors]-->ju2-1[collectingAndThen]-->ju2-2[toList]-->ju3[Collections]-->ju3-1[unmodifiableList]
        sb3-2 -->ju1-3[getOrDefault]
        sb3-1 -->sb3-3[instantiateFactory] -->su2[ClassUtils] --factoryImplementationName, classLoader-->su2-1[forName]
        -->su3[ReflectionUtils]-->su3-1[accessibleConstructor]-->su3-2[newInstance]
        sb1-3 -->sb12[setInitializers]
        sb3-3 -->sc3[AnnotationAwareOrderComparator]-->sc3-1[sort]
        sb1-3 -->sb13[setListeners]
        sb1-3 -->sb14[deduceMainApplicationClass]
        sb14 -->jl1[RuntimeException] -->jl1-1[getStackTrace]

        sb1-2 -->sb1-7[createBootstrapContext]
        sb1-7 -->sb4[DefaultBootstrapContext]
  end
```


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
    ApplicationContextFactory :+ConfigurableApplicationContext create(WebApplicationType webApplicationType)
    ApplicationContextFactory:ApplicationContextFactory ofContextClass(Class<?> contextClass)
    ApplicationContextFactory :+ApplicationContextFactory of(Supplier<ConfigurableApplicationContext> supplier) 

    ApplicationContextFactory -- SpringFactoriesLoader
    ApplicationContextFactory -- ConfigurableApplicationContext
    ApplicationContextFactory -- AnnotationConfigApplicationContext
```

```text
org.springframework.boot.ApplicationContextFactory.DEFAULT

```

---

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