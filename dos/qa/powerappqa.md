# dos
## Power Apps
### QA
#### p1
#### p1
- Introduction
  Professionals with valuable Microsoft PowerApps skills are in high demand by both medium-sized and large-sized businesses. Low-code applications are becoming increasingly popular in the current environment due to their ease of creation. PowerApps is one of the Microsoft Power Platform's four primary services, along with Power Automate, Power Virtual Agents, and Power BI. It is yet another Microsoft solution connected with the Office 365 package of tools that provides new potential for businesses of all kinds to build custom apps, automate processes, and achieve efficiency.

PowerApps supports a variety of connectors that allow you to use data from a variety of sources, including SharePoint, Microsoft Dynamics 365, Salesforce, and other third-party systems. Mobile applications can be created with this tool kit to solve certain duties in a business. PowerApps is a low-code platform that allows you to configure apps without having to be a developer.

Using Microsoft Power Platform App Maker, technical business analysts and programmers with Data Modelling skills may create and enforce business processes as well as solve business challenges. IT workers interested in a career as a PowerApps Consultant should have a basic understanding of data modelling, user experience design, requirement analysis, and process analysis. You can wow your clients as a PowerApps Consultant with model-driven charts, dashboards, and a user-friendly GUI.


If you're interested in learning more about PowerApps and want to pursue a career in the industry, this article contains PowerApps interview questions and answers that your potential employer might ask. Examine them attentively, plan accordingly, and you'll have a better chance of getting employed.
- Power Apps Interview Questions for Freshers
1. What are Power Apps?
   PowerApps is a Platform as a Service (PaaS) at its core. It enables users to construct Mobile Apps that operate on a variety of platforms, including Android, iOS, and Windows (Modern Apps), as well as practically any Web browser. Power Apps is a set of apps, services, adapters, and data platforms that work together to create an agile development environment for creating unique software that meets business needs. You may quickly construct unique business apps with Power Apps that interface with your company's data, which is deposited either from the underpinning data platform (Common Data Service) or from a variety of internet and on-premises data sources (SharePoint, Excel, Office 365, Dynamics 365, SQL Server, and so on).

2. What are the features of PowerApps?
   PowerApps, like Flow and other Office 365 automation technologies, has capabilities and tools to let you create apps without coding. These are some of them:

A collection of sample apps that you may use as a starting point and then customise.
A collection of more than 200 connectors for integrating data and systems across the Office 365 universe
A simple drag-and-drop interface for app construction.
Tight connectivity with other Dynamics and Office 365 tools.
There is robust support infrastructure in place, including a strong PowerApps community.
3. Is it feasible to develop PowerApps without having a licence?
   No. Without a licence, neither the creation nor the consumption of PowerApps is possible.

By joining up for a 30-day PowerApps trial plan, you may try out all of the features for free. If you don't have a Power Apps licence, the trial plan gives you temporary access to the following features:

It extends Office 365's capabilities (SharePoint Online, Teams, Excel, and more)
You can create and execute canvas apps with Microsoft Dataverse and over 200 other data sources, including premium connectors and on-premises data.
Model-driven apps can be created and run.
With Power Automate, you can create automated workflows.
Create and administer Dataverse databases and environments.
4. What are the major components of PowerApps?
   Power Apps is a high-productivity business app development platform with four primary components:

Canvas apps.
Model-driven apps.
Portals.
Microsoft Dataverse.
5. Explain common data services and why they should be used.
   The common data service allows data from several sources to be combined into a single store that can be used in Power Automate, Power Virtual Agent, Power BI, and PowerApps. This makes the app development process go as smoothly as possible. The Common Data Service will enable you to store and manage data that is securely utilised by business applications The data that is saved in the Common Data Service is organised into a set of entities. A set of records is referred to as an entity, and it is used to store data in the same way that a table does in a database. The Common Data Service also has a set of basic entities that will handle most circumstances, but you can also construct new entities that are unique to your company and populate them with data using Power Query. PowerApps will be used by app developers to create sophisticated applications based on this data.


