<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:13.999999999999998pt;&quot;&gt;PSP(Chargebee) Integration High-Level System Architecture&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Backend:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;.NET Core for microservices.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Database:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;Azure Cosmos DB with MongoDB API. (Azure Cosmos DB provides compatibility with the MongoDB API, which means you can use existing MongoDB libraries, drivers, and tools to interact with Azure Cosmos DB.)&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;API Gateway:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;Azure API Management. Can be used together with Azure API Gateway.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Message Queue:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;Azure Service Bus. (Apache Kafka is also a nice option) (Azure Service Bus would likely be the best fit but Azure Event Hubs are an option too especially when we need to quickly accept events (millions) from end-users.)&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Authentication:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;OAuth or JWT.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Containerization:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;Docker (if needed for local development or deployment). Azure Kubernetes Service for orchestration&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;API Documentation:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;&lt;/span&gt;&lt;span style=&quot;color:#1d1c1d;background-color:#ffffff;font-size:11.5pt;&quot;&gt;Azure APIM also provides API documentation which we can import via OpenAPI specification&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Storage for sensitive information:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;Azure Key Vault. Secure all services inside a VNET and communication is primarily via APIM (Azure API Management). Also, leverage&nbsp;&lt;/span&gt;&lt;em&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Azure Managed Identity&lt;/span&gt;&lt;/em&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;to completely eliminate handling of secure strings where possible.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Monitoring:&nbsp;&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Use tools like Prometheus, Azure Application Insights and Grafana for monitoring microservices and infrastructure.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Email Infrastructure:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;SendGrid&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Payment system:&lt;/span&gt;&lt;/u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;Chargebee as PSP&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;High Availability and Disaster Recovery Plan&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;High Availability:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Utilize Azure Availability Sets for VMs and AKS for microservices to ensure redundancy. (Deploy resources across multiple zones)&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Microservices can be deployed and scaled independently, allowing for optimal resource allocation and handling increased load. (Autoscaling configured for microservices based on demand.)&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Docker for easy deployment and scaling.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Container Orchestration (Azure Kubernetes Service - AKS):&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Deploy microservices as containers for scalability and manageability.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Disaster Recovery:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Regularly backup Azure Cosmos DB to Azure Blob Storage for quick recovery in case of data loss.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Use Azure Site Recovery for VM-level disaster recovery.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Implement geographically distributed data centers for additional redundancy.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Runbook Documentation: Develop runbooks with detailed procedures for recovery in case of a disaster.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Logging and Monitoring (Azure Application Insights):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Use Azure Application Insights for real-time monitoring microservice performance, troubleshooting and logs. Splunk, New Relic, Datadog, ELK (Elasticsearch, Logstash, Kibana) Stack (for centralized logging, analyzing user actions, and troubleshooting issues) , Prometheus, Grafana (Prometheus and Grafana for monitoring system health, resource usage, and performance metrics) can also be options&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;API Gateway (Azure API Management):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Azure API Gateway to manage and route requests. Acts as a single entry point for clients.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Responsible for authentication, rate limiting, request validation, and routing to appropriate microservices.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Load Balancer (Azure Load Balancer) (not a must):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Azure Load Balancer for distributing incoming traffic across multiple instances of microservices for scalability and high availability. It can reroute traffic away from unhealthy instances, preventing them from affecting overall system performance. NGINX can be used as well. &lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;** The combination of an API Gateway and Load Balancer allows for both vertical and horizontal scalability, ensuring the system can handle increased loads efficiently. API Gateway enhances security by handling authentication and authorization, while the Load Balancer contributes to system resilience and fault tolerance. Separating concerns between API management and traffic distribution provides a modular and more easily maintainable architecture.Centralized monitoring and logging through the API Gateway help in tracking and diagnosing issues, while the Load Balancer ensures even distribution of traffic for optimal performance.&nbsp;&lt;/span&gt;&lt;em&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Azure API Management alone may be sufficient, especially if the APIs are not distributed across multiple backend servers.&lt;/span&gt;&lt;/em&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Security Risks and Mitigations&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Data Breach:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Implement encryption at rest, use secure connections (HTTPS) by ensuring Azure App Service is configured to use a valid SSL/TLS certificate, and regularly update security patches.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Unauthorized Access:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Implement OAuth or JWT for authentication, RBAC for microservices access (authorization), and secure API key management.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Secure Key Management:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Store and manage sensitive information such as API keys and secrets in Azure Key Vault. (managed identity)&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Denial of Service (DoS) Attacks:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Utilize Azure DDoS Protection.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Implement rate limiting and throttling (via API Gateway/ APIM).&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Webhook Security:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Use secure HTTPS for webhook communication.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Validate and verify incoming webhook payloads from Chargebee or any other 3rd party.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Anti Fraud - block fraudsters from signing up (without knowing who they are):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;ChargeBee is detecting fraudulent transactions via IP addresses and is collecting these IP&apos;s via Hosted Pages &amp; API Users. Chargebee monitors all transactions and makes note of the IP addresses. This system flags a customer as suspicious if one or more of their transactions are made from a suspicious IP address.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Chargebee provides the option to block prepaid credit cards. Or virtual cards&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Payment Failure Recovery:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &apos;Accounts Receivable&apos; product from Chargebee. It&apos;s a customizable follow up flow after payments fail. Proactively alert customers on card expiries and missing payment information to avoid disrupting their service and your recurring revenue.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Idempotency:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Design microservices and event processing in an idempotent manner to handle potential duplicate events. (Save RequestId/eventid/idempotencyKey coming from Chargebee and check whether it&rsquo;s processed already or not. If it&rsquo;s a duplicate event, then simply ignore it and log it to Splunk)&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Ordering or messages in the queue:&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Use sessionId to make sure ordering of messages in an Azure Service Bus queue or topic. Imagine a case like this: 2 events are published to the Service Bus queue, UserUpdated &amp; UserUpdated. The first one has Name = &quot;Ece&quot; and the other one has Name = &quot;Ece&lt;/span&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;m&lt;/span&gt;&lt;/strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&quot;. If the &quot;Ece&lt;/span&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;m&lt;/span&gt;&lt;/strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&quot; one is processed before the &quot;Ece&quot; for a reason, the latest state in the database will hold the &quot;Ece&quot; which is wrong&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Testing:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Comprehensive testing, including unit tests, integration tests, and security testing.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Specflow tests&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Perform Canary Testing (before official launch): select a group of clients to participate in testing new features, guaranteeing that the new API aligns with the requirements and operates smoothly. &lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Penetration Testing: Periodic testing to discover and address potential security weaknesses.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Other security best practices:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Configure API Gateway to authenticate requests using &lt;/span&gt;&lt;em&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Azure Managed Identity&lt;/span&gt;&lt;/em&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;. This ensures that only authorized services can access the gateway.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Register each microservice as an Azure Active Directory App. This allows us to configure access permissions and roles for each service.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;For each of your microservices enable Managed Identity on the respective Azure services.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Ensure that the Blob Storage Service has the necessary permissions to read and write to Azure Blob Storage using Managed Identity.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Data Model&nbsp;&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The data model can be designed to represent entities such as Companies (Clients), Users, Subscriptions, and Licenses. Below is a simplified representation of the data model using a document-oriented approach for MongoDB:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Company Collection:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;_id&quot;: ObjectId(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;createdAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;updatedAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;name&quot;: &quot;Company Name&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;email&quot;: &quot;<a data-fr-linked="true" href="mailto:company@email.com">company@email.com</a>&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;expiresAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;featurePackage&quot;: &quot;Enterprise&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;contractualUsers&quot;: 5&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;User collection&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;_id&quot;: ObjectId(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;createdAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;updatedAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;name&quot;: &quot;User Name&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;email&quot;: &quot;<a data-fr-linked="true" href="mailto:user@email.com">user@email.com</a>&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;hash&quot;: &quot;user_unique_hash&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;company&quot;: ObjectId(&quot;...&quot;) &nbsp;// Reference to the Company document&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;PaymentOrder Collection (Part of OrderService):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;payment_order_id&quot;: ObjectId(&quot;...&quot;), // idempotencyKey (PK)&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;createdAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;updatedAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;userId&quot;: ObjectId(&quot;...&quot;), &nbsp;// Reference to the User document&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;package&quot;: &quot;Enterprise&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;quantity&quot;: 5,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;paymentStatus&quot;: &quot;success&quot;, //not_started,executing, success, failed&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;expiryDate&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &quot;amount&quot;: &quot;100.0&quot;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;License Collection (Part of License Service):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;license_id&quot;: ObjectId(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;createdAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;updatedAt&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;orderId&quot;: ObjectId(&quot;...&quot;), &nbsp;// Reference to the Order document&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;userId&quot;: ObjectId(&quot;...&quot;), &nbsp;// Reference to the User document&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;expirationDate&quot;: ISODate(&quot;...&quot;),&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;status&quot;: &quot;Active&quot;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Note: We can embed the licenses directly within the Company document as an array. Each license could be represented as an object with relevant details, such as license type, expiration date, etc.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Pros:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Simplicity in retrieval as licenses are directly associated with the company.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;All data is stored in a single document, reducing the need for multiple queries.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Cons:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Document size limitations in MongoDB could become a concern if the number of licenses grows significantly.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Updating licenses might require updating the entire Company document.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Instead I would create a separate collection for licenses and establish a relationship with the User entity (Company entity is also possible). Each license document references the ID of the associated Company or User.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Pros:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Allows for more flexibility in managing and updating licenses independently.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Can handle a larger number of licenses without hitting document size limitations.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Cons:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Requires additional queries to retrieve license information when needed.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;How Microservices Look like&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;User Service (Microservice 1):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Manages user and company-related operations. Update user&rsquo;s name etc.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Stores user and company information in MongoDB/CosmosDB.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;If it&rsquo;s an existing user, the service checks whether the max license amount is exceeded by checking the license quantity in the database&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;When a new license is created or updated, UserService updates the license quantity&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Order Service (Microservice 2):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Handles order-related logic.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;When a new order is created, it creates a new PaymentOrder record in MongoDB/CosmosDB&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Communicates with PaymentService via Service Bus when a new order is generated&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Payment Service (Microservice 3):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Integrates with Chargebee for payment processing.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Handles webhooks from Chargebee to update PaymentStatus in PaymentOrder table.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Manages payment-related operations.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The initial status is NOT_STARTED. When the payment service sends the payment order to the Chargebee, the status changes to EXECUTING. The payment service updates the status to SUCCESS or FAILED based on the response from Chargebee.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;License Service (Microservice 4):&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;License Allocation: Tracks and manages the allocation of licenses to clients (companies).&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Expiration Management: Monitors license expiration dates and takes appropriate actions (e.g., sending notifications, updating the status).&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Usage Tracking: Keeps track of the number of licenses purchased by a client and their current usage.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;License Information Storage: Stores license-related information, including expiration dates, usage, and other relevant details, in the MongoDB database. But the license itself is saved to Blob storage.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Communicates with the User Service to update license information based on order changes (e.g., an increase in the number of licensed users, allocate or deallocate licenses).&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;A sample flow (please check&nbsp;&lt;/span&gt;&lt;/strong&gt;&lt;strong&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Chargebee_Integration.pdf&lt;/span&gt;&lt;/u&gt;&lt;/strong&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;&nbsp;to see the detailed diagram);&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Having both Azure Gateway and APIM helped to centralise cross-cutting concerns such as authentication, SSL termination, and load balancing, rate limiting. Depending on the permission model, configure either a key vault access policy or Azure RBAC access for an API Management managed identity. The APIM service performs its security checks, and forwards valid requests to the downstream services in the AKS cluster. All services are secured inside a VNET.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;User Registration/Login:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Users register on the website or log in with existing credentials.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Upon successful authentication, the website obtains an API key or OAuth token.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;API Key or Token Inclusion:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The website includes the API key or OAuth token in the headers of requests to the API Gateway. (save those API keys to keyvault)&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;API Gateway Authentication:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The API Gateway verifies the API key or OAuth token.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;For user-specific actions, it may validate against the user&apos;s credentials stored in the User Service.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Authorization Check:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;After authentication, the API Gateway checks the user&apos;s role and subscription level.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;It ensures that the user has the necessary permissions to perform the requested action.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Validated Request Forwarding:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;If authentication and authorization are successful, the API Gateway forwards the validated request to the appropriate microservice, User Service in this case.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;-&gt; User service checks whether the entered license quantity is valid (not exceeding 10) by querying the related Company table. If it&rsquo;s a new subscription then there&rsquo;s no need to check the database as the max amount is always 10.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Note: I assume there are other services for Pricing and Product. And the total amount of selected packages is calculated by checking the Pricing table.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;-&gt; User service publishes to package_selected topic with details like total amount, selected package, quantity, expiry date,userId&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;-&gt; Order service subscribed to package_selected topic. And created a new PaymentOrder record;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;order_id&quot;: // idempotencykey&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;userId&quot;: ObjectId(&quot;...&quot;), &lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;package&quot;: &quot;Enterprise&quot;,&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;quantity&quot;: 5&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;paymentStatus&quot;: &quot;not_started&quot;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&quot;expiryDate&quot;:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &quot;amount&quot;: &quot;100.0&quot;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;-&gt; Order service publishes to order_created topic with all these details and Payment Service receives this information. Upon receiving the payment order information, the payment service sends a payment registration request to Chargebee. This registration request contains relevant payment details such as the amount, currency, expiration date of the payment request, and the redirect URL. To ensure unique registration and prevent duplication, a UUID field is included. This UUID corresponds to the ID of the payment order.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;In the 2nd step, Chargebee returns a token to the payment service, which serves as a unique identifier for the payment registration on Chargebee side. This token enables later examination of the payment registration and payment execution status.&nbsp;&lt;/span&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Eg: Use non-recurring payment methods used to do recurring payments.&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li&gt;&lt;strong&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;ul&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;When the initial payment is done via iDeal and completed successfully, we store the transaction ID (token).&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;/ul&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;/strong&gt;&lt;strong&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;ul&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;When we upload the payment information to buckaroo after the billing run, we use that transaction ID (token) as OriginalTransaction.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &lt;/ul&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;/strong&gt;&lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Buckaroo will then do a new transaction of type SEPA Direct Debit, using the IBAN of the original iDeal transaction. &lt;/span&gt;&lt;/strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The payment service stores the token in the database before initiating the call to the Chargebee-hosted payment page. Once the token is saved, the client displays the Chargebee-hosted payment page.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Chargebee handles the collection of sensitive payment information, ensuring it never reaches our payment system. The hosted payment page typically requires two pieces of information:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The token received in step 3: Chargebee&apos;s JS code provides this token to retrieve detailed information about the payment request from Chargebee&apos;s backend. One crucial piece of information is the amount to be collected.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The redirect URL: This is the web page URL that is called upon completion of the payment. When Chargebee&apos;s JS completes the payment process, it redirects the browser to the specified redirect URL.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The user enters the payment information, including the credit card number, cardholder&apos;s name, expiration date, and other relevant details, on the Chargebee&apos;s webpage. After filling in the necessary information, the user clicks the pay button. Then, Chargebee initiates the payment processing procedure. In an asynchronous way, Chargebee communicates the payment status to the payment service through a webhook. During the initial setup with the Chargebee, a URL on the payment system&apos;s side is registered as the webhook. When payment events are sent to the payment system through the webhook, the payment system extracts the payment status information and updates the &quot;payment_order_status&quot; field in the PaymentOrder table.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;-&gt; If the payment is successful, then Payment Service publishes a payment_successful topic. License service subscribed to this topic receives the information and generates the license. The service stores the license in Azure blob storage and then sends notification to the user using SendGrid. Then user service updates the license quantity information in the Company table.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Note: I preferred using Pub/sub mechanism, because I assumed there can be multiple services to consume the same message. For instance Payment events are published to Azure Service Bus and can subsequently be consumed by various services, including the payment system itself, an analytics service, and a billing service. This design enables the seamless distribution of payment-related information across multiple services, ensuring that each service can perform its specific tasks and process the payment events accordingly.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;** Additional consideration: There should be a nightly-scheduled AzureWebjob to check whether there are any expiring licenses by filtering Mongodb. This can be a logic app (add a schedule and runbook to run every midnight) that puts a message in a queue called scheduled-jobs and the webjob queries MongoDB/CosmosDB to find out the licenses that are about to expire, then sends an email to those customers. If there are any licenses to be ended on the day the job runs, then the job needs to update the status of those licenses as Inactive by updating the right record in Mongodb and inform the customer by sending a notification.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Another way is to use a timer function:&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;In the License Service, we can create a Timer Trigger Function. This function will be triggered at regular intervals to check for licenses about to expire. We can use this function to initiate the notification process.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;public static class LicenseExpirationCheckFunction&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;[FunctionName(&quot;LicenseExpirationCheck&quot;)]&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;public static void Run([TimerTrigger(&quot;0 0 0 * * *&quot;)] TimerInfo myTimer, ILogger log)&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;// This function runs every day at midnight (0 0 0 * * *)&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;// Implement logic to check for licenses about to expire&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;// Trigger the process to notify users about expiring licenses&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;NotifyUsersAboutExpiringLicenses();&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;private static void NotifyUsersAboutExpiringLicenses()&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;// Implement the logic to get licenses about to expire&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;// Trigger the Notification Service to send notifications&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Once the LicenseExpirationCheckFunction identifies licenses about to expire, it can trigger the Notification Service. This can be achieved by calling an HTTP endpoint exposed by the Notification Service or by using a message queue. The NotifyUsers function is triggered by a message in the &quot;notificationqueue&quot;.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;public static class NotificationService&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;[FunctionName(&quot;NotifyUsers&quot;)]&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;public static void Run([QueueTrigger(&quot;notificationqueue&quot;)] string message, ILogger log)&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;{&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;// Implement logic to send notifications to users&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp; &nbsp; &nbsp;log.LogInformation($&quot;Sending notification: {message}&quot;);&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt; &nbsp; &nbsp;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;}&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;strong&gt;&lt;span style=&quot;font-size:13.999999999999998pt;&quot;&gt;How to handle failed payments&lt;/span&gt;&lt;/strong&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Retry queue: retryable errors such as transient errors are routed to a retry queue. &lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Dead letter queue: if a message fails repeatedly, it eventually lands in the dead letter queue. A dead letter queue is useful for debugging and isolating problematic messages for inspection to determine why they were not processed successfully.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Check whether the failure is retryable.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Retryable failures are routed to a retry queue.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;For non-retryable failures such as invalid input, errors are stored in a database.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The payment system consumes events from the retry queue and retries failed payment transactions.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;If the payment transaction fails again:&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;If the retry count doesn&rsquo;t exceed the threshold, the event is routed to the retry queue.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;If the retry count exceeds the threshold, the event is put in the dead letter queue. Those failed events might need to be investigated.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Another concern is to achieve&nbsp;&lt;/span&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;exactly-once delivery&lt;/span&gt;&lt;/strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;. One of the most critical issues that a payment system can encounter is double-charging a customer. By combining retry mechanisms for at-least-once execution and implementing idempotency checks for&nbsp;&lt;/span&gt;&lt;strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;at-most-once execution&lt;/span&gt;&lt;/strong&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;, we can create a robust and reliable payment system that ensures the execution of payment orders exactly once, mitigating the risk of double-charging customers.&nbsp;&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Here are some common retry strategies:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Immediate retry: The client promptly resends the request after a failure occurs.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Fixed intervals: A fixed amount of time is waited between the failed payment and subsequent retry attempts.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Incremental intervals: The client initially waits for a short period before the first retry and then gradually increases the waiting time for subsequent retries.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Exponential backoff: The waiting time between retries is doubled after each failed attempt. For instance, if the request fails the first time, a retry is attempted after 1 second. If it fails again, the next retry is attempted after 2 seconds, and so on.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Cancel: The client has the option to cancel the request, especially when the failure is permanent or further retries are unlikely to succeed.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;One potential problem with retries is the possibility of double payments.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Scenario: What if a customer clicks the &ldquo;pay&rdquo; button quickly twice?&nbsp;&lt;/span&gt;&lt;/u&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;When a user clicks the &quot;pay&quot; button, an idempotency key is included in the HTTP request sent to the payment system. In the case of a second request, it is considered a retry since the payment system has already encountered the idempotency key (payment_order_id). By including the previously specified idempotency key in the request header, the payment system responds by providing the latest status of the previous request. This approach ensures that duplicate requests or retries are effectively handled and prevents unintended consequences that may arise from multiple submissions of the same payment. If multiple concurrent requests are detected with the same idempotency key, only one request is processed and the others receive the &ldquo;429 Too Many Requests&rdquo; status code.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;br&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;u&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;Scenario: The payment is successfully processed by Chargebee, but the response fails to reach our payment system due to network errors. Then the user clicks the &ldquo;pay&rdquo; again.&lt;/span&gt;&lt;/u&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;if the payment is successfully processed by Chargebee, but the response fails to reach our payment system due to network errors, and subsequently the user clicks the &quot;pay&quot; button again, the following scenario can occur:&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;ul&gt;</p>
<p>&nbsp; &nbsp; &lt;li style=&quot;list-style-type:disc;font-size:11pt;&quot;&gt;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;The second &quot;pay&quot; request is sent to the payment system, unaware that the initial payment was actually successful.&lt;/span&gt;&lt;/p&gt;</p>
<p>&nbsp; &nbsp; &lt;/li&gt;</p>
<p>&lt;/ul&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;At this point, the payment system needs to handle the duplicate request and ensure that the duplicate payment is not processed twice, preventing any unintended consequences or duplicate charges.&lt;/span&gt;&lt;/p&gt;</p>
<p>&lt;p&gt;&lt;span style=&quot;font-size:11pt;&quot;&gt;To address this situation, the payment system can implement mechanisms such as idempotency keys or unique identifiers. By including an idempotency key in the request, the payment system can identify and recognize the duplicate request. It can then determine that the payment has already been successfully processed and respond accordingly, without processing the payment again. This helps maintain data integrity and prevents any duplicate or erroneous transactions caused by network errors or user interactions.&lt;/span&gt;&lt;/p&gt;</p>
