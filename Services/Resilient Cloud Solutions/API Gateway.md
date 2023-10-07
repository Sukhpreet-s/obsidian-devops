- Provide an interface from client to communicate with AWS services publicaly.
- Configure Authentication and Authorization for endpoints
- Define endpoints that can be connected to any of the services.
- Allows integration with WebSocket

#### Endpoint Types
- Edge-Optimized (default) - For global clients
	- API Gateway lives in one Region but all the global requests are routed through CloudFront Edge locations to improve latency.
- Regional - For one region clients
	- Can manually setup CloudFront
- Private - Only access within VPC


#### Security
- User Authentication
	- IAM Roles (for internal services)
	- Cognito (for mobile/web application users)
	- Custom Authorizer (custom logic using Lambda)
- Custom Domain Name with HTTPS using Certificate Manager
	- If Edge-Optimized Gateway, then the certificate must be in us-east-1


#### Stage variables are like environment variables for API Gateway
- Format: `${stateVariables.variableName}`
- Common use case: 
	- Create a variable to indicate which lambda alias to use.


Logging - CloudWatch logs and X-Ray

Metrics (Monitoring)
- Cache monitoring - 
	- CacheHitCount, 
	- CacheMissCount, 
- IntegrationLatency - time between api gateway sends request to the backend and when it receives response from backend.
- Latency - time between request from client and response to client
- 4XXError & 5XXError metrics

Throttling
- Very similar to Lambda Concurrency throttle.
- limit: 10000 rps across all API Gateways
- 429 Too Many Requests error
- Set Stage Limit & Method Limit for better performance
- Usage Plans to throttle per customer