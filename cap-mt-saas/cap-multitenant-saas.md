<!-- [IMPORTANT] Do not remove the comments below. These comments are necessary for importing the content to DC -->

<!-- dc-ref-arch-metadata : 
    {
        "id": "ref-arch-cap-multitenant-saas",
        "name": "CAP-Based Multitenant SaaS Application Development",
        "shortDescription": "Develop Multitenant Software-as-a-Service application using Cloud Application Programming Model leveraging  Kyma and Cloud Foundry Runtimes on SAP BTP",
        "archDiagramLink": "images/Susaas_App_Architecture_ExpertCf.png",
        "tags": "Application Development",
        "category": "Application Development"
    }
dc-ref-arch-metadata  -->

<!-- dc-ref-arch-detail-page-start -->
## **CAP-Based Multitenant SaaS Application Development leveraging  Kyma and Cloud Foundry Runtimes on SAP BTP**

Multitenancy is an important architectural concept used in SaaS application development in which a single instance of an application serves multiple customers (tenants). Multiple customers share computing resources that is physically integrated but logically separated.

This reference architecture is a comprehensive architecture designed to guide developers, partners, and customers in building multitenant Software-as-a-Service (SaaS) applications using the SAP Cloud Application Programming Model (CAP). This demonstrates the development and deployment of a multitenant application on the SAP BTP with integration to multiple BTP services and business systems like SAP S/4 HANA leveraging both Cloud Foundry and Kyma runtimes.

### Flow (Mandatory)

-   #### Subscription and Consumer Access flow   
    1.  For each customer, a subaccount (consumer subaccount) is created, and an instance of the SaaS application is subscribed, triggering the subscription process via SAP SaaS Provisioning Service.   
    2.   During this process, the CAP framework creates a HANA HDI container instance via the SAP Manager service, which can be extended with creation of specific services or components of the SaaS application, such as IAS instance integration or SaaS API Broker registration. Upon successful subscription, a unique (approuter) URL is provided for each customer.     
    3.  As part of the application setup, destinations can be configured in the consumer subaccount to connect to SAP ERP systems or third-party systems, if needed. Additionally, one consumer admin user is added by the SaaS provider, who can then add more users and assign roles as needed for accessing the SaaS application.    
    4.  Users access the application via the (approuter) URL, which redirects them for authentication. Once logged in, the SaaS application (UI component) is loaded based on the user's authorization.    
    5.  In the SaaS application, data is loaded from the CAP Business Application Service, which retrieves data from the HANA HDI container instance created during subscription, as well as from SAP ERP systems or third-party systems using destinations configured in the consumer subaccount via the Destination Service.     

-   #### SaaS Service API flow    
    1.  After subscribing to a SaaS application in the Consumer Subaccount, an instance of the API service broker with the necessary plan is creared. The Service Broker is automatically registered in the Tenant Subaccount during the subscription/provisioning process. Note that roles can be assigned and/or features can be enabled/disabled according to the plan.   
    2.  Then, a new Service Binding is created which will provide necessary credentials to call CAP based SaaS APIs that can be used by API clients like SAP S/4 HANA or any third party tool. It allowes SaaS consumers to interact programmatically with their data stored in specific HDI containers.   
    3.  Depending on the plan, different API policies, such as rate limiting, maximum body content, and quota policies, can be applied using the SAP API management component of the SAP Integration Suite.

### Characteristics (Mandatory)

