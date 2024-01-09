<p><strong><span style="font-size:13.999999999999998pt;">PSP(Chargebee) Integration High-Level System Architecture</span></strong></p>
<p><br></p>
<p><u><span style="font-size:11pt;">Backend:</span></u><span style="font-size:11pt;">&nbsp;.NET Core for microservices.</span></p>
<p><u><span style="font-size:11pt;">Database:</span></u><span style="font-size:11pt;">&nbsp;Azure Cosmos DB with MongoDB API. (Azure Cosmos DB provides compatibility with the MongoDB API, which means you can use existing MongoDB libraries, drivers, and tools to interact with Azure Cosmos DB.)</span></p>
<p><u><span style="font-size:11pt;">API Gateway:</span></u><span style="font-size:11pt;">&nbsp;Azure API Management. Can be used together with Azure API Gateway.&nbsp;</span></p>
<p><u><span style="font-size:11pt;">Message Queue:</span></u><span style="font-size:11pt;">&nbsp;Azure Service Bus. (Apache Kafka is also a nice option) (Azure Service Bus would likely be the best fit but Azure Event Hubs are an option too especially when we need to quickly accept events (millions) from end-users.)</span></p>
<p><u><span style="font-size:11pt;">Authentication:</span></u><span style="font-size:11pt;">&nbsp;OAuth or JWT.</span></p>
<p><u><span style="font-size:11pt;">Containerization:</span></u><span style="font-size:11pt;">&nbsp;Docker (if needed for local development or deployment). Azure Kubernetes Service for orchestration</span></p>
<p><u><span style="font-size:11pt;">API Documentation:</span></u><span style="font-size:11pt;">&nbsp;</span><span style="color:#1d1c1d;background-color:#ffffff;font-size:11.5pt;">Azure APIM also provides API documentation which we can import via OpenAPI specification</span></p>
<p><u><span style="font-size:11pt;">Storage for sensitive information:</span></u><span style="font-size:11pt;">&nbsp;Azure Key Vault. Secure all services inside a VNET and communication is primarily via APIM (Azure API Management). Also, leverage&nbsp;</span><em><span style="font-size:11pt;">Azure Managed Identity</span></em><span style="font-size:11pt;">&nbsp;to completely eliminate handling of secure strings where possible.</span></p>
<p><u><span style="font-size:11pt;">Monitoring:&nbsp;</span></u><span style="font-size:11pt;">Use tools like Prometheus, Azure Application Insights and Grafana for monitoring microservices and infrastructure.</span></p>
<p><u><span style="font-size:11pt;">Email Infrastructure:</span></u><span style="font-size:11pt;">&nbsp;SendGrid</span></p>
<p><u><span style="font-size:11pt;">Payment system:</span></u><span style="font-size:11pt;">&nbsp;Chargebee as PSP</span></p>
<p><br></p>
<p><strong><span style="font-size:11pt;">High Availability and Disaster Recovery Plan</span></strong></p>
<p><span style="font-size:11pt;">High Availability:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Utilize Azure Availability Sets for VMs and AKS for microservices to ensure redundancy. (Deploy resources across multiple zones)</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Microservices can be deployed and scaled independently, allowing for optimal resource allocation and handling increased load. (Autoscaling configured for microservices based on demand.)</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Docker for easy deployment and scaling.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Container Orchestration (Azure Kubernetes Service - AKS):</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Deploy microservices as containers for scalability and manageability.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Disaster Recovery:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Regularly backup Azure Cosmos DB to Azure Blob Storage for quick recovery in case of data loss.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Use Azure Site Recovery for VM-level disaster recovery.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Implement geographically distributed data centers for additional redundancy.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Runbook Documentation: Develop runbooks with detailed procedures for recovery in case of a disaster.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Logging and Monitoring (Azure Application Insights):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Use Azure Application Insights for real-time monitoring microservice performance, troubleshooting and logs. Splunk, New Relic, Datadog, ELK (Elasticsearch, Logstash, Kibana) Stack (for centralized logging, analyzing user actions, and troubleshooting issues) , Prometheus, Grafana (Prometheus and Grafana for monitoring system health, resource usage, and performance metrics) can also be options</span></p>
    </li>
