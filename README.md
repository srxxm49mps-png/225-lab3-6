# 225-lab3-6
CI/CD pipeline Example.  Deploys to DEV with __ClusterIP and Ingress__, checks with Selenium, then to PROD with __LoadBalanced IP__.

1) Create a new blank repository in your GitHub account using the lab name above.
2) Copy the URL of this repository and paste it into your repository.
3) View each file, and make changes where it is commented.
4) Run your pipeline.
5) Demonstrate your changes to the code in your video, and show the resulting web page.

## This deployment

DEV: http://10.48.229.166/lab3-6/

PROD: http://10.48.229.166:8082/

`Dockerfile.build` builds the application. `Dockerfile.test` builds the
isolated Selenium/Firefox test container. The pipeline deploys DEV and waits
for its rollout, runs the acceptance test against that DEV page, and proceeds
to production only if the expected heading passes. The test container is
removed automatically after execution.

Production uses the existing MetalLB v0.14.3 single-IP pool. Each lab has a
separate LoadBalancer service and selector: Lab 3.4 on port 8080, Lab 3.5 on
8081, and this lab on 8082. All opt into the same IP-sharing key. The pipeline
verifies production IP assignment and the resulting page before success.
