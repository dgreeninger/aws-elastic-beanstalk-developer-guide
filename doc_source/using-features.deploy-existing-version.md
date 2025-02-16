# Deploying Applications to AWS Elastic Beanstalk Environments<a name="using-features.deploy-existing-version"></a>

You can use the AWS Management Console to upload an updated [source bundle](applications-sourcebundle.md) and deploy it to your AWS Elastic Beanstalk environment, or redeploy a previously uploaded version\.

Deploying a new version of your application to an environment is typically a fairly quick process\. The new source bundle is deployed to an instance and extracted\. Then the web container or application server picks up the new version and, if necessary, restarts\. During deployment, your application might still become unavailable to users for a few seconds\. You can prevent this by configuring your environment to use [rolling deployments](using-features.rolling-version-deploy.md) to deploy the new version to instances in batches\.

Each deployment is identified by a deployment ID\. Deployment IDs start at `1` and increment by one with each deployment and instance configuration change\. If you enable [enhanced health reporting](health-enhanced.md), Elastic Beanstalk displays the deployment ID in both the [health console](health-enhanced-console.md) and the [EB CLI](health-enhanced-ebcli.md) when it reports instance health status\. The deployment ID helps you determine the state of your environment when a rolling update fails\.

To ensure that your application source is always deployed to new instances, instead of updating existing instances, you can configure your environment to use [immutable updates](environmentmgmt-updates-immutable.md) for deployments\. In an immutable update, a second Auto Scaling group is launched in your environment and the new version serves traffic alongside the old version until the new instances pass health checks\.

**Warning**  
During managed platform updates with instance replacement enabled, immutable updates, and deployments with immutable updates enabled all instances are replaced\. This causes all accumulated [Amazon EC2 Burst Balances](https://docs.aws.amazon.com/AWSEC2/latest/DeveloperGuide/burstable-performance-instances.html) to be lost\.


**Supported Deployment Policies**  

| Deployment Policy | Load\-Balanced Environments | Single\-Instance Environments | Legacy Windows Server Environments† | 
| --- | --- | --- | --- | 
|  All at Once  |  ✓  |  ✓  |  ✓  | 
|  Rolling  |  ✓  |  ☓  |  ✓  | 
|  Rolling with an Additional Batch  |  ✓  |  ☓  |  ☓  | 
|  Immutable  |  ✓  |  ✓  |  ☓  | 

† For the purpose of this table, a *Legacy Windows Server Environment* is an environment based on a [Windows Server platform configuration](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.net) that use an IIS version earlier than IIS 8\.5\.

**To configure deployments**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Navigate to the [management page](environments-console.md) for your environment\.

1. Choose **Configuration**\.

1. In the **Rolling updates and deployments** configuration category, choose **Modify**\.

1. In the **Application Deployments** section, choose a [Deployment policy](using-features.rolling-version-deploy.md) and batch settings\.

1. Choose **Apply**\.

For deployments that depend on resource configuration changes or a new version that can't run alongside the old version, you can launch a new environment with the new version and perform a CNAME swap for a [blue/green deployment](using-features.CNAMESwap.md)\.

The following table compares deployment methods\.


**Deployment Methods**  

| **Method** | **Impact of Failed Deployment** | **Deploy Time** | **Zero Downtime** | **No DNS Change** | **Rollback Process** | **Code Deployed To** | 
| --- | --- | --- | --- | --- | --- | --- | 
| All at once | Downtime | ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png) | ☓ | ✓ | Manual Redeploy | Existing instances | 
| Rolling | Single batch out of service; any successful batches before failure running new application version | ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)† | ✓ | ✓ | Manual Redeploy | Existing instances | 
| Rolling with additional batch | Minimal if first batch fails; otherwise, similar to Rolling | ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)† | ✓ | ✓ | Manual Redeploy | New and existing instances | 
| Immutable | Minimal | ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png) | ✓ | ✓ | Terminate New Instances | New instances | 
| Blue/green | Minimal | ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/clock.png) | ✓ | ☓ | Swap URL | New instances | 

† *Varies depending on batch size\.*

If you deploy often, consider using the [Elastic Beanstalk Command Line Interface](eb-cli3.md) \(EB CLI\) to manage your environments\. The EB CLI creates a repository alongside your source code and can create a source bundle, upload it to Elastic Beanstalk, and deploy it with a single command\.

## Deploying a New Application Version<a name="deployments-newversion"></a>

You can perform deployments from your environment's dashboard\.

**To deploy a new application version to an Elastic Beanstalk environment**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Navigate to the [management page](environments-console.md) for your environment\.

1. Choose **Upload and Deploy**\.

1. Choose **Browse** to select the application source bundle for the application version you want to deploy\.  
![\[The Upload and Deploy dialog box\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-app-version-upload-loadbalancing.png)

1. Type a unique **Version label** to represent the new application version\.

1. Choose **Deploy**\.

## Redeploying a Previous Version<a name="deployments-existingversion"></a>

You can also deploy a previously uploaded version of your application to any of its environments from the application versions page\. 

**To deploy an existing application version to an existing environment**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Choose **Actions** next to the application name, and then choose **View application versions**\.

1. Select the application version to deploy, and then click **Deploy**\.

1. Choose an environment, and then choose **Deploy**\.