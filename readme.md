# TypeScript on Azure
This guide will teach you the basics of building, deploying, and maintaining a web application on Azure. This guide assumes all of your source code is implemented in TypeScript

## Before You Start
If you haven't yet started your project, now is a good time to plan for which Azure services you will use to host your application and store your application's data. If you already know this, or already have an application you want to deploy, you can skip to the next section.

### Application Host
Azure offers a number of ways to host your server-side application code. The options are, in brief:

* **Virtual Machines:** Azure supports arbitrary OSes running in a virtual machine. This option gives you complete control over your app's environment at the cost of managing everything yourself.
* **App Service for Linux:** Azure App Service is a scalable, self-patching managed service for running your Node applications on Linux.
* **Docker Containers:** Azure has first-class support for managing and deploying Docker containers. You can register containers using AKS or support more advanced deployment recipes using Kubernetes.
* **Functions:** Simple applications, for example single API endpoints or proxies, can be implemented as an Azure Function. Functions are a low-cost, low-overhead hosting option for simple applications.

While any of these options are great depending on your requirements, most applications will either want to use App Service or Docker containers. App Service has less management overhead at the cost of a bit more complexity deploying TypeScript builds. Docker containers give you more control but are a bit more work to set up. Both these options are discussed in more detail in the next section.

Also keep in mind that you can move between these options at any time. You can also use more than one option in a single application, e.g. your main application can be managed by App Service with portions of the application implemented as Azure Functions.

### Database
Most applications will need to persist application state and session data. Azure has many hosted database options. MongoDB, CosmosDB, and SQL Server are the most popular options for Node applications. Since Azure offers VMs you can run any database software you like (and the marketplace has many hosted options if you'd prefer not to manage your database yourself), but sticking with one of the first-class options above will ensure a great experience with Node and TypeScript.

* **MongoDB:** Hosted MongoDB is supported in the marketplace. You can also use CosmosDB with the MongoDB APIs. This option gives you the familiar MongoDB API (and support for the variety of Node libraries for talking to it, e.g. mongoid) while taking advantage of CosmosDB's global scaling capabilities.
* **CosmosDB:** CosmosDB is Azure's premier document store database. This highly scalable database can be used with either the DocumentDB API or the MongoDB API.
* **SQL Server:** For applications which need a relational database, SQL Server is a great option on Azure.

Hosted support for other popular SQL databases such as Postgres and MySQL can be found in the marketplace.

## Talking to your Database

### MongoDB

### CosmosDB

### SQL Server

## Storage
Applications which need to store files should do so using a Storage account.

## Authentication

Of course any authentication scheme will work on Azure. However, be aware that Azure offers some hosted services that make authentication easier especially if you're planning on integrating with your existing workplace's Active Directory.

### Azure Active Directory
If your workplace uses Active Directory, you can use AD libraries to authenticate against your existing (what is this thing callled?)

### Twitter, GitHub, Facebook, OAuth...
## Building &amp; Deploying to Azure

### Deploying Application Code

### App Service

### Docker Containers

### Functions

## Production Diagnostics &amp; Telemetry

No application would be complete without feedback from your users! Azure Application Insights is a great way to gather and report on all the telemetry a Node application needs.

### Server-side Telemetry

Application Insights can track a number of server-side metrics. Most important for Node applications are 

### Client-side Telemetry

Application Insights can also track metrics gathered from your clients' browsers. Among other important data, you can collect page load time and client-side JavaScript errors and call stacks. By instrumenting your client-side code you can also track custom events (e.g. how many users click a particular button) and even funnels (e.g. how many users make it through the entire sign up process vs. fall off at each step).

Tracking client-side telemetry requires adding the following snippet to your HTML:

```js
var appInsights=window.appInsights||function(config){
    function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
}({
    instrumentationKey:"d2cb4759-8e2c-453a-996c-e65c9d0e946a"
});

window.appInsights=appInsights;
appInsights.trackPageView();
```

Take care to replace the instrumentation key above with your own instrumentation key.