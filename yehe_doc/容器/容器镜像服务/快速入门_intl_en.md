This document describes how to purchase an instance of Tencent Container Registry (TCR) Enterprise Edition, configure the network access policy, and push and pull container images.  
To use TCR Personal Edition, please see [Image Registry User Guide](https://intl.cloud.tencent.com/document/product/457/9117).


## Step 1: Signing up for a Tencent Cloud Account
If you already have a Tencent Cloud account, ignore this step.  
If you have not, go to the [Sign up](https://intl.cloud.tencent.com/register) page and register an account.

<span id ="domain"></span>

## Step 2: Purchasing an Enterprise Edition Instance


>! If your enterprise has not activated the TCR service, activate it and authorize TCR to access your COS and VPC resources. To activate TCR, use a root account or a sub-account with admin permissions. If you are using a sub-account, grant the sub-account corresponding permissions first. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).


1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and go to the "Instance List" page.
2. Click **Create**. On the TCR purchase page, purchase an instance by referring to the following information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/08381f45c1058bce009f1359eed985ab.png)
 - **Billing Mode**: TCR is billed in pay-as-you-go mode. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1051/35483).
 - **Instance Name**: enter a custom instance name. The name must be globally unique and cannot be identical with an existing instance name of your own or another user. This name is used as the access domain name of this TCR instance. **The name cannot be modified after creation.** We recommend that you use an abbreviation that combines the company name and instance region or project as the instance name.
 - **Instance Region**: select a region where you want to deploy the instance. **The region cannot be changed after the instance is created**. Select the region based on the location of the container cluster resources.
 - **Instance Specification**: select the instance specifications that you want to purchase. Different instance specifications have different instance performance levels and quotas. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1051/35483).
 - **Instance Domain Name**: the instance domain name that is automatically generated. Its prefix is the same as that of the instance name. **The instance domain name cannot be modified after the instance is created.** This domain name is used when you run the `docker login` command to log in to the instance.
 - **Backend Storage**: when an instance is created, a Tencent Cloud COS bucket will be automatically created and associated under the current account. Images and other data in the instance will be stored in the bucket, incurring storage and traffic costs. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871). After instance creation, you can go to the COS console to view the bucket. Avoid mistakenly deleting the bucket. Otherwise, data such as images hosted in the instance will be lost.
 - **Instance Tag**: bind the newly created instance to a Tencent Cloud tag. You can also bind and edit tags on the instance details page after instance creation.
4. Read and agree to the TCR Service Agreement.
   Enterprise edition instances are billed differently based on their region and specifications. Please confirm the selected specifications and configuration fees after configuring the basic information.
5. After ticking the selected option, click **Buy Now** to purchase the enterprise edition instance you have selected and configured.
6. You can check the instance purchase progress on the "Instance List" page. When the instance state changes to "Running", the instance has been successfully purchased and is available. You can complete the following steps to configure the access control policy of the instance and log in to the instance to push and pull images.

<span id ="network"></span>

## Step 3: Configuring the Network Access Policy

