
### 1. Using ELB

Elastic load balancer will route traffic to a new target group right away at once or use weighted TG.

### 2. Route 53 (DNS level)

There are multiple ELBs and want to change traffic from one ELB to another.
Little slower since clients may have previous DNS in the cache.

### 3. API Gateway

Create different stages to switch traffic. Allows Canary feature.


### 4. Lambda Alias

Change alias to point to new version using canary