6. Difference between Canvas and Model Driven Apps.
   Canvas Apps: Canvas apps, on the other hand, start with the user experience and allow for customization through various UI features such as charts, media, drop-down lists, text-input boxes, labels, and more. You may also create canvas apps for use on the web, mobile devices, and tablets. Canvas apps provide you with the freedom to customise the user experience and interface in any manner you choose. It also allows you to use your imagination and business savvy to help you decide how you want your apps to be presented.
   Model-driven Apps: To create a significant app, model-driven apps use a component-based methodology. Dashboards, business processes, forms, charts, views, and entities are some of the components that make up a user interface. Model-driven Apps begin with your data model, which will be built up from the shape of your core business data and processes in the CDS to model forms, views, and a variety of other components. Model-driven apps will create fantastic user experiences that are responsive across devices automatically. You can also use the Power Apps portal to create model-driven apps.
7. When should you use Model-driven apps instead of Canvas apps as a consultant?
   Model-driven apps can be a simpler alternative to create when the data can be managed with Dataverse defined tables.

8. Is it possible to share a canvas app with contractors and external business partners?
   Yes, visitor users can be invited to utilise the app using Azure AD B2B external collaboration for the tenancy.

9. What are the different kinds of apps that PowerApps can create?
   Canvas apps, common data services, model-driven apps, and portals are all possible with PowerApps, a productivity development platform.

10. Can you make the canvas apps more responsive?
    You may achieve this by using the height and width attributes of app screens. Container controls are also available.


11. What are the various methods of submitting data from PowerApps?
    Patch() and Submit form are two functions that can be used to complete this task (). Patch(), on the other hand, can be used to upload partial data.

12. Is it possible to use PowerApps to access local network data sources?
    Yes, we can easily connect to data sources on the local network.

13. What are the options for using media files in the Canvas app?
    PowerApps allows you to upload up to 200 MB of media for each app. However, leveraging media/blog storage services like Azure Media or Azure Storage and embedding the media URL inside the app is highly suggested.

14. What is a collection?
    A Collection is a unique form of data source because it is not connected to a cloud service but rather is local to the app. This is usually utilised as the device's local storage, and it can't be shared between devices for one or numerous users. They can be saved and accessed locally as well. Clear function, ClearCollect, and Collect are used to manage collections.


15. In PowerApps, how can separate user environments be created?
    The location where data, apps, and business processes are stored, managed, and shared is referred to as an environment. It can also be thought of as a container that separates apps according to their target audiences, security requirements, and responsibilities. Creating or selecting the environment to be used, on the other hand, is mostly dependent on the company and the apps you intend to develop.

16. In PowerApps, how do you define or use a local or global variable?
    The Set function is used to set the value of the global variable. This stores a piece of data momentarily, such as the outcome of operational data or the number of times a button has been pushed. The content variable is then created using the UpdateContext function, which temporarily stores information. Context variables (also known as local variables) are exclusively available on that screen; the value cannot be accessed from any other screen.

Syntax for local variable:

UpdateContext( { ContextVariable1: Value1 [, ContextVariable2: Value2 [, … ] ] } );
Example:

UpdateContext( { Name: “rose”, Score: 10 } );
Syntax for global variable:

Set( VariableName, Value );
Example:

Set( Counter, 1 );
17. How may a distinct user environment be created in PowerApps?
    An environment is a location where your company's business data, apps, and flows are stored, managed, and shared. It can also be thought of as a container that can be used to separate programs with distinct roles, security needs, or target audiences. The way you use the environments is determined by your company and the apps you're aiming to create.

You can create an environment with a Dataverse database. To utilise Dataverse as data storage, you must first construct a database. The Dataverse is a cloud-based database that securely stores data for Power Apps-based business applications. Dataverse offers not only data storage but also a mechanism to apply business logic to the data, such as business rules and automation. You can also construct an environment that doesn't require a database and instead uses your own data storage.


