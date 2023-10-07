
Build instructions are stored in `buildspec.yml` file.

By default, the build process is done outside VPC.
Can specify VPC ID to have it in the VPC to access all other resources for integration testing and other stuff.


Validate Pull Requests before merging:
- EventBridge listens for any PRcreated event
- Triggers Lambda to comment on PR that it is being reviewed
- Then triggers CodeBuild to start the build/test process
- EventBridge listens for CodeBuild success/failure result
- Then triggers Lambda to update the PR

CodeBuild can use Test Reports to show test results in the UI. (Requires the testing framework to create the test report files in specific format)