-   **Multitenancy**: CAP has built-in support for multitenancy with [@sap/cds-mtxs](https://www.npmjs.com/package/@sap/cds-mtxs) package. This package facilitates handling subscribe/unsubscribe events from the SAP BTP SaaS provisioning Service, and also manages SAP HANA database containers by connecting to the SAP Service Manager.

-   **Consumer Extensibility**: Consumer-driven customization enhances customer experience and satisfaction by offering tailored extensibility. CAP incorporates built-in extension capabilities that enable SaaS consumers to seamlessly integrate additional functionalities and custom extensions according to their specific requirements. This enhances flexibility and adaptability, ensuring that the SaaS solution efficiently meets diverse business needs.

-   **User Management**: Central User Management using Identity Authentication Service (IAS) for a multi-tenant SaaS application provides streamlined user and role management, enhances security through robust authentication, and simplifies the integration with SAP BTP, ensuring a more efficient and secure user management process. This makes your solution independent from SAP ID Service, which requires users of your SaaS consumers to sign up for an SAP-managed user account

-   **API Service Broker**: the service broker is responsible of creating SaaS API service instances in the Subscriber Subaccounts. Using these service instances, subscribers can then create so called service bindings, providing them with Client Credentials to interact with the SaaS API. Service Brokers facilitate secure access control and role management, ensuring secure multi-tenant environment and access to customer data.

-   **Custom Domain**: it enhances brand identity by using personalized URLs, improves user trust and experience. Additionally, custom domains offer more flexibility and control over domain management and security settings.


### Examples in an SAP context (Mandatory)

SAP Partners use the Business Technology Platform (BTP) to create specialized SaaS solutions for various industries. This reference architecture helps ensure their cloud applications are strong and adaptable. It includes guidelines for security, data management, and integrating with other systems, which speeds up development and improves operations. Following this approach, SAP Partners may offer high-quality SaaS solutions tailored to each industry's needs, addressing specific business challenges in today's dynamic market.

Additionally, the multitenant architecture introduced on SAP Business Technology Platform (BTP) is utilized in [Circelligence by BCG](https://store.sap.com/dcp/en/product/display-2001014822_live_v1/circelligence-by-bcg). Circelligence by BCG, a partner product, uses this architecture to measure how products are used by its customers.

### Reasonable alternatives (Optional)

<!-- dc-ref-arch-detail-page-end -->

### Services and Components (Mandatory)

<!-- dc-ref-arch-services-start -->
-   [SAP BTP, Cloud Foundry Runtime](https://discovery-center.cloud.sap/serviceCatalog/cloud-foundry-runtime?region=all)
-   [SAP BTP, Kyma Runtime](https://discovery-center.cloud.sap/serviceCatalog/kyma-runtime?region=all&tab=feature)
-   [Application Autoscaler	Standard](https://discovery-center.cloud.sap/serviceCatalog/application-autoscaler/?service_plan=standard&region=all&commercialModel=cloud)
-   [Destination Service](https://discovery-center.cloud.sap/serviceCatalog/destination?service_plan=lite&region=all&commercialModel=cloud)
-   [SAP Alert Notification service](https://discovery-center.cloud.sap/serviceCatalog/alert-notification?region=all)
-   [SAP Application Logging Service](https://discovery-center.cloud.sap/serviceCatalog/application-logging-service/?region=all)
-   [SAP Cloud Identity Services](https://discovery-center.cloud.sap/serviceCatalog/identity-authentication?region=all)
-   [SAP Authorization and Trust Management Service](https://discovery-center.cloud.sap/serviceCatalog/authorization-and-trust-management-service?region=all&tab=feature)
-   [SAP Cloud Management Service](https://discovery-center.cloud.sap/serviceCatalog/cloud-management-service/?region=all)
-   [SAP Credential Store](https://discovery-center.cloud.sap/serviceCatalog/credential-store?region=all)
-   [SAP HTML5 Application Repository Service](https://discovery-center.cloud.sap/serviceCatalog/html5-application-repository-service?region=all) 
-   [SAP SaaS Provisioning Service](https://discovery-center.cloud.sap/serviceCatalog/saas-provisioning-service?service_plan=application&region=all&commercialModel=cloud)
-   [SAP HANA Cloud	hana-free](https://discovery-center.cloud.sap/serviceCatalog/sap-hana-cloud?tab=customerreference&region=all)
-   [SAP Service Manager](https://discovery-center.cloud.sap/serviceCatalog/service-manager/?region=all)
<!-- dc-ref-arch-services-end -->

### Resources (Mandatory)

<!-- dc-ref-arch-resources-start -->
-   [Reference Application : SAP Samples | GitHub ](https://github.com/SAP-samples/btp-cap-multitenant-saas/tree/main)
-   [Developing Multitenant Applications in the Cloud Foundry Environment](https://help.sap.com/docs/btp/sap-business-technology-platform/developing-multitenant-applications-in-cloud-foundry-environment)
<!-- dc-ref-arch-resources-end -->

### Related Missions (Optional)

<!-- dc-ref-arch-related-missions-start -->
-   [Develop a multitenant SaaS application on SAP BTP using CAP](https://discovery-center.cloud.sap/missiondetail/4064/)
-   [Develop a CAP-based (multitenant) application using GenAI and RAG](https://discovery-center.cloud.sap/missiondetail/4371/)
<!-- dc-ref-arch-related-missions-end -->
