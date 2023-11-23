# Symbiotic Framework


## Features

- PSR friendly
- Only a few dependencies (only PSR interfaces and PSR-7 implementation).
- Light weight.
- Optimized to work in symbiosis with other frameworks.
- Multilevel DI container system **(Core <- Application <- Plugin)**, with access to the parent container.
- Virtual file system (proxying static from the package folder to the web).
- The familiar api of the container (laravel/container).
- Blade template engine (stripped down), + the ability to add your own template engine.
- No static collectors (Each package must have already compiled files).
- Deferred routing (only the routes of the requested application are loaded, determined by the prefix-settlement).
- The ability to extend the kernel via Bootstrap and Service Provider.
- Each application has its own container service and services.
- Cache support (PSR-16 Simple Cache) + Cached DI Container.
- Middleware support for intercepting a request before loading the core of the framework (response in 1 ms).


## Description

**The framework was created to simplify the integration of independent small applications into other CMS and frameworks,
as well as to expand the functionality of the composer packages.**

Ideology is a separate ecosystem of small applications for collaboration with other frameworks and convenient
integration of additional functionality.

There are many packages and separately written applications
that deliver useful functionality, have their own business logic and sometimes even have their own separate web interface.

In Laravel packages, in Symfony Bundles, in various CMS in the form of plugins and add-ons, all have their own implementation of routing,
events, caching, etc.
A package written for Laravel to integrate another framework or CMS will be problematic in most cases,
and in some cases impossible due to certain dependencies on the framework.

Application developers themselves have to write adaptations for each framework and CMS,
which creates a lot of problems and does not cover all ecosystems.

**Also, such applications have to do various integrations into the system:**

1. Configure ACL
2. Integrate the necessary scripts to the admin panel and to the site
3. Create query handlers and a structure in the database
4. Configure a bundle with the file system
5. To save settings and configuration

**Such applications include:**

- Single Page Applications
- Text editors and their plugins with multiple levels of dependency (plugin for plugin)
- Media Handlers
- Various optimizers and compressors
- Applications for administrative work with files and databases
- Chat bots, messengers, widgets
- Integration API components, OAuth authorization providers
- Hosting administration and monitoring tools, analytical tools
- Landing pages and other micro applications ....

**The framework is optimized to work with a large amount of applications, as well as to work as a subsystem for
the main framework.**

Each application is a composer package,
with an additional description directly in the composer.json file.

## Integration

 ```mermaid

    flowchart TB
    Symbiotic[("Symbiotic
    Container PSR-11 
    Events PSR-14
    Middleware PSR-15
    HTTP Message PSR-7
    Cache PSR-16
    Logger PSR-3")]:::asdasdasasd
    IntegrationBase[("-------
    Symbiotic as Service
    Symbiotic events
    Cms Events
    ")]:::IntegrationBase
    Application([Application]):::APP --> |Write your app for Symbiotic|Symbiotic
    Symbiotic:::Integration ---> LaravelPackage[Laravel Package]:::bridge-->Laravel[[Laravel]]:::framework
    Symbiotic:::Integration ---> SymfonyBundle[Symfony Bundle]:::bridge-->Symfony[[Symfony]]:::framework
    Symbiotic:::Integration ---> WPIntegration[Wordpress plugin]:::bridge-->Wordpres(Wordpress):::framework
    Symbiotic:::Integration ---> joomlaIntegration[Joomla plugin]:::bridge-->Joomla(Joomla):::framework
    Symbiotic:::Integration ---> psr15integration[PSR-15 Middleware ]:::bridge-->PRS-15[[PSR-15]]:::framework
    Symbiotic:::Integration ---> otherIntegration[Other...]:::bridge-->other[...Other CMS]:::framework
    subgraph INTEGRATIONS 
    direction BT
    IntegrationBase-.->  LaravelPackage 
    IntegrationBase-.->  SymfonyBundle 
    IntegrationBase-.-> WPIntegration 
    IntegrationBase-.-> joomlaIntegration
    IntegrationBase-.-> psr15integration
    IntegrationBase-.-> otherIntegration
    end
    classDef desc fill:#000,stroke:#000,color:#000,font-size:10pt
    classDef bridge fill:#333,stroke:#222,color:#fff,font-size:12pt
    classDef APP fill:#ff9000,stroke:#000,color:#fff
    classDef Integration fill:#5cff6b,stroke:#000,color:#000,font-size:12pt
    classDef IntegrationBase fill:#eee,stroke:#000,color:#333
    classDef framework fill:#5cff6b,stroke:#555,color:#000,width:140px
    linkStyle 1,3,5,7,9,11 stroke:#ff9000,stroke-width:2px,color:#fff
    linkStyle 2,4,6,8,10,12 stroke:#5cff6b,stroke-width:2px,color:#fff


```