</ul>
<p><br></p>
<p><br></p>
<p><br></p>
<p><span style="font-size:11pt;">API Gateway (Azure API Management):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Azure API Gateway to manage and route requests. Acts as a single entry point for clients.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Responsible for authentication, rate limiting, request validation, and routing to appropriate microservices.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Load Balancer (Azure Load Balancer) (not a must):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Azure Load Balancer for distributing incoming traffic across multiple instances of microservices for scalability and high availability. It can reroute traffic away from unhealthy instances, preventing them from affecting overall system performance. NGINX can be used as well.&nbsp;</span></p>
    </li>
</ul>
<p><br></p>
<p><span style="font-size:11pt;">** The combination of an API Gateway and Load Balancer allows for both vertical and horizontal scalability, ensuring the system can handle increased loads efficiently. API Gateway enhances security by handling authentication and authorization, while the Load Balancer contributes to system resilience and fault tolerance. Separating concerns between API management and traffic distribution provides a modular and more easily maintainable architecture.Centralized monitoring and logging through the API Gateway help in tracking and diagnosing issues, while the Load Balancer ensures even distribution of traffic for optimal performance.&nbsp;</span><em><span style="font-size:11pt;">Azure API Management alone may be sufficient, especially if the APIs are not distributed across multiple backend servers.</span></em></p>
<p><br></p>
<p><br></p>
<p><strong><span style="font-size:11pt;">Security Risks and Mitigations</span></strong></p>
<p><span style="font-size:11pt;">Data Breach:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Implement encryption at rest, use secure connections (HTTPS) by ensuring Azure App Service is configured to use a valid SSL/TLS certificate, and regularly update security patches.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Unauthorized Access:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Implement OAuth or JWT for authentication, RBAC for microservices access (authorization), and secure API key management.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Secure Key Management:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Store and manage sensitive information such as API keys and secrets in Azure Key Vault. (managed identity)</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Denial of Service (DoS) Attacks:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Utilize Azure DDoS Protection.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Implement rate limiting and throttling (via API Gateway/ APIM).</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Webhook Security:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Use secure HTTPS for webhook communication.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Validate and verify incoming webhook payloads from Chargebee or any other 3rd party.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Anti Fraud - block fraudsters from signing up (without knowing who they are):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">ChargeBee is detecting fraudulent transactions via IP addresses and is collecting these IP&apos;s via Hosted Pages &amp; API Users. Chargebee monitors all transactions and makes note of the IP addresses. This system flags a customer as suspicious if one or more of their transactions are made from a suspicious IP address.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Chargebee provides the option to block prepaid credit cards. Or virtual cards</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Payment Failure Recovery:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">&nbsp;&apos;Accounts Receivable&apos; product from Chargebee. It&apos;s a customizable follow up flow after payments fail. Proactively alert customers on card expiries and missing payment information to avoid disrupting their service and your recurring revenue.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Idempotency:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Design microservices and event processing in an idempotent manner to handle potential duplicate events. (Save RequestId/eventid/idempotencyKey coming from Chargebee and check whether it&rsquo;s processed already or not. If it&rsquo;s a duplicate event, then simply ignore it and log it to Splunk)</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Ordering or messages in the queue:&nbsp;</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Use sessionId to make sure ordering of messages in an Azure Service Bus queue or topic. Imagine a case like this: 2 events are published to the Service Bus queue, UserUpdated &amp; UserUpdated. The first one has Name = &quot;Ece&quot; and the other one has Name = &quot;Ece</span><strong><span style="font-size:11pt;">m</span></strong><span style="font-size:11pt;">&quot;. If the &quot;Ece</span><strong><span style="font-size:11pt;">m</span></strong><span style="font-size:11pt;">&quot; one is processed before the &quot;Ece&quot; for a reason, the latest state in the database will hold the &quot;Ece&quot; which is wrong</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Testing:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Comprehensive testing, including unit tests, integration tests, and security testing.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Specflow tests</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Perform Canary Testing (before official launch): select a group of clients to participate in testing new features, guaranteeing that the new API aligns with the requirements and operates smoothly.&nbsp;</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Penetration Testing: Periodic testing to discover and address potential security weaknesses.</span></p>
    </li>