To protect your data, all Internet and private network access requests are denied by default after the instance is created. Before you log in to the instance and push and pull images, you must configure the network access policy.
Click **Network ACL** in the left sidebar of the console, select **Public network** or **Private network** as needed, and configure the network access policy by referring to the following procedure.
### Private network access (recommended)
> ? To use this service in TKE, refer to [Using a Container Image in a TCR Enterprise Instance to Create a Workload](https://intl.cloud.tencent.com/document/product/457/36838) to configure the network access policy.
> We recommend that you push and pull container images through private network access because it can significantly accelerate the push and pull speeds and reduce public network traffic costs. In addition, you can manage private network access links to specify the VPCs that are allowed to access your image data and improve data security.
>

1. In the upper part of the "Private network" page, select the created instance.
2. Click **Create**. In the "Create a private network access linkage" window, configure the VPC and subnet information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/124639a65dc47d9fe0254ce897afa11a.png)
Select the VPC where the container cluster to access the image repository is located and select any subnet in this VPC that has usable private IP addresses.
3. After the private network access link is successfully established, implement private network domain name resolution by [using VPC resolution VPCDNS for automatic configuration](https://intl.cloud.tencent.com/document/product/1051/35492) or [using the TCR plug-in for automatic configuration](https://intl.cloud.tencent.com/document/product/1051/35492). For more information, see [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).

### Internet access
> ! Enabling the Internet access entry opens your dedicated instance in the public network environment. We recommend that you disable the Internet access entry as soon as possible after completing private network access configuration.
>
1. In the upper part of the "Public network" page, select the created instance.
2. Click **Open Internet Access Entry** in the upper left corner. The button status changes to **Opening**, as shown in the figure below.
After Internet access is enabled, the Docker client can access the image repositories through the Internet.
![](https://main.qcloudimg.com/raw/31ae2358e87e596ef12f4b8b9e5cb523.png)
3. When the button status changes from **Opening** to **Close Internet Access Entry**, Internet access has been successfully enabled. Then, click **Add a public IP to allowlist** in the upper left of the list to add the public IP addresses that are allowed to access the image repositories.
4. In the "Create Public Network Access Allowlist" window, add the public IP addresses or IP ranges that are allowed to access the image repositories and add remarks for this rule (optional), as shown in the figure below.
We do not recommend that you add `0.0.0.0/0` to allow all Internet access. Alternatively, delete this rule before formally activating the instance.
![](https://main.qcloudimg.com/raw/b593fe4891d6cf1a74da21d795b0011a.png)

## Step 4: Creating a Namespace
1. Select **Namespace** in the left sidebar. On the "Namespace" page that appears, click "Create".
>? Namespaces are used to manage image repositories in the instance. They do not directly store container images, but can map to teams, product projects, or other custom layers in an enterprise.
>
2. In the "Create a Namespace" window, configure the namespace information and click **OK**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/2f3af5bfcb131ce96fa0c86876722dc7.png)
 - **Name**: we recommend that you set this parameter to the name of an enterprise team or product project. Namespace names must be unique in an instance.
 - **Access Level**: you can select either **Private** or **Public**. Image repositories and Helm chart repositories in the namespace will inherit this attribute. You can modify this attribute after creating the namespace.

## Step 5: (Optional) Creating an Image Repository
>? After creating a namespace, you can use the Docker client to push images to the namespace, and the corresponding image repository will be automatically created.
>
1. Click **Image Repository** in the left sidebar to go to the "Image Repository" list page.
2. Click **Create**. In the "Create an Image Repository" window, configure the image repository information and click **OK**, as shown in the figure below.
In the "Namespace" drop-down list, you can select a created namespace. "Name" can be a multi-level path, and "Detailed Description" supports the Markdown syntax.
![](https://main.qcloudimg.com/raw/71c59a7a90db11bd3cbdc1347762b60b.png)

## Step 6: Pushing and Pulling an Image
After completing the preceding steps, you have created an instance and image repository. Next, you can perform the following operations to push an image to or pull an image from the image repository.
>? In this step, you need to use a CVM or CPM with Docker installed and ensure that the target client is in the Internet or private network access allowlist defined in [Configuring the Network Access Policy](#network).  

### Logging in to the TCR instance
1. Select **Instance List** in the left sidebar and click the instance name to go to the instance management page.
2. Click the **Access Credential** tab and click **Generate a temporary login command**.
>? In this document, a temporary login command for the instance is used as an example. You can also [obtain a long-term access credential](https://intl.cloud.tencent.com/document/product/1051/37253).
>
3. In the "Temporary Login Command" window that appears, click **Copy login command**.
4. In the command-line tool, run the login command that you have obtained to log in to the instance. The following shows a sample command:
```
sudo docker login demo-tcr.tencentcloudcr.com --username 1xxx1019xxxx --password eyJhbGciOiJSUzI1NiIsImtpZCI6IlZCVTY6VTVGVzpP...
```
If `Login Succeeded` is displayed in the command line tool, you have logged in to the instance successfully.



### Pushing a container image
You can create a container image on the local server or obtain a public image from Docker Hub for testing.
This document uses the official and latest Nginx image on Docker Hub as an example. In the command line tool, run the following commands sequentially to push this image. Replace `demo-tcr`, `project-a`, and `nginx` with the actual instance, namespace, and image repository names you have created.
```
sudo docker tag nginx:latest demo-tcr.tencentcloudcr.com/project-a/nginx:latest
```
```
sudo docker push demo-tcr.tencentcloudcr.com/project-a/nginx:latest
```

### Pulling a container image
This document uses a successfully pushed Nginx image as an example. In the command line tool, run the following command to pull this image:
```
sudo docker pull demo-tcr.tencentcloudcr.com/project-a/nginx:latest
```

## Related Documents
TCR Enterprise Edition provides advanced features such as Helm chart hosting, cross-region instance synchronization, and image security scanning. To use them, refer to the following documents:
- [Managing Helm charts](https://intl.cloud.tencent.com/document/product/1051/35493)
- [Configuring instance synchronization](https://intl.cloud.tencent.com/document/product/1051/35494)
- [Managing triggers](https://intl.cloud.tencent.com/document/product/1051/37254)
- [Network access control](https://intl.cloud.tencent.com/document/product/1051/35490)
- [Access permission management](https://intl.cloud.tencent.com/document/product/1051/37246)


## What If a Problem Occurs?
If you encounter a problem while using TCR, locate and solve the problem by referring to the [FAQ](https://intl.cloud.tencent.com/document/product/1051/37243). Alternatively, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will solve the problem for you as soon as possible.
