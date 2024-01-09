<p><strong>PSP(Chargebee) Integration High-Level System Architecture</strong></p>
<p>Backend: .NET Core for microservices.</p>
<p>Database: Azure Cosmos DB with MongoDB API. (Azure Cosmos DB provides compatibility with the MongoDB API, which means you can use existing MongoDB libraries, drivers, and tools to interact with Azure Cosmos DB.)</p>
<p>API Gateway: Azure API Management. Can be used together with Azure API Gateway.&nbsp;</p>
<p>Message Queue: Azure Service Bus. (Apache Kafka is also a nice option) (Azure Service Bus would likely be the best fit but Azure Event Hubs are an option too especially when we need to quickly accept events (millions) from end-users.)</p>
<p>Authentication: OAuth or JWT.</p>
<p>Containerization: Docker (if needed for local development or deployment). Azure Kubernetes Service for orchestration</p>
<p>API Documentation:Azure APIM also provides API documentation which we can import via OpenAPI specification</p>
<p>Storage for sensitive information: Azure Key Vault. Secure all services inside a VNET and communication is primarily via APIM (Azure API Management). Also, leverage <em>Azure Managed Identity</em> to completely eliminate handling of secure strings where possible.</p>
<p>Monitoring: Use tools like Prometheus, Azure Application Insights and Grafana for monitoring microservices and infrastructure.</p>
<p>Email Infrastructure: SendGrid</p>
<p>Payment system: Chargebee as PSP</p>
<p><strong>High Availability and Disaster Recovery Plan</strong></p>
<p>High Availability:</p>
<ul>
<li>Utilize Azure Availability Sets for VMs and AKS for microservices to ensure redundancy. (Deploy resources across multiple zones)</li>
<li>Microservices can be deployed and scaled independently, allowing for optimal resource allocation and handling increased load. (Autoscaling configured for microservices based on demand.)</li>
<li>Docker for easy deployment and scaling.</li>
<li>Container Orchestration (Azure Kubernetes Service - AKS):</li>
<li>Deploy microservices as containers for scalability and manageability.</li>
</ul>
<p>Disaster Recovery:</p>
<ul>
<li>Regularly backup Azure Cosmos DB to Azure Blob Storage for quick recovery in case of data loss.</li>
<li>Use Azure Site Recovery for VM-level disaster recovery.</li>
<li>Implement geographically distributed data centers for additional redundancy.</li>
<li>Runbook Documentation: Develop runbooks with detailed procedures for recovery in case of a disaster.</li>
</ul>
<p>Logging and Monitoring (Azure Application Insights):</p>
<ul>
<li>Use Azure Application Insights for real-time monitoring microservice performance, troubleshooting and logs. Splunk, New Relic, Datadog, ELK (Elasticsearch, Logstash, Kibana) Stack (for centralized logging, analyzing user actions, and troubleshooting issues) , Prometheus, Grafana (Prometheus and Grafana for monitoring system health, resource usage, and performance metrics) can also be options</li>
</ul>
<p><br /><br /><br /></p>
<p>API Gateway (Azure API Management):</p>
<ul>
<li>Azure API Gateway to manage and route requests. Acts as a single entry point for clients.</li>
<li>Responsible for authentication, rate limiting, request validation, and routing to appropriate microservices.</li>
</ul>
<p>Load Balancer (Azure Load Balancer) (not a must):</p>
<ul>
<li>Azure Load Balancer for distributing incoming traffic across multiple instances of microservices for scalability and high availability. It can reroute traffic away from unhealthy instances, preventing them from affecting overall system performance. NGINX can be used as well.&nbsp;</li>
</ul>
<p>** The combination of an API Gateway and Load Balancer allows for both vertical and horizontal scalability, ensuring the system can handle increased loads efficiently. API Gateway enhances security by handling authentication and authorization, while the Load Balancer contributes to system resilience and fault tolerance. Separating concerns between API management and traffic distribution provides a modular and more easily maintainable architecture.Centralized monitoring and logging through the API Gateway help in tracking and diagnosing issues, while the Load Balancer ensures even distribution of traffic for optimal performance. <em>Azure API Management alone may be sufficient, especially if the APIs are not distributed across multiple backend servers.</em></p>
<p><strong>Security Risks and Mitigations</strong></p>
<p>Data Breach:</p>
<ul>
<li>Implement encryption at rest, use secure connections (HTTPS) by ensuring Azure App Service is configured to use a valid SSL/TLS certificate, and regularly update security patches.</li>
</ul>
<p>Unauthorized Access:</p>
<ul>
<li>Implement OAuth or JWT for authentication, RBAC for microservices access (authorization), and secure API key management.</li>
</ul>
<p>Secure Key Management:</p>
<ul>
<li>Store and manage sensitive information such as API keys and secrets in Azure Key Vault. (managed identity)</li>
</ul>
<p>Denial of Service (DoS) Attacks:</p>
<ul>
<li>Utilize Azure DDoS Protection.</li>
<li>Implement rate limiting and throttling (via API Gateway/ APIM).</li>
</ul>
<p>Webhook Security:</p>
<ul>
<li>Use secure HTTPS for webhook communication.</li>
<li>Validate and verify incoming webhook payloads from Chargebee or any other 3rd party.</li>
</ul>
<p>Anti Fraud - block fraudsters from signing up (without knowing who they are):</p>
<ul>
<li>ChargeBee is detecting fraudulent transactions via IP addresses and is collecting these IP's via Hosted Pages &amp; API Users. Chargebee monitors all transactions and makes note of the IP addresses. This system flags a customer as suspicious if one or more of their transactions are made from a suspicious IP address.</li>
<li>Chargebee provides the option to block prepaid credit cards. Or virtual cards</li>
</ul>
<p>Payment Failure Recovery:</p>
<ul>
<li>&nbsp;'Accounts Receivable' product from Chargebee. It's a customizable follow up flow after payments fail. Proactively alert customers on card expiries and missing payment information to avoid disrupting their service and your recurring revenue.</li>
</ul>
<p>Idempotency:</p>
<ul>
<li>Design microservices and event processing in an idempotent manner to handle potential duplicate events. (Save RequestId/eventid/idempotencyKey coming from Chargebee and check whether it&rsquo;s processed already or not. If it&rsquo;s a duplicate event, then simply ignore it and log it to Splunk)</li>
</ul>
<p>Ordering or messages in the queue:&nbsp;</p>
<ul>
<li>Use sessionId to make sure ordering of messages in an Azure Service Bus queue or topic. Imagine a case like this: 2 events are published to the Service Bus queue, UserUpdated &amp; UserUpdated. The first one has Name = "Ece" and the other one has Name = "Ece<strong>m</strong>". If the "Ece<strong>m</strong>" one is processed before the "Ece" for a reason, the latest state in the database will hold the "Ece" which is wrong</li>
</ul>
<p>Testing:</p>
<ul>
<li>Comprehensive testing, including unit tests, integration tests, and security testing.</li>
<li>Specflow tests</li>
<li>Perform Canary Testing (before official launch): select a group of clients to participate in testing new features, guaranteeing that the new API aligns with the requirements and operates smoothly.&nbsp;</li>
<li>Penetration Testing: Periodic testing to discover and address potential security weaknesses.</li>
</ul>
<p>Other security best practices:</p>
<ul>
<li>Configure API Gateway to authenticate requests using <em>Azure Managed Identity</em>. This ensures that only authorized services can access the gateway.</li>
<li>Register each microservice as an Azure Active Directory App. This allows us to configure access permissions and roles for each service.</li>
<li>For each of your microservices enable Managed Identity on the respective Azure services.</li>
<li>Ensure that the Blob Storage Service has the necessary permissions to read and write to Azure Blob Storage using Managed Identity.</li>
</ul>
<p><strong>Data Model&nbsp;</strong></p>
<p>The data model can be designed to represent entities such as Companies (Clients), Users, Subscriptions, and Licenses. Below is a simplified representation of the data model using a document-oriented approach for MongoDB:</p>
<p>Company Collection:</p>
<p>{</p>
<p>"_id": ObjectId("..."),</p>
<p>"createdAt": ISODate("..."),</p>
<p>"updatedAt": ISODate("..."),</p>
<p>"name": "Company Name",</p>
<p>"email": "company@email.com",</p>
<p>"expiresAt": ISODate("..."),</p>
<p>"featurePackage": "Enterprise",</p>
<p>"contractualUsers": 5</p>
<p>}</p>
<p>User collection</p>
<p>{</p>
<p>"_id": ObjectId("..."),</p>
<p>"createdAt": ISODate("..."),</p>
<p>"updatedAt": ISODate("..."),</p>
<p>"name": "User Name",</p>
<p>"email": "user@email.com",</p>
<p>"hash": "user_unique_hash",</p>
<p>"company": ObjectId("...") // Reference to the Company document</p>
<p>}</p>
<p>PaymentOrder Collection (Part of OrderService):</p>
<p>{</p>
<p>"payment_order_id": ObjectId("..."), // idempotencyKey (PK)</p>
<p>"createdAt": ISODate("..."),</p>
<p>"updatedAt": ISODate("..."),</p>
<p>"userId": ObjectId("..."), // Reference to the User document</p>
<p>"package": "Enterprise",</p>
<p>"quantity": 5,</p>
<p>"paymentStatus": "success", //not_started,executing, success, failed</p>
<p>"expiryDate": ISODate("..."),</p>
<p>"amount": "100.0"</p>
<p>}</p>
<p>License Collection (Part of License Service):</p>
<p>{</p>
<p>"license_id": ObjectId("..."),</p>
<p>"createdAt": ISODate("..."),</p>
<p>"updatedAt": ISODate("..."),</p>
<p>"orderId": ObjectId("..."), // Reference to the Order document</p>
<p>"userId": ObjectId("..."), // Reference to the User document</p>
<p>"expirationDate": ISODate("..."),</p>
<p>"status": "Active"</p>
<p>}</p>
<p>Note: We can embed the licenses directly within the Company document as an array. Each license could be represented as an object with relevant details, such as license type, expiration date, etc.</p>
<p>Pros:</p>
<p>Simplicity in retrieval as licenses are directly associated with the company.</p>
<p>All data is stored in a single document, reducing the need for multiple queries.</p>
<p>Cons:</p>
<p>Document size limitations in MongoDB could become a concern if the number of licenses grows significantly.</p>
<p>Updating licenses might require updating the entire Company document.</p>
<p>Instead I would create a separate collection for licenses and establish a relationship with the User entity (Company entity is also possible). Each license document references the ID of the associated Company or User.</p>
<p>Pros:</p>
<p>Allows for more flexibility in managing and updating licenses independently.</p>
<p>Can handle a larger number of licenses without hitting document size limitations.</p>
<p>Cons:</p>
<p>Requires additional queries to retrieve license information when needed.</p>
<p><br /><br /></p>
<p><strong>How Microservices Look like</strong></p>
<p>User Service (Microservice 1):</p>
<ul>
<li>Manages user and company-related operations. Update user&rsquo;s name etc.</li>
<li>Stores user and company information in MongoDB/CosmosDB.</li>
<li>If it&rsquo;s an existing user, the service checks whether the max license amount is exceeded by checking the license quantity in the database</li>
<li>When a new license is created or updated, UserService updates the license quantity</li>
</ul>
<p>Order Service (Microservice 2):</p>
<ul>
<li>Handles order-related logic.</li>
<li>When a new order is created, it creates a new PaymentOrder record in MongoDB/CosmosDB</li>
<li>Communicates with PaymentService via Service Bus when a new order is generated</li>
</ul>
<p>Payment Service (Microservice 3):</p>
<ul>
<li>Integrates with Chargebee for payment processing.</li>
<li>Handles webhooks from Chargebee to update PaymentStatus in PaymentOrder table.</li>
<li>Manages payment-related operations.</li>
<li>The initial status is NOT_STARTED. When the payment service sends the payment order to the Chargebee, the status changes to EXECUTING. The payment service updates the status to SUCCESS or FAILED based on the response from Chargebee.</li>
</ul>
<p>License Service (Microservice 4):</p>
<ul>
<li>License Allocation: Tracks and manages the allocation of licenses to clients (companies).</li>
<li>Expiration Management: Monitors license expiration dates and takes appropriate actions (e.g., sending notifications, updating the status).</li>
<li>Usage Tracking: Keeps track of the number of licenses purchased by a client and their current usage.</li>
<li>License Information Storage: Stores license-related information, including expiration dates, usage, and other relevant details, in the MongoDB database. But the license itself is saved to Blob storage.</li>
<li>Communicates with the User Service to update license information based on order changes (e.g., an increase in the number of licensed users, allocate or deallocate licenses).</li>
</ul>
<p><br /><br /><br /></p>
<p><strong>A sample flow (please check </strong><strong>Chargebee_Integration.pdf</strong><strong> to see the detailed diagram);</strong></p>
<p>Having both Azure Gateway and APIM helped to centralise cross-cutting concerns such as authentication, SSL termination, and load balancing, rate limiting. Depending on the permission model, configure either a key vault access policy or Azure RBAC access for an API Management managed identity. The APIM service performs its security checks, and forwards valid requests to the downstream services in the AKS cluster. All services are secured inside a VNET.</p>
<p>User Registration/Login:</p>
<ul>
<li>Users register on the website or log in with existing credentials.</li>
<li>Upon successful authentication, the website obtains an API key or OAuth token.</li>
</ul>
<p>API Key or Token Inclusion:</p>
<ul>
<li>The website includes the API key or OAuth token in the headers of requests to the API Gateway. (save those API keys to keyvault)</li>
</ul>
<p>API Gateway Authentication:</p>
<ul>
<li>The API Gateway verifies the API key or OAuth token.</li>
<li>For user-specific actions, it may validate against the user's credentials stored in the User Service.</li>
</ul>
<p>Authorization Check:</p>
<ul>
<li>After authentication, the API Gateway checks the user's role and subscription level.</li>
<li>It ensures that the user has the necessary permissions to perform the requested action.</li>
</ul>
<p>Validated Request Forwarding:</p>
<ul>
<li>If authentication and authorization are successful, the API Gateway forwards the validated request to the appropriate microservice, User Service in this case.</li>
</ul>
<p>-&gt; User service checks whether the entered license quantity is valid (not exceeding 10) by querying the related Company table. If it&rsquo;s a new subscription then there&rsquo;s no need to check the database as the max amount is always 10.&nbsp;</p>
<p>Note: I assume there are other services for Pricing and Product. And the total amount of selected packages is calculated by checking the Pricing table.&nbsp;</p>
<p>-&gt; User service publishes to package_selected topic with details like total amount, selected package, quantity, expiry date,userId</p>
<p>-&gt; Order service subscribed to package_selected topic. And created a new PaymentOrder record;</p>
<p>{</p>
<p>"order_id": // idempotencykey</p>
<p>"userId": ObjectId("..."),&nbsp;</p>
<p>"package": "Enterprise",</p>
<p>"quantity": 5</p>
<p>"paymentStatus": "not_started"</p>
<p>"expiryDate":</p>
<p>"amount": "100.0"</p>
<p>}</p>
<p>-&gt; Order service publishes to order_created topic with all these details and Payment Service receives this information. Upon receiving the payment order information, the payment service sends a payment registration request to Chargebee. This registration request contains relevant payment details such as the amount, currency, expiration date of the payment request, and the redirect URL. To ensure unique registration and prevent duplication, a UUID field is included. This UUID corresponds to the ID of the payment order.&nbsp;</p>
<p>In the 2nd step, Chargebee returns a token to the payment service, which serves as a unique identifier for the payment registration on Chargebee side. This token enables later examination of the payment registration and payment execution status. <strong>Eg: Use non-recurring payment methods used to do recurring payments.</strong></p>
<ul>
<li><strong><strong>When the initial payment is done via iDeal and completed successfully, we store the transaction ID (token).</strong></strong></li>
</ul>
<ul>
<li><strong>When we upload the payment information to buckaroo after the billing run, we use that transaction ID (token) as OriginalTransaction.</strong></li>
</ul>
<ul>
<li><strong>Buckaroo will then do a new transaction of type SEPA Direct Debit, using the IBAN of the original iDeal transaction. </strong></li>
</ul>
<p>The payment service stores the token in the database before initiating the call to the Chargebee-hosted payment page. Once the token is saved, the client displays the Chargebee-hosted payment page.&nbsp;</p>
<p>Chargebee handles the collection of sensitive payment information, ensuring it never reaches our payment system. The hosted payment page typically requires two pieces of information:</p>
<ul>
<li>The token received in step 3: Chargebee's JS code provides this token to retrieve detailed information about the payment request from Chargebee's backend. One crucial piece of information is the amount to be collected.</li>
<li>The redirect URL: This is the web page URL that is called upon completion of the payment. When Chargebee's JS completes the payment process, it redirects the browser to the specified redirect URL.</li>
</ul>
<p>The user enters the payment information, including the credit card number, cardholder's name, expiration date, and other relevant details, on the Chargebee's webpage. After filling in the necessary information, the user clicks the pay button. Then, Chargebee initiates the payment processing procedure. In an asynchronous way, Chargebee communicates the payment status to the payment service through a webhook. During the initial setup with the Chargebee, a URL on the payment system's side is registered as the webhook. When payment events are sent to the payment system through the webhook, the payment system extracts the payment status information and updates the "payment_order_status" field in the PaymentOrder table.</p>
<p>-&gt; If the payment is successful, then Payment Service publishes a payment_successful topic. License service subscribed to this topic receives the information and generates the license. The service stores the license in Azure blob storage and then sends notification to the user using SendGrid. Then user service updates the license quantity information in the Company table.&nbsp;</p>
<p>Note: I preferred using Pub/sub mechanism, because I assumed there can be multiple services to consume the same message. For instance Payment events are published to Azure Service Bus and can subsequently be consumed by various services, including the payment system itself, an analytics service, and a billing service. This design enables the seamless distribution of payment-related information across multiple services, ensuring that each service can perform its specific tasks and process the payment events accordingly.</p>
<p>** Additional consideration: There should be a nightly-scheduled AzureWebjob to check whether there are any expiring licenses by filtering Mongodb. This can be a logic app (add a schedule and runbook to run every midnight) that puts a message in a queue called scheduled-jobs and the webjob queries MongoDB/CosmosDB to find out the licenses that are about to expire, then sends an email to those customers. If there are any licenses to be ended on the day the job runs, then the job needs to update the status of those licenses as Inactive by updating the right record in Mongodb and inform the customer by sending a notification.&nbsp;</p>
<p>Another way is to use a timer function:&nbsp;</p>
<p>In the License Service, we can create a Timer Trigger Function. This function will be triggered at regular intervals to check for licenses about to expire. We can use this function to initiate the notification process.</p>
<p>public static class LicenseExpirationCheckFunction</p>
<p>{</p>
<p>[FunctionName("LicenseExpirationCheck")]</p>
<p>public static void Run([TimerTrigger("0 0 0 * * *")] TimerInfo myTimer, ILogger log)</p>
<p>{</p>
<p>// This function runs every day at midnight (0 0 0 * * *)</p>
<p>// Implement logic to check for licenses about to expire</p>
<p>&nbsp;</p>
<p>// Trigger the process to notify users about expiring licenses</p>
<p>NotifyUsersAboutExpiringLicenses();</p>
<p>}</p>
<p>private static void NotifyUsersAboutExpiringLicenses()</p>
<p>{</p>
<p>// Implement the logic to get licenses about to expire</p>
<p>// Trigger the Notification Service to send notifications</p>
<p>}</p>
<p>}</p>
<p>Once the LicenseExpirationCheckFunction identifies licenses about to expire, it can trigger the Notification Service. This can be achieved by calling an HTTP endpoint exposed by the Notification Service or by using a message queue. The NotifyUsers function is triggered by a message in the "notificationqueue".</p>
<p>public static class NotificationService</p>
<p>{</p>
<p>[FunctionName("NotifyUsers")]</p>
<p>public static void Run([QueueTrigger("notificationqueue")] string message, ILogger log)</p>
<p>{</p>
<p>// Implement logic to send notifications to users</p>
<p>log.LogInformation($"Sending notification: {message}");</p>
<p>}</p>
<p>}</p>
<p><br /><strong>How to handle failed payments</strong></p>
<ul>
<li>Retry queue: retryable errors such as transient errors are routed to a retry queue.&nbsp;</li>
<li>Dead letter queue: if a message fails repeatedly, it eventually lands in the dead letter queue. A dead letter queue is useful for debugging and isolating problematic messages for inspection to determine why they were not processed successfully.</li>
</ul>
<p>Check whether the failure is retryable.</p>
<ul>
<li>Retryable failures are routed to a retry queue.</li>
<li>For non-retryable failures such as invalid input, errors are stored in a database.</li>
</ul>
<p>The payment system consumes events from the retry queue and retries failed payment transactions.</p>
<ul>
<li>If the payment transaction fails again:</li>
<li>If the retry count doesn&rsquo;t exceed the threshold, the event is routed to the retry queue.</li>
<li>If the retry count exceeds the threshold, the event is put in the dead letter queue. Those failed events might need to be investigated.</li>
</ul>
<p>Another concern is to achieve <strong>exactly-once delivery</strong>. One of the most critical issues that a payment system can encounter is double-charging a customer. By combining retry mechanisms for at-least-once execution and implementing idempotency checks for <strong>at-most-once execution</strong>, we can create a robust and reliable payment system that ensures the execution of payment orders exactly once, mitigating the risk of double-charging customers.&nbsp;</p>
<p>Here are some common retry strategies:</p>
<ul>
<li>Immediate retry: The client promptly resends the request after a failure occurs.</li>
<li>Fixed intervals: A fixed amount of time is waited between the failed payment and subsequent retry attempts.</li>
<li>Incremental intervals: The client initially waits for a short period before the first retry and then gradually increases the waiting time for subsequent retries.</li>
<li>Exponential backoff: The waiting time between retries is doubled after each failed attempt. For instance, if the request fails the first time, a retry is attempted after 1 second. If it fails again, the next retry is attempted after 2 seconds, and so on.</li>
<li>Cancel: The client has the option to cancel the request, especially when the failure is permanent or further retries are unlikely to succeed.</li>
</ul>
<p>One potential problem with retries is the possibility of double payments.</p>
<p><strong>Scenario:</strong> What if a customer clicks the &ldquo;pay&rdquo; button quickly twice?&nbsp;</p>
<p>When a user clicks the "pay" button, an idempotency key is included in the HTTP request sent to the payment system. In the case of a second request, it is considered a retry since the payment system has already encountered the idempotency key (payment_order_id). By including the previously specified idempotency key in the request header, the payment system responds by providing the latest status of the previous request. This approach ensures that duplicate requests or retries are effectively handled and prevents unintended consequences that may arise from multiple submissions of the same payment. If multiple concurrent requests are detected with the same idempotency key, only one request is processed and the others receive the &ldquo;429 Too Many Requests&rdquo; status code.</p>
<p><strong>Scenario:</strong> The payment is successfully processed by Chargebee, but the response fails to reach our payment system due to network errors. Then the user clicks the &ldquo;pay&rdquo; again.</p>
<p>if the payment is successfully processed by Chargebee, but the response fails to reach our payment system due to network errors, and subsequently the user clicks the "pay" button again, the following scenario can occur:</p>
<ul>
<li>The second "pay" request is sent to the payment system, unaware that the initial payment was actually successful.</li>
</ul>
<p>At this point, the payment system needs to handle the duplicate request and ensure that the duplicate payment is not processed twice, preventing any unintended consequences or duplicate charges.</p>
<p>To address this situation, the payment system can implement mechanisms such as idempotency keys or unique identifiers. By including an idempotency key in the request, the payment system can identify and recognize the duplicate request. It can then determine that the payment has already been successfully processed and respond accordingly, without processing the payment again. This helps maintain data integrity and prevents any duplicate or erroneous transactions caused by network errors or user interactions.</p>