</ul>
<p><br></p>
<p><span style="font-size:11pt;">Other security best practices:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Configure API Gateway to authenticate requests using&nbsp;</span><em><span style="font-size:11pt;">Azure Managed Identity</span></em><span style="font-size:11pt;">. This ensures that only authorized services can access the gateway.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Register each microservice as an Azure Active Directory App. This allows us to configure access permissions and roles for each service.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">For each of your microservices enable Managed Identity on the respective Azure services.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Ensure that the Blob Storage Service has the necessary permissions to read and write to Azure Blob Storage using Managed Identity.</span></p>
    </li>
</ul>
<p><br></p>
<p><strong><span style="font-size:11pt;">Data Model&nbsp;</span></strong></p>
<p><span style="font-size:11pt;">The data model can be designed to represent entities such as Companies (Clients), Users, Subscriptions, and Licenses. Below is a simplified representation of the data model using a document-oriented approach for MongoDB:</span></p>
<p><br></p>
<p><span style="font-size:11pt;">Company Collection:</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;_id&quot;: ObjectId(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;createdAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;updatedAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;name&quot;: &quot;Company Name&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;email&quot;: &quot;company@email.com&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;expiresAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;featurePackage&quot;: &quot;Enterprise&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;contractualUsers&quot;: 5</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><br></p>
<p><span style="font-size:11pt;">User collection</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;_id&quot;: ObjectId(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;createdAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;updatedAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;name&quot;: &quot;User Name&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;email&quot;: &quot;user@email.com&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;hash&quot;: &quot;user_unique_hash&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;company&quot;: ObjectId(&quot;...&quot;) &nbsp;// Reference to the Company document</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><br></p>
<p><span style="font-size:11pt;">PaymentOrder Collection (Part of OrderService):</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;payment_order_id&quot;: ObjectId(&quot;...&quot;), // idempotencyKey (PK)</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;createdAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;updatedAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;userId&quot;: ObjectId(&quot;...&quot;), &nbsp;// Reference to the User document</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;package&quot;: &quot;Enterprise&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;quantity&quot;: 5,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;paymentStatus&quot;: &quot;success&quot;, //not_started,executing, success, failed</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;expiryDate&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp;&quot;amount&quot;: &quot;100.0&quot;</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><br></p>
<p><span style="font-size:11pt;">License Collection (Part of License Service):</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;license_id&quot;: ObjectId(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;createdAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;updatedAt&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;orderId&quot;: ObjectId(&quot;...&quot;), &nbsp;// Reference to the Order document</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;userId&quot;: ObjectId(&quot;...&quot;), &nbsp;// Reference to the User document</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;expirationDate&quot;: ISODate(&quot;...&quot;),</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;status&quot;: &quot;Active&quot;</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><br></p>
<p><span style="font-size:11pt;">Note: We can embed the licenses directly within the Company document as an array. Each license could be represented as an object with relevant details, such as license type, expiration date, etc.</span></p>
<p><span style="font-size:11pt;">Pros:</span></p>
<p><span style="font-size:11pt;">Simplicity in retrieval as licenses are directly associated with the company.</span></p>
<p><span style="font-size:11pt;">All data is stored in a single document, reducing the need for multiple queries.</span></p>
<p><span style="font-size:11pt;">Cons:</span></p>
<p><span style="font-size:11pt;">Document size limitations in MongoDB could become a concern if the number of licenses grows significantly.</span></p>
<p><span style="font-size:11pt;">Updating licenses might require updating the entire Company document.</span></p>
<p><br></p>
<p><span style="font-size:11pt;">Instead I would create a separate collection for licenses and establish a relationship with the User entity (Company entity is also possible). Each license document references the ID of the associated Company or User.</span></p>
<p><span style="font-size:11pt;">Pros:</span></p>
<p><span style="font-size:11pt;">Allows for more flexibility in managing and updating licenses independently.</span></p>
<p><span style="font-size:11pt;">Can handle a larger number of licenses without hitting document size limitations.</span></p>
<p><span style="font-size:11pt;">Cons:</span></p>
<p><span style="font-size:11pt;">Requires additional queries to retrieve license information when needed.</span></p>
<p><br></p>
<p><br></p>
<p><strong><span style="font-size:11pt;">How Microservices Look like</span></strong></p>
<p><br></p>
<p><span style="font-size:11pt;">User Service (Microservice 1):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Manages user and company-related operations. Update user&rsquo;s name etc.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Stores user and company information in MongoDB/CosmosDB.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">If it&rsquo;s an existing user, the service checks whether the max license amount is exceeded by checking the license quantity in the database</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">When a new license is created or updated, UserService updates the license quantity</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Order Service (Microservice 2):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Handles order-related logic.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">When a new order is created, it creates a new PaymentOrder record in MongoDB/CosmosDB</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Communicates with PaymentService via Service Bus when a new order is generated</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Payment Service (Microservice 3):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Integrates with Chargebee for payment processing.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Handles webhooks from Chargebee to update PaymentStatus in PaymentOrder table.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Manages payment-related operations.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">The initial status is NOT_STARTED. When the payment service sends the payment order to the Chargebee, the status changes to EXECUTING. The payment service updates the status to SUCCESS or FAILED based on the response from Chargebee.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">License Service (Microservice 4):</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">License Allocation: Tracks and manages the allocation of licenses to clients (companies).</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Expiration Management: Monitors license expiration dates and takes appropriate actions (e.g., sending notifications, updating the status).</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Usage Tracking: Keeps track of the number of licenses purchased by a client and their current usage.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">License Information Storage: Stores license-related information, including expiration dates, usage, and other relevant details, in the MongoDB database. But the license itself is saved to Blob storage.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Communicates with the User Service to update license information based on order changes (e.g., an increase in the number of licensed users, allocate or deallocate licenses).</span></p>
    </li>
</ul>
<p><br></p>
<p><br></p>
<p><br></p>
<p><strong><span style="font-size:11pt;">A sample flow (please check&nbsp;</span></strong><strong><u><span style="font-size:11pt;">Chargebee_Integration.pdf</span></u></strong><strong><span style="font-size:11pt;">&nbsp;to see the detailed diagram);</span></strong></p>
<p><span style="font-size:11pt;">Having both Azure Gateway and APIM helped to centralise cross-cutting concerns such as authentication, SSL termination, and load balancing, rate limiting. Depending on the permission model, configure either a key vault access policy or Azure RBAC access for an API Management managed identity. The APIM service performs its security checks, and forwards valid requests to the downstream services in the AKS cluster. All services are secured inside a VNET.</span></p>
<p><br></p>
<p><span style="font-size:11pt;">User Registration/Login:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Users register on the website or log in with existing credentials.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Upon successful authentication, the website obtains an API key or OAuth token.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">API Key or Token Inclusion:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">The website includes the API key or OAuth token in the headers of requests to the API Gateway. (save those API keys to keyvault)</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">API Gateway Authentication:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">The API Gateway verifies the API key or OAuth token.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">For user-specific actions, it may validate against the user&apos;s credentials stored in the User Service.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Authorization Check:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">After authentication, the API Gateway checks the user&apos;s role and subscription level.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">It ensures that the user has the necessary permissions to perform the requested action.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">Validated Request Forwarding:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">If authentication and authorization are successful, the API Gateway forwards the validated request to the appropriate microservice, User Service in this case.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">-&gt; User service checks whether the entered license quantity is valid (not exceeding 10) by querying the related Company table. If it&rsquo;s a new subscription then there&rsquo;s no need to check the database as the max amount is always 10.&nbsp;</span></p>
<p><span style="font-size:11pt;">Note: I assume there are other services for Pricing and Product. And the total amount of selected packages is calculated by checking the Pricing table.&nbsp;</span></p>
<p><span style="font-size:11pt;">-&gt; User service publishes to package_selected topic with details like total amount, selected package, quantity, expiry date,userId</span></p>
<p><span style="font-size:11pt;">-&gt; Order service subscribed to package_selected topic. And created a new PaymentOrder record;</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;order_id&quot;: // idempotencykey</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;userId&quot;: ObjectId(&quot;...&quot;),&nbsp;</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;package&quot;: &quot;Enterprise&quot;,</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;quantity&quot;: 5</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;paymentStatus&quot;: &quot;not_started&quot;</span></p>
<p><span style="font-size:11pt;">&nbsp; &quot;expiryDate&quot;:</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp;&quot;amount&quot;: &quot;100.0&quot;</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><span style="font-size:11pt;">-&gt; Order service publishes to order_created topic with all these details and Payment Service receives this information. Upon receiving the payment order information, the payment service sends a payment registration request to Chargebee. This registration request contains relevant payment details such as the amount, currency, expiration date of the payment request, and the redirect URL. To ensure unique registration and prevent duplication, a UUID field is included. This UUID corresponds to the ID of the payment order.&nbsp;</span></p>
<p><br></p>
<p><span style="font-size:11pt;">In the 2nd step, Chargebee returns a token to the payment service, which serves as a unique identifier for the payment registration on Chargebee side. This token enables later examination of the payment registration and payment execution status.&nbsp;</span><strong><span style="font-size:11pt;">Eg: Use non-recurring payment methods used to do recurring payments.</span></strong></p>
<ul>
    <li><strong>
            <ul>
                <li style="list-style-type:disc;font-size:11pt;">
                    <p><span style="font-size:11pt;">When the initial payment is done via iDeal and completed successfully, we store the transaction ID (token).</span></p>
                </li>
            </ul>
        </strong><strong>
            <ul>
                <li style="list-style-type:disc;font-size:11pt;">
                    <p><span style="font-size:11pt;">When we upload the payment information to buckaroo after the billing run, we use that transaction ID (token) as OriginalTransaction.</span></p>
                </li>
            </ul>
        </strong></li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><strong><span style="font-size:11pt;">Buckaroo will then do a new transaction of type SEPA Direct Debit, using the IBAN of the original iDeal transaction.&nbsp;</span></strong><span style="font-size:11pt;">&nbsp;&nbsp;</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">The payment service stores the token in the database before initiating the call to the Chargebee-hosted payment page. Once the token is saved, the client displays the Chargebee-hosted payment page.&nbsp;</span></p>
<p><span style="font-size:11pt;">Chargebee handles the collection of sensitive payment information, ensuring it never reaches our payment system. The hosted payment page typically requires two pieces of information:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">The token received in step 3: Chargebee&apos;s JS code provides this token to retrieve detailed information about the payment request from Chargebee&apos;s backend. One crucial piece of information is the amount to be collected.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">The redirect URL: This is the web page URL that is called upon completion of the payment. When Chargebee&apos;s JS completes the payment process, it redirects the browser to the specified redirect URL.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">The user enters the payment information, including the credit card number, cardholder&apos;s name, expiration date, and other relevant details, on the Chargebee&apos;s webpage. After filling in the necessary information, the user clicks the pay button. Then, Chargebee initiates the payment processing procedure. In an asynchronous way, Chargebee communicates the payment status to the payment service through a webhook. During the initial setup with the Chargebee, a URL on the payment system&apos;s side is registered as the webhook. When payment events are sent to the payment system through the webhook, the payment system extracts the payment status information and updates the &quot;payment_order_status&quot; field in the PaymentOrder table.</span></p>
<p><span style="font-size:11pt;">-&gt; If the payment is successful, then Payment Service publishes a payment_successful topic. License service subscribed to this topic receives the information and generates the license. The service stores the license in Azure blob storage and then sends notification to the user using SendGrid. Then user service updates the license quantity information in the Company table.&nbsp;</span></p>
<p><br></p>
<p><span style="font-size:11pt;">Note: I preferred using Pub/sub mechanism, because I assumed there can be multiple services to consume the same message. For instance Payment events are published to Azure Service Bus and can subsequently be consumed by various services, including the payment system itself, an analytics service, and a billing service. This design enables the seamless distribution of payment-related information across multiple services, ensuring that each service can perform its specific tasks and process the payment events accordingly.</span></p>
<p><br></p>
<p><span style="font-size:11pt;">** Additional consideration: There should be a nightly-scheduled AzureWebjob to check whether there are any expiring licenses by filtering Mongodb. This can be a logic app (add a schedule and runbook to run every midnight) that puts a message in a queue called scheduled-jobs and the webjob queries MongoDB/CosmosDB to find out the licenses that are about to expire, then sends an email to those customers. If there are any licenses to be ended on the day the job runs, then the job needs to update the status of those licenses as Inactive by updating the right record in Mongodb and inform the customer by sending a notification.&nbsp;</span></p>
<p><br></p>
<p><span style="font-size:11pt;">Another way is to use a timer function:&nbsp;</span></p>
<p><span style="font-size:11pt;">In the License Service, we can create a Timer Trigger Function. This function will be triggered at regular intervals to check for licenses about to expire. We can use this function to initiate the notification process.</span></p>
<p><br></p>
<p><span style="font-size:11pt;">public static class LicenseExpirationCheckFunction</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; [FunctionName(&quot;LicenseExpirationCheck&quot;)]</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; public static void Run([TimerTrigger(&quot;0 0 0 * * *&quot;)] TimerInfo myTimer, ILogger log)</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; {</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; // This function runs every day at midnight (0 0 0 * * *)</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; // Implement logic to check for licenses about to expire</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; // Trigger the process to notify users about expiring licenses</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; NotifyUsersAboutExpiringLicenses();</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; }</span></p>
<p><br></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; private static void NotifyUsersAboutExpiringLicenses()</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; {</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; // Implement the logic to get licenses about to expire</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; // Trigger the Notification Service to send notifications</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; }</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><br></p>
<p><span style="font-size:11pt;">Once the LicenseExpirationCheckFunction identifies licenses about to expire, it can trigger the Notification Service. This can be achieved by calling an HTTP endpoint exposed by the Notification Service or by using a message queue. The NotifyUsers function is triggered by a message in the &quot;notificationqueue&quot;.</span></p>
<p><br></p>
<p><span style="font-size:11pt;">public static class NotificationService</span></p>
<p><span style="font-size:11pt;">{</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; [FunctionName(&quot;NotifyUsers&quot;)]</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; public static void Run([QueueTrigger(&quot;notificationqueue&quot;)] string message, ILogger log)</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; {</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; // Implement logic to send notifications to users</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; &nbsp; &nbsp; log.LogInformation($&quot;Sending notification: {message}&quot;);</span></p>
<p><span style="font-size:11pt;">&nbsp; &nbsp; }</span></p>
<p><span style="font-size:11pt;">}</span></p>
<p><br></p>
<p><br></p>
<p><br></p>
<p><strong><span style="font-size:13.999999999999998pt;">How to handle failed payments</span></strong></p>
<p><br></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Retry queue: retryable errors such as transient errors are routed to a retry queue.&nbsp;</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Dead letter queue: if a message fails repeatedly, it eventually lands in the dead letter queue. A dead letter queue is useful for debugging and isolating problematic messages for inspection to determine why they were not processed successfully.</span></p>
    </li>
</ul>
<p><br></p>
<p><span style="font-size:11pt;">Check whether the failure is retryable.</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Retryable failures are routed to a retry queue.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">For non-retryable failures such as invalid input, errors are stored in a database.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">The payment system consumes events from the retry queue and retries failed payment transactions.</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">If the payment transaction fails again:</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">If the retry count doesn&rsquo;t exceed the threshold, the event is routed to the retry queue.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">If the retry count exceeds the threshold, the event is put in the dead letter queue. Those failed events might need to be investigated.</span></p>
    </li>
</ul>
<p><br></p>
<p><span style="font-size:11pt;">Another concern is to achieve&nbsp;</span><strong><span style="font-size:11pt;">exactly-once delivery</span></strong><span style="font-size:11pt;">. One of the most critical issues that a payment system can encounter is double-charging a customer. By combining retry mechanisms for at-least-once execution and implementing idempotency checks for&nbsp;</span><strong><span style="font-size:11pt;">at-most-once execution</span></strong><span style="font-size:11pt;">, we can create a robust and reliable payment system that ensures the execution of payment orders exactly once, mitigating the risk of double-charging customers.&nbsp;</span></p>
<p><span style="font-size:11pt;">Here are some common retry strategies:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Immediate retry: The client promptly resends the request after a failure occurs.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Fixed intervals: A fixed amount of time is waited between the failed payment and subsequent retry attempts.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Incremental intervals: The client initially waits for a short period before the first retry and then gradually increases the waiting time for subsequent retries.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Exponential backoff: The waiting time between retries is doubled after each failed attempt. For instance, if the request fails the first time, a retry is attempted after 1 second. If it fails again, the next retry is attempted after 2 seconds, and so on.</span></p>
    </li>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">Cancel: The client has the option to cancel the request, especially when the failure is permanent or further retries are unlikely to succeed.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">One potential problem with retries is the possibility of double payments.</span></p>
<p><br></p>
<p><u><span style="font-size:11pt;">Scenario: What if a customer clicks the &ldquo;pay&rdquo; button quickly twice?&nbsp;</span></u></p>
<p><span style="font-size:11pt;">When a user clicks the &quot;pay&quot; button, an idempotency key is included in the HTTP request sent to the payment system. In the case of a second request, it is considered a retry since the payment system has already encountered the idempotency key (payment_order_id). By including the previously specified idempotency key in the request header, the payment system responds by providing the latest status of the previous request. This approach ensures that duplicate requests or retries are effectively handled and prevents unintended consequences that may arise from multiple submissions of the same payment. If multiple concurrent requests are detected with the same idempotency key, only one request is processed and the others receive the &ldquo;429 Too Many Requests&rdquo; status code.</span></p>
<p><br></p>
<p><u><span style="font-size:11pt;">Scenario: The payment is successfully processed by Chargebee, but the response fails to reach our payment system due to network errors. Then the user clicks the &ldquo;pay&rdquo; again.</span></u></p>
<p><span style="font-size:11pt;">if the payment is successfully processed by Chargebee, but the response fails to reach our payment system due to network errors, and subsequently the user clicks the &quot;pay&quot; button again, the following scenario can occur:</span></p>
<ul>
    <li style="list-style-type:disc;font-size:11pt;">
        <p><span style="font-size:11pt;">The second &quot;pay&quot; request is sent to the payment system, unaware that the initial payment was actually successful.</span></p>
    </li>
</ul>
<p><span style="font-size:11pt;">At this point, the payment system needs to handle the duplicate request and ensure that the duplicate payment is not processed twice, preventing any unintended consequences or duplicate charges.</span></p>
<p><span style="font-size:11pt;">To address this situation, the payment system can implement mechanisms such as idempotency keys or unique identifiers. By including an idempotency key in the request, the payment system can identify and recognize the duplicate request. It can then determine that the payment has already been successfully processed and respond accordingly, without processing the payment again. This helps maintain data integrity and prevents any duplicate or erroneous transactions caused by network errors or user interactions.</span></p>
