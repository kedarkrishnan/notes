# Serverless
- Event driven compute service
- Compute service in response to HTTP request using AWS Gateway
- Node.js, Java, Python, C#, Go

- Pricing
	- Number of request: First 1 million request are free. $0.2 per 1 million request thereafter
	- Duration: time your code runs, rounded up to nearest 100ms. Depends on amount of memory you allocate to your function. $0.00001667 / GB-Sec used

- Features
	- Scales out (not up) automatically: run in parallel
	- Independent 1event = 1function
	- Serverless
	- Is a Compute service	
	- Lambda can trigger other lambda functions
	- Debug Lamdba => AWS X-ray
	- Can do things globally
	
#### API Gateway
- Features
	- Has caching capabilities
	- low cost and scales automatically
	- Can throttle API gateway tp prevent attacks
	- Log results using CloudWatch
	- Mutiple domains with API gateway -  enable CORS on API gateway
	- CORS is enforced by the client