18. Is it possible to use several data sources in a single canvas app?
    Yes, it is correct. Any number of connections can be made using Power Apps, and once they're made with an account, any number of data sources can be used in a single program.

19. Is Flow reliant on Power Apps, or does Power Apps rely on Flow?
    It's extremely simple to get mixed up on this. PowerApps is a new version of the solution that allows you to create a mobile-oriented app that is routed to SharePoint for forms. PowerApps extensively uses the Flow, but it is not essential. Flow, on the other hand, can use Power Apps and does so frequently as a frontend for its work, but it does not require them.

20. What are the different license choices available for the Microsoft Power Platform's Storage features?
    Storage capacity is provided by three types of licenses:

Dataverse for Apps Database capacity.
Dataverse for Apps File capacity.
Dataverse for Apps Log capacity.
21. How can PowerApps benefit your company?
    Workflow, automation, data visualisation and reporting, collaboration, and other activities may all be handled using PowerApps. Teams, field workers, your management team, and even your consumers could be involved. The use cases might range from the simple to the complicated. You can improve your fundamentals while simultaneously being incredibly inventive. PowerApps can be accessed through a mobile app, a website, or an Office 365 product like Microsoft Teams.

The numerous ways to automate business operations, which includes many PowerApps-based solutions, such as:

App for onboarding new employees: Power Apps' ability to communicate with other Office 365 workloads and access data from services like Outlook, tasks, and calendars is an important capability. Many businesses utilise the free Power Apps template to construct an onboarding tasks app that aids HR and new workers during the onboarding process. These apps give new employees various tools, such as connections to policy manuals, team member contact information, and forms new employees can use to create their internal profiles.
Speeds up the transformation of businesses: One of the biggest advantages of Power Apps is how quickly your company can create a professional app. Businesses are no longer reliant on IT. When compared to traditional development processes, developing and deploying an app using Power Apps is substantially faster, especially if your IT team has a huge backlog of projects. The low-code platform features a simple drag-and-drop interface with pre-built templates, allowing you to quickly design an interface, link your data, and more.
New user configuration scenarios: Power Apps is also an excellent tool for streamlining new user setup. It provides recruiting managers with simple intake forms to fill out and submit to the appropriate departments for new hires. For process automation and approval, several firms are merging PowerApps forms with Microsoft Flow. Power Apps' ability to communicate with other Office 365 workloads and access data in services like Outlook, tasks, and calendars is a key capability.
Apps are fully secure to use: Power Apps-created custom apps are incredibly safe. These apps and workflows integrate with Azure Active Directory and other Microsoft security technologies, such as Common Data Services (CDS), which offers a role-based security paradigm. End-users only see what's relevant to them since you may regulate rights at the data and application levels. Apps developed on the CDS are likewise GDPR-compliant by default.
22. Explain the concept of security roles in Power Apps.
    In Power Platform, Security Roles are used to providing authorization levels for certain users or teams. The rights and access levels for each security role must be configured.

Security roles can be used to configure access to specific apps and data in the environment, or they can be used to configure environment-wide access to all resources in the environment. Through a set of access levels and permissions, security roles manage a user's access to an environment's resources. The constraints on the user's view of apps and data, as well as the user's interactions with that data, are determined by the combination of access levels and permissions specified in a certain security role.

23. What is the purpose of DLP Policies?
    We can design Data Loss Prevention(DLP) policies that act as guardrails to keep organisational data from being exposed unintentionally. You must be a tenant admin or have the Environment Admin role to use this feature.


24. What is the purpose of the Patch Function feature in canvas apps?
    Users can create their power apps with the power apps canvas app. Power users can choose from a list of functions in power apps and use the ones they want.

When many requirements in one power app must all be met, the user must go through all of the power apps and then utilise the power apps patch feature. Using an if-then statement, the power apps patch function allows users to combine numerous power apps into a single power app.

25. What kind of company should use Power Apps?
    Power Apps is designed for companies of all sizes. It will enable you to design apps that are tailored to your specific needs; this is true for small, medium, and large enterprises alike. This holds regardless of the industry in which your business operates.

