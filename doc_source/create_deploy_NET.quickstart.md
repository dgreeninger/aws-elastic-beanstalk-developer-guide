# Tutorial: How to Deploy a \.NET Sample Application Using AWS Elastic Beanstalk<a name="create_deploy_NET.quickstart"></a>

In this tutorial, you will learn how to deploy a \.NET sample application to AWS Elastic Beanstalk using the AWS Toolkit for Visual Studio\.

**Note**  
This tutorial uses a sample ASP\.NET Web application that you can download [here](samples/dotnet-aspmvc5-v1.zip)\. It also uses the [Toolkit for Visual Studio](https://aws.amazon.com/visualstudio/) and was tested using Visual Studio Professional 2012\.

## Create the Environment<a name="aws-elastic-beanstalk-tutorial-step-1-create-environment"></a>

First, use the Create New Application wizard in the Elastic Beanstalk console to create the application environment\. For **Platform**, choose **\.NET**\.

**To launch an environment \(console\)**

1. Open the Elastic Beanstalk console using this preconfigured link: [console\.aws\.amazon\.com/elasticbeanstalk/home\#/newApplication?applicationName=tutorials&environmentType=LoadBalanced](https://console.aws.amazon.com/elasticbeanstalk/home#/newApplication?applicationName=tutorials&environmentType=LoadBalanced)

1. For **Platform**, choose the platform that matches the language used by your application\.

1. For **Application code**, choose **Sample application**\.

1. Choose **Review and launch**\.

1. Review the available options\. When you're satisfied with them, choose **Create app**\.

When the environmentis up and running, add an Amazon RDS database instance that the application uses to store data\. For **DB engine**, choose **sqlserver\-ex**\.

**To add a DB instance to your environment**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Navigate to the [management page](environments-console.md) for your environment\.

1. Choose **Configuration**\.

1. In the **Database** configuration category, choose **Modify**\.

1. Choose a DB engine, and enter a user name and password\.

1. Choose **Apply**\.

## Publish Your Application to Elastic Beanstalk<a name="aws-elastic-beanstalk-tutorial-step-2-publish-application"></a>

Use the AWS Toolkit for Visual Studio to publish your application to Elastic Beanstalk\.

**To publish your application to Elastic Beanstalk**

1. Ensure that your environment launched successfully by checking the **Health** status in the Elastic Beanstalk console\. It should be **Green**\.  
![\[Elastic Beanstalk .NET tutorial environment health Green\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-environment-health-green.png)

1. In Visual Studio, open **BeanstalkDotNetSample\.sln**\.
**Note**  
If you haven't done so already, you can get the sample [here](samples/dotnet-aspmvc5-v1.zip)\.

1. On the **View** menu, choose **Solution Explorer**\.

1. Expand **Solution ‘BeanstalkDotNetSample’ \(2 projects\)**\.

1. Open the context \(right\-click\) menu for **MVC5App**, and then choose **Publish to AWS**\.  
![\[Elastic Beanstalk .NET tutorial Solution Explorer Publish to AWS\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-visual-studio-solution-explorer.png)

1. On the **Publish to AWS Elastic Beanstalk** page, for **Deployment Target**, choose the environment that you just created, and then choose **Next**\.  
![\[Elastic Beanstalk .NET tutorial Publish to AWS Elastic Beanstalk Deployment Target\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-visual-studio-publish-to-aws-elastic-beanstalk.png)

1. On the **Application Options** page, accept all of the defaults, and then choose **Next**\.  
![\[Elastic Beanstalk .NET tutorial Publish to AWS Elastic Beanstalk Application Options\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-visual-studio-application-options.png)

1. On the **Review** page, choose **Deploy**\.  
![\[Elastic Beanstalk .NET tutorial Review and Deploy\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-visual-studio-review-and-deploy.png)

1. If you want to monitor deployment status, use the **NuGet Package Manager** in Visual Studio\.  
![\[Elastic Beanstalk .NET tutorial monitor status NuGet Package Manager\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-visual-studio-nuget-package-manager.png)

   When the application has successfully been deployed, the **Output** box displays **completed successfully**\.  
![\[Elastic Beanstalk .NET tutorial output completed successfully\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-visual-studio-output-completed-successfully.png)

1. Return to the Elastic Beanstalk console and choose the name of the application, which appears next to the environment name\.  
![\[Elastic Beanstalk .NET tutorial launch sample app from console\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-launch-sample-app-from-console.png)

   Your ASP\.NET application opens in a new tab\.  
![\[Elastic Beanstalk .NET tutorial see your ASP.NET application running in the Web browser\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/dot-net-tutorial-my-asp-net-application.png)

## Clean Up Your AWS Resources<a name="aws-elastic-beanstalk-tutorial-step-3-clean-up-your-resources"></a>

After your application has deployed successfully, learn more about Elastic Beanstalk by [watching the video](http://bit.ly/1sSvFzg) in the application\.

If you are done working with Elastic Beanstalk for now, you can terminate your \.NET environment\.

**To terminate your Elastic Beanstalk environment**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Navigate to the [management page](environments-console.md) for your environment\.

1. Choose **Actions** and then choose **Terminate Environment**\.

Elastic Beanstalk cleans up all AWS resources associated with your environment, including EC2 instances, DB instance, load balancer, security groups, CloudWatch alarms, etc\.

For more information, see [Creating and Deploying Elastic Beanstalk Applications in \.NET Using AWS Toolkit for Visual Studio](create_deploy_NET.md), the [ AWS \.NET Development Blog ](http://aws.amazon.com/blogs/developer/category/net/), or the [AWS Application Management Blog](http://aws.amazon.com/blogs/devops/)\.