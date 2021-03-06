# Tagging Applications<a name="applications-tagging"></a>

You can apply tags to your AWS Elastic Beanstalk applications\. Tags are key\-value pairs associated with AWS resources\. For information about Elastic Beanstalk resource tagging, use cases, tag key and value constraints, and supported resource types, see [Tagging AWS Elastic Beanstalk Application Resources](applications-tagging-resources.md)\.

You can specify tags when you create an application\. In an existing application, you can add or remove tags, and update the values of existing tags\. You can add up to 50 tags to each application\.

## Adding Tags during Application Creation<a name="applications-tagging.create"></a>

When you use the Elastic Beanstalk console to [create an application](applications.md), you can specify tag keys and values in the **Create New Application** dialog box\.

![\[Create New Application dialog box shows tags for a new application in the Elastic Beanstalk console\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/applications-create-dialog.png)

If you use the EB CLI to create an application, use the `--tags` option with [eb init](eb3-init.md) to add tags\.

```
~/workspace/my-app$ eb init --tags mytag1=value1,mytag2=value2
```

With the AWS CLI or other API\-based clients, add tags by using the `--tags` parameter on the [create\-application](https://docs.aws.amazon.com/cli/latest/reference/elasticbeanstalk/create-application.html) command\.

```
$ aws elasticbeanstalk create-application \
      --tags Key=mytag1,Value=value1 Key=mytag2,Value=value2 \
      --application-name my-app --version-label v1
```

## Managing Tags of an Existing Application<a name="applications-tagging.manage"></a>

You can add, update, and delete tags in an existing Elastic Beanstalk application\.

**To manage an application's tags in the Elastic Beanstalk console**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Choose **Actions** next to the name of the application\.

1. Choose **Manage tags**\.

   The **Manage Tags** dialog box shows the list of tags that are currently applied to the application\.  
![\[Manage Tags dialog box shows tags for an application in the Elastic Beanstalk console\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/tagging-manage-tags-dialog-app.png)

1. Add, update, or delete tags:
   + To add a tag, enter it into the empty boxes at the bottom of the list\.
   + To update a tag's key or value, edit the respective box in the tag's row\.
   + To delete a tag, choose ![\[Remove tag\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/x.png) next to the tag's value box\.

1. Choose **Apply**\.

If you use the EB CLI to update your application, use [eb tags](eb3-tags.md) to add, update, delete, or list tags\.

For example, the following command lists the tags in an application\.

```
~/workspace/my-app$ eb tags --list --resource "arn:aws:elasticbeanstalk:us-east-2:my-account-id:application/my-app"
```

The following command updates the tag `mytag1` and deletes the tag `mytag2`\.

```
~/workspace/my-app$ eb tags --update mytag1=newvalue --delete mytag2 \
      --resource "arn:aws:elasticbeanstalk:us-east-2:my-account-id:application/my-app"
```

For a complete list of options and more examples, see `[eb tags](eb3-tags.md)`\.

With the AWS CLI or other API\-based clients, use the [list\-tags\-for\-resource](https://docs.aws.amazon.com/cli/latest/reference/elasticbeanstalk/list-tags-for-resource.html) command to list the tags of an application\.

```
$ aws elasticbeanstalk list-tags-for-resource --resource-arn "arn:aws:elasticbeanstalk:us-east-2:my-account-id:application/my-app"
```

Use the [update\-tags\-for\-resource](https://docs.aws.amazon.com/cli/latest/reference/elasticbeanstalk/update-tags-for-resource.html) command to add, update, or delete tags in an application\.

```
$ aws elasticbeanstalk update-tags-for-resource \
      --tags-to-add Key=mytag1,Value=newvalue --tags-to-remove mytag2 \
      --resource-arn "arn:aws:elasticbeanstalk:us-east-2:my-account-id:application/my-app"
```

Specify both tags to add and tags to update in the `--tags-to-add` parameter of update\-tags\-for\-resource\. A nonexisting tag is added, and an existing tag's value is updated\.

**Note**  
To use some of the EB CLI and AWS CLI commands with an Elastic Beanstalk application, you need the application's ARN\. You can retrieve the ARN by using the following command\.  

```
$ aws elasticbeanstalk describe-applications --application-names my-app
```