26. Is it necessary to learn to code?
    The Power Apps platform was created to allow anyone who isn’t a programmer to create their apps. As a result, learning to code is entirely unnecessary. To make things even easier, you can use one of the many pre-defined templates available in the PowerApps library. Then you can personalise it to create an application that is tailored to your requirements.

27. What are some examples of Microsoft PowerApps Use Cases?
    You may use Power Apps to construct applications that help you collect data more efficiently daily.

You could, for example, make an application that allows you to accomplish the following:

Make it easy for your employees to enter information about their working hours.
Allowing you to obtain expense accounts from each employee can help you manage expenses more effectively.
Allows your subcontractors to submit control notes into your database directly (for example, for the regular checking of the condition of your equipment)
Unlike traditional development, Power Apps has the distinct advantage of being able to be produced and released quickly. Companies now can respond to their customers' needs swiftly and independently.
28. What is Dataverse?
    Dataverse is a data platform included with Power Apps that let you store and model business data. Dynamics 365 apps (such as Dynamics 365 Sales, Customer Service, Field Service, Marketing, and Project Service Automation) is created on this platform. Your data is already in Dataverse if you're a Dynamics 365 customer.

Dataverse allows you to securely store and manage data in a collection of standard and custom tables, with the ability to add columns as needed.

29. What are PowerApps Portals, and what do they do?
    The newest type, Power Apps Portals, is more focused on website design. In simple terms, a Portal is to web design what a Canvas app is to app design.

It's a simpler approach for users to develop external-facing websites with a simple studio and expose data to customers and vendors (who can be guests and don't need to check in). You may also play around with the CSS if you want to get a little more technical.

Portals and model-driven apps have a lot in common in that they're both built on Dataverse and have access to the same pool of Dataverse components (Views, Forms, and so on) as well as the same data.


30. What are the benefits of the Microsoft PowerApps Portal?
    The advantages of the PowerApps Portal are numerous, but the following are the most compelling:

Increased satisfaction among customers, partners, and employees.
Improved business outcomes as a result of better, faster, and more informed decision-making.
Integration with Power BI and other Microsoft applications, like SharePoint, provide added value.
Enhanced security features and efforts to safeguard sensitive client information.
It engages with external users, that is, it grants safe access to your data to internal and external users, either anonymously or through commercial authentication services such as LinkedIn, Facebook, Microsoft, or enterprise providers.
It combines your data and adds forms, charts, and dashboards to your portal.
It allows secure access to your data to internal and external users, either anonymously or through commercial authentication services like LinkedIn, Facebook, Microsoft, or enterprise providers.
It connects your data, that is, it combines your data to add forms, charts, and dashboards to your portal.
31. How do you ensure the versioning of a canvas app in a collaborative setting when there are frequent updates?
    A version-specific message or comment can be left while saving the app. We may also put a label on the app's Home screen to symbolise a version number that the app maker can manually update.

32. What Can't PowerApps Do? What Sets It Apart From Others?
    PowerApps are designed to be utilised within a company. It improves scalability, robustness, and performance while also making business app development easier. PowerApps, in conjunction with Microsoft Flow and Power BI, has been demonstrated to be the greatest solution for small businesses since it scales as your company grows. Because PowerApps cannot be shared with everyone, they cannot be utilised publicly. It also has 'no-code' functionality, which means that no further JavaScript or HTML can be added. This feature improves development speed overall, but it also limits developers to using only inbuilt templates and connectors.

33. How to connect to SharePoint from a canvas app?
    Connect to a SharePoint site to instantly produce an app from a custom list, or create a connection before adding data to an existing app or creating a new one.

You can use one or both of these methods, depending on where your data is stored:

In a SharePoint Online or on-premises site, display data from a custom list.
In a library, you can display photos and play video or music files (SharePoint Online only).
Power Apps can automatically create a three-screen app for you if you want to handle data in a custom list. On the first screen, users can explore the list; on the second screen, they can view item information; and on the third screen, they can create or amend things.

Establish a Connection:

Sign in to Power Apps, then go to Data > Connections in the left menu bar, then New connection in the upper-left corner.
Choose SharePoint.
Perform one of the following sets of steps:
Select Connect directly (cloud services), Create, and then provide credentials to connect to SharePoint Online (if prompted). After you've established the connection, you can either add data to an existing app or start from scratch.
Select Connect using an on-premises data gateway to connect to an on-premises location. After that, select Windows as the authentication type and enter your credentials. (Specify domain/alias if your credentials include a domain name.)
Select the gateway you want to use under Choose a gateway, and then click Create.
After you've established the connection, you can either add data to an existing app or start from scratch.


Power Apps Interview Questions for Experienced
34. Explain the error function in PowerApps?
    When a record of a data source is modified, errors can occur. Network failures, insufficient permissions, and edit conflicts are all possibilities.

The Patch and other data functions do not return errors directly. They instead return the outcome of their operation. You can use the Errors function to get the details of any errors that occur after a data function has been completed. The [IsEmpty] function in the formula IsEmpty( Errors (...) ) can be used to check for errors. Using the Validate and DataSourceInfo functions, you can prevent some mistakes from occurring. For additional information on how to work with and avoid errors, see Working with Data Sources.

The Errors function returns a table of errors with the columns listed below:

Record: The data source record that included the error. This field will be blank if the mistake occurred during the record creation process.
Column: If the issue can be traced back to a single column, here is the column that caused it. Otherwise, this will be left blank.
Message: An explanation of the problem. For the end-user, this error string can be displayed. Be aware that the data source may generate this message, which may be long and contain raw column names that the user may not understand.
Error: An error code that can be used in formulas to assist in the resolution of the problem. Syntax: Errors( DataSource [, Record ] )
DataSource: This is a must-have. The data source for which you'd like to get error messages.
Record: It is optional. You wish to return errors for a specific record. If this parameter is omitted, the function will return errors for the full data source.
35. In PowerApps, how can I cache data?
    To access this feature, go to https://make.PowerApps.com > Apps > Other > Choose your Portal application and click on Settings and then administration from the drop-down menu. Select Portal Actions from the left menu and select Restart: The website app service will be restarted, and the server-side cache will be cleared.

36. In PowerApps, how do I store an attachment?
    Then, to enable attachments, you must:

Choose the forms to which you'd like to add attachments.
To open the data panel, click the Data box in the properties pane.
Find the Attachment field in the list of fields and turn it on.
Make a backup of your app and then publish it.
37. What's the difference between PowerApps and Power Automate?
    Microsoft PowerApps is largely a form design tool, whereas Microsoft Power Automate is a workflow and process automation program. They're individual items that can be mixed and matched.

38. How do you add components to a canvas app?
    To get started, go to PowerApps Studio.

Create a new canvas app or update an existing app with the code component to which you wish to add it.
Select Add (+) in the left pane, and then Get more components in the right pane.
Select the Code tab, then Import after selecting a component from the list.
39. What is the purpose of the Power Apps Loading Spinner?
    In PowerApps, the Loading Spinner is an animated element that indicates when loading is underway. The loading spinner will display if the data loading is taking too long. This means that it aids in informing the user that the procedure is busy and that it may take some time to appear.

In the Advanced tab, as well as the Dropdown in the top left of the application, Microsoft offered a property named "LoadingSpinner."

When you set the loading spinner attribute to data, a loading spinner will appear anytime a user opens the screen.


40. In what programming language is PowerApps written in?
    Microsoft Power Fx is a low-level programming language that may be used to express logic throughout the Microsoft Power Platform. It's the same language that's at the heart of today's Microsoft PowerApps canvas programs, and it's inspired by Microsoft Excel," said Greg Lindhorst, a Microsoft Principal Program Manager.

41. What can I do to increase the performance of my PowerApps?
    The performance of PowerApps can e increased in the following ways:

Data connections should be limited: Don't use the same app to connect to more than 30 data sources. Apps require new users to sign in to each connection, thus each additional connector lengthens the time it takes for the program to load. When an app requests data from a source, each connector takes CPU resources, memory, and network bandwidth.
Reduce the number of controls used: Add no more than 500 controls to a single app. To render each control, Power Apps creates an HTML document object model. The more controls you include, the longer PowerApps takes to generate.
Improve the OnStart property's performance: If data doesn't change during the user session, use the ClearCollect function to cache it locally. Use the Concurrent function to load data sources at the same time, which can cut the time it takes for an app to load data in half.
Lookup data is cached: To prevent continually retrieving data from the source, use the Set function to cache data from lookup tables locally. If the data is unlikely to change during a session, this strategy improves performance.
Avoid screen-to-screen control reliance: Avoid screen-to-screen formula dependencies. You can exchange information between screens in some circumstances by using a global variable or collection.
Make use of delegation: Instead of retrieving data to the local device for processing, utilise functions that delegate data processing to the data source. When an app must analyse data locally, it requires significantly more processing power, memory, and network traffic, particularly if the dataset is huge.
Avoid using the same formula over and over again: Consider setting the formula once and then referencing the outcome of the first property in future ones if many properties run the same formula (especially if it's complicated).
DelayOutput should be enabled for all Text input controls: Set the DelayedOutput attribute of a Text input control to true if you have numerous formulas or rules that reference the value of that control. Only when a string of keystrokes has been entered in rapid succession will the Text attribute of that control be updated. The formulae or rules will not be executed as frequently, and the app's performance will improve.
42. What are the drawbacks of using PowerApps?
    PowerApps have the following limitations:

Under the Microsoft 365 umbrella, licensing is restricted.
A convoluted licensing scheme.
It is costly.
Support for a variety of device sizes and screen orientations is limited.
The number of items allowed is limited.
The connector ecosystem's throughput limits is another limitation of PowerApps.
SharePoint as a back-end will function perfectly with attachment control. Attachment control will be disabled if custom SQL is used. Use OneDrive, SharePoint, or other cloud storage to store attachments and refer to them in PowerApps as a workaround.
JavaScript isn't supported in PowerApps forms.
43. What Is A DataStore And How Does It Work? What Events Does It Now Support/No Longer Support?
    It's a statistics window that can't be seen. If you wish to retrieve records from a desk without having to show it, for example, you may pass for a statistics store. It no longer guides clicked events, but now assists with deleting row (), inserting a row (), retrieving row (), and updating row ().  It also supports the Item Error () event.

44. What is a Combo Box? What distinguishes it from Drop-down?
    In the PowerApps canvas software, a combo box is a form of control. A Combo box control also allows you to search for the items you want to select. Furthermore, because the search takes place on the server, the performance of this search tool is unaffected. When looking for items to pick, you can change the Layout options in the Data pane to show a single data value, two values, or an image and two values (Person) for each item.

Another sort of control offered in PowerApps is a drop-down menu. This control saves screen space, which is especially useful when the list has a lot of options.

Unless the user selects the chevron to show more options, the control only takes up one line. A maximum of 500 things will be displayed in the control.


45. What is the meaning of the Environment variable? How do you make one?
    Environment variables are produced in PowerApps for each environment and store the parameter keys and values. Furthermore, these variables are used as input to a variety of other application objects.

This method allows you to separate the parameters from the consuming objects and alter the values within the same environment or when migrating solutions to different environments.

The following are some of the advantages of using environmental variables:

While importing solutions to various environments, provide new parameter values.
Save settings for canvas apps and flows' data sources. You can, for example, keep SharePoint Online site and list parameters in environment variables, allowing you to connect to different sites and lists in different environments without having to change the apps or flows.
Continuous integration and continuous delivery (CI/CD) are enabled by SolutionPackager and DevOps tools.
The environment variables can be unpacked and saved in source control. You can also save different environment variables values files for the varied configurations required in various environments. The file matching to the environment where the solution will be imported can then be accepted by Solution Packager.

The steps to create an environment variable in a solution are:

Sign in to Power Apps (make.powerapps.com) and then click Solutions from the left pane.
Create a new solution or open the one you want.
Select New > More from the command bar, then the Environment variable.
Complete the following columns in the right pane, then click Save:
Display name: Give the environment variable a name.
Name: The unique name is produced automatically from the Display name, however, you can alter it if you want.
Data type: Decimal number, Text, JSON, Two options, Data source, or Secret are the possibilities available.
Current value: Also referred to as the value. This property is a part of the environment variable value table and is optional. Even if a default value is provided, if a value is available, it will be used. If you don't want to use the value in the next environment, remove it from your solution. Within the exported solution.zip file, the values are also divided into distinct JSON files that can be changed offline.
The default value: This column is not necessary and is part of the environment variable definition table. If there is no current value, the default value is used.
46. What context does the power app/automate run in? In powerapps, how can you get impersonation/elevated privileges?
    Power apps run in the context of the current user.

If your flow is triggered by an automatic event, it will always operate in the context of a flow owner (Who created the flow). Manually triggered flows, such as those that begin with a button in a PowerApp, however, execute in the context of the person who clicks the button.

Although there is no default impersonation action, we can create two flows in which Flow A is called when a power app button is pressed and passes HTTP request data to Flow B. This is when we pass data that is critical to the business logic, lose all context knowledge, and impersonate the user.

47. How to export to excel in PowerApps?
    Because there is no direct function in PowerApps, we must use a flow to do this.

Create a button in PowerApps and link it to a flow when the button is pressed.
As a parameter, pass JSON data to the flow. To save the JSON data to excel in a SharePoint site, use the create CSV and create file actions in the flow. To communicate back the URL of our Excel file to Power App, use the react to power app action.
When the power app receives the Excel link, it uses the download function to save the file.
48. Explain concurrent function.
    Multiple formulas are evaluated at the same time using the Concurrent function. Multiple formulas are usually evaluated by chaining them together with the ; operator, which evaluates each one in turn. Users wait for less for the same outcome when the app executes activities concurrently.

Syntax for concurrent function: Concurrent( Formula1, Formula2 [, ...] )

Formula(s) – These are required. Formulas for evaluating multiple variables at the same time. At least two formulas must be provided.

We can utilise the Concurrent function to run many formulas simultaneously. Instead of utilising numerous formulas with a semicolon (;), you can use Concurrent to collect data from many tables during Page Load, which will significantly shorten the overall load time of the screen.


49. Give an example of how to use the LookUp() and Filter() function. What distinguishes it from Filter()?
    The LookUp() function locates the first record in a database that meets a formula's requirements. LookUp() can be used to locate a single record that meets one or more criteria.
    Filter(), on the other hand, retrieves all records/items from a database that meet the criteria.

LookUp(Table*, Formula [, ReductionFormula]) is the syntax for LookUp() function.
Example:

LookUp(Cake, Flavour = “Chocolate”, Quantity)
Filter(Table*, Formula1 [, Formula2, … ] ) is the syntax for Filter() function.
Example:

Filter(cake, “chocolate” in Lower(Flavour ));
50. What is the difference between the PowerApps functions IsMatch, Match, and MatchAll?
    The IsMatch method returns True or False depending on whether a string matches a pattern, which is usually done via a regular expression. The first record that matches a pattern is returned by the Match function. For each match discovered, the MatchAll method returns a table.

51. What is the difference between an action and a trigger in MS-Flow?
    Action: Changes guided by a User are referred to as actions. For example, you can utilise an action to do SQL Database operations such as lookup, update, and remove data. All actions will have direct mappings to Swagger operations.
    Trigger: Several connectors have triggers that can be used to notify your app when certain events occur. Let's look at an FTP connector with the OnUpdatedFile trigger as an example. You can create a Logic App or a flow that listens for this trigger and takes action whenever it occurs.
    The trigger is divided into two categories:
    Polling Trigger: These triggers can check for new data by calling your service at a specific interval. When fresh data becomes available, your workflow instance will be restarted with the new data as input.
    Push Trigger: These triggers can listen for data on an endpoint, which implies they'll wait for something to happen. The event triggers a fresh execution of your workflow instance whenever it occurs.
52. How do I use the canvas components in my apps?
    Components are reusable building blocks for canvas apps, allowing app developers to design custom controls and reuse them across several apps. Components can be exported and imported between apps in different organisations. The Components are useful since they allow you to create larger programs with similar control patterns. For example, we may create a navigation control that can be used across multiple screens in our program. When you update a component, your changes will be reflected in all instances of the app.

Components ensure that performance is upgraded or improved, as well as assisting in the standardisation of the appearance and feel of PowerApps apps across an enterprise. The input attributes of a component are also capable of receiving values from the app, and the component can use these internally. Output attributes, which are capable of giving output values to the app, are also included in components.

53. In PowerApps, how can Error Handling be implemented?
    If there is a mistake while sending the feedback, the app will display an appropriate message. This will assist the salesman in determining what went wrong and how to proceed. The Canvas App introduces the 'IfError' and 'isError' functions to handle errors and display the relevant message.

To use these functions, Formula-level error management must be enabled. Please follow the steps below to enable Formula-level error management:

To begin, open the Canvas App and select File.
Go to Advanced Settings under Settings.
Enable Formula-level error management.
54. Explain SaveData, LoadData and ClearData functions.
    The SaveData function saves a collection under a name for later use.
    The LoadData function reloads a collection that was previously saved with the SaveData function. This function cannot be used to load a collection from another source.
    ClearData clears the storage associated with a given name, or all storage linked with the application if no name is provided.
    Syntax for SaveData, LoadData and ClearData functions:

SaveData ( Collection, Name )

LoadData ( Collection, Name [, IgnoreNonexistentFile ])

Note:
The collection is a must. To be stored or loaded, a collection must be made.

Name - This is required. The storage's name. To store and load the same collection of data, the name must be the same. Other programs or users do not have access to the namespace. Any of the following characters must not appear in a name: *".?:\<>|/.

IgnoreNonexistent Optional file. If the file doesn't already exist, a Boolean value indicates what to do. To return an error, use false (the default), and to silence the error, use true.

ClearData  ( [Name] )

Name - This is an optional field. SaveData already saved the name of the storage. All storage connected with the app is wiped if the Name is not specified.

55. In PowerApps, what does delegation mean?
    The key to developing efficient apps is to keep the amount of data on your device to a minimum. Maybe you only need a few hundred records out of a million, or maybe a single aggregate value might represent thousands of entries. When the expressiveness of PowerApps formulas meets the requirement to reduce data movement across the network, delegation is the result. In other words, rather than bringing data to the app for processing locally, Power Apps will delegate data processing to the data source.

The next stage is to limit your use of formulas to those that can be delegated. The formula elements that can be delegated are listed here. However, each data source is unique, and not all of these elements are supported by all of them. In your specific formula, look for delegation warnings.


Filtering, searching, and looking up information can all be delegated.
It's possible to delegate Sort and SortByColumns. The formula in Sort can only be the name of one column and cannot contain any additional operators or functions.
Sum, Average, Min, and Max are all tasks that can be delegated. At this moment, only a small number of data sources support this delegation; see the delegation list for further information.
CountRows, CountA, and Count are all counting functions that cannot be delegated.
StdevP and VarP are two other aggregate functions that cannot be delegated.
Conclusion
As you may be aware, there is a significant need for application development because clients expect fresh developments and advancements. Business organisations are continuing their efforts by ensuring that the correct language is used to implement their initiatives or innovations. As a result, hunting for people who are knowledgeable or skilled has become commonplace these days. And I'm sure you're hoping to ace the interview and land one of the jobs. These interview questions will undoubtedly assist you in securing a job.

Useful Resources:

Power BI Interview Questions
SharePoint Interview Questions






### references
#### links
- <https://www.interviewbit.com/power-apps-interview-questions/>