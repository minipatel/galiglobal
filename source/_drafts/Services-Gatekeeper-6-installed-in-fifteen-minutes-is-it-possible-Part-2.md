title: Services Gatekeeper 6 installed in fifteen minutes, is it possible? - Part 1
date: 2015-04-30 22:00:00
categories:
- Technical
tags:
- OCSG
- Services Gatekeeper
- Service Delivery
- Oracle
---


Oracle Communications [Services Gatekeeper 6](http://www.oracle.com/us/products/applications/communications/connected-digital-lifestyle/services-gatekeeper/overview/index.html), the industry-leading API exposure platform, is Generally Available and with many new and interesting features. One of them is the simplified configuration and deployment with installation in 15 minutes, based on lightweight single tier deployment option. I really like the idea, it's going to help with Proofs of Concept and Training. So in this article, I am going to review this feature: a fight against the clock to know how many time an OCSG student needs to deploy OCSG. 

![Services Gatekeeper Standalone System](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/StandaloneOCSG6.png)

Disclaimer: some steps shouldn't be executed in production environments.

## Preparations Overview

As good practice, the first step is always check the [Supported Platform Matrix](http://docs.oracle.com/cd/E50778_01/doc.60/e50756/ins_sysreq.htm#SGINS122). For this installation, we have the following pre-requisites:

1. Oracle Linux 6: in this case, it is version 6.6 x64, you can download it from [Oracle Software Delivery Cloud](https://edelivery.oracle.com/linux). It may run hosted in an [Oracle Virtualbox environment](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html). 
2. JDK 1.7 installed: in this case, Java SE Development Kit 7u75 for Linux x64 (tgz). You can download it from [Oracle Java SE Development Kit 7 Downloads](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html).
3. Access as root user and also as oracle user. 

## OCSG installation

1. Login to [Oracle Software Delivery Cloud](https://edelivery.oracle.com/), choose *Oracle Communications* in **Select a Product Pack** and *Linux x86-64* and click on **Go**.

2. Click on *Oracle Communications Services Gatekeeper 6.0*. Download Oracle Communications Services Gatekeeper 6.0 Software, V73995-01.zip and copy it into the VM.

3. Open a Terminal and execute:

```sh
sudo mkdir /opt/ocsg6
sudo chown oracle:oracle /opt/ocsg6
```

4. Unzip the file and execute the installer:

```sh
unzip V73995-01.zip
java -jar ocsg_generic.jar
```

5. In the first window, accept the default Inventory Directory pressing **OK**.

![Inventory Screen](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/Inventory.png)

6. The Welcome screen appears, press **Next**.

![Welcome Screen](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/Welcome.png)

7. Introduce */opt/ocsg6* in the Oracle Home field and press **Next**.

![Location Screen](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/Location.png)

8. Select *Custom Installation* and press **Next**. Check all the features and press **Next**.

![Custom Installation](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/AllFeatures.png)

9. The Prerequisite Check should be OK. Press **Next**.

10. Note the IP in the first field. Introduce the password for the domain user and for the Partner and API Management Portal user. It's *welcome1* in my case but you can use something different. Let the default value in others fields and press **Next**.

![Credentials](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/Credentials.png)

11. Introduce the IP in /etc/hosts with **ocsg** as reference. If you ping **ocsg**, you should receive a response from the IP you've noted in the previous step.

12. Let *Java DB* selected and press **Next**.

![JavaDB](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/Javadb.png)

13. Review the Installation Summary and press **Install**. It may take a while.

![Installation End](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/IntallationEnd.png)

14. Press **Next** when available and **Finish**.

## Start OCSG

1. Open a Terminal and execute:

```sh
cd /opt/ocsg6/user_projects/domains/services-gatekeeper-domain
./startWebLogic.sh
```

When it asks for username and password, introduce *weblogic* and *welcome1*. After a while, a *The server started in RUNNING mode.* message should appear.

2. Open a Terminal (or a tab in the previous one) and execute:

```sh
cd /opt/ocsg6/user_projects/domains/services-gatekeeper-domain/bin
./startGatekeeper.sh
```
When it asks for username and password, introduce *weblogic* and *welcome1*. After a while, *The server started in RUNNING mode.* message should appear.

## Account configuration

1. Open Firefox and go to [http://ocsg:7001/console](http://ocsg:7001/console) , login as **weblogic** with password **welcome1**. In the Domain Structure (left), go to **OCSG** -> **Server 1**. In the Oracle Communications Services Gatekeeper box, click on **Container Services** and **PluginManager**.

![Container Services](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/ContainerServices.png)

2. Click on **Operations tab** and choose *createPluginInstance* in the **Select An Operation:** combo. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **PluginServiceId**: *Plugin_px21_short_messaging_smpp*
  * **PluginInstanceId**: *Plugin_px21_short_messaging_smpp_instance*

![Create Plugin Instance](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/CreatePluginInstance.png)

3. Choose *Add Route* in the **Select An Operation:** combo. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **PluginInstanceId**: *Plugin_px21_short_messaging_smpp_instance*
  * **AddressExpression**: *.**

![add Route](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/addRoute.png)

4. Go to **Container Services -> Application Groups -> addServiceProviderGroup**. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **ServiceProviderGroupIdentifier**: *default_sp_group*
  * **Properties**: *.**

![Service Provider Group](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/serviceProviderGroup.png)

5. Go to **Container Services -> ApplicationGroups -> addApplicationGroup**. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **ApplicationGroupIdentifier**: *default_app_group*

![Application Group](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/ApplicationgGroup.png)

6. Go to **Container Services -> ApplicationAccounts -> addServiceProviderAccount**. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **ServiceProviderIdentifier:**: *default_sp*
  * **ServiceProviderGroupIdentifier**: *default_sp_group*
  * **Reference**: *default*

![Service Provider Account](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/serviceProviderAccount.png)

7. Go to **Container Services -> ApplicationAccounts -> addApplicationAccount**. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **ApplicationIdentifier:**: *default_app*
  * **ServiceProviderIdentifier:**: *default_sp*
  * **ApplicationGroupIdentifier**: *default_sp_group*
  * **Reference**: *default*

![Application Account](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/ApplicationAccount.png)

8. Go to **Container Services -> ApplicationInstances -> addApplicationInstance**. Fill the fields with the following values and click on **Invoke**. An *Operation invoked successfully* message should be returned.
  * **ApplicationInstanceName:** *domain_user*
  * **Password:** *domain_user*
  * **ApplicationIdentifier:**: *default_app*
  * **ServiceProviderIdentifier:**: *default_sp*
  * **Reference**: *default*

![Application Instance](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/ApplicationInstance.png)

## Platform Test Environment (PTE) Installation

1. Login to [Oracle Software Delivery Cloud](https://edelivery.oracle.com/), choose *Oracle Communications* in **Select a Product Pack** and *Linux x86-64* and click on **Go**. Click on *Oracle Communications Services Gatekeeper 6.0*.

2. Download Oracle Communications Services Gatekeeper 6.0 Platform Test Environment, V73999-01.zip and copy it into the VM.

3. Unzip the file and execute the installer:

```sh
unzip V73999-01.zip
java -jar ocsg_pte_generic.jar
```

4. In the first window, accept the default Inventory Directory pressing **OK**.

5. The Welcome screen appears, press **Next**.

6. Introduce */opt/ocsg6* in the Oracle Home field and press **Next**.

7. Let **PTE Installation** selected and press **Next**.

![PTE Installation](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/installationPTE.png)

8. Review the Installation Summary and press **Install**. It may take a while. Press **Next** when available and **Finish**.

![PTE Installation Done](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/installationPTEDone.png)

## Start the PTE

1. Open a new Terminal and execute the following commands. 

```sh
cd /opt/ocsg6/ocsg_pte/
./run.sh
```

2. The PTE should appear:

![The PTE](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/PTE.png)

3. Go to **Tools -> Variables Manager** or press **Ctrl+3**.

![Variables Manager Menu](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/VariablesManagerMenu.png)

4. Change the following fields and press **OK**:
  * **at.host:** *ocsg*
  * **nt.host:** *ocsg*

![Variables Manager Screen](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/VariablesManager.png)

5. Click on **Server** and change the following fields:
  * **Hostname:** *ocsg*
  * **Port:** *8001*
  * **Username:** *weblogic*
  * **Password:** *welcome1*

![Server Credentials](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/ServerCredentials.png)

6. Go to **Tools -> SLA Manager** or press **Ctrl+1**.

![SLA Manager Menu](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/SLAManagerMenu.png)

7. Select **default_app_group** and click on the pencil icon.

![Default App Group SLA](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/default_app_group.png)

8. Click on the globe icon with a green arrow pointing up and press **Local**. The message *The SLA was succesfully uploaded to OCSG* should appear. Press **OK** twice.

![Default App Group SLA Done](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/default_app_group_done.png)

9. Select **default_sp_group** and click on the pencil icon. Click on the globe icon with a up arrow and press **Local**. The message *The SLA was succesfully uploaded to OCSG* should appear. Press **OK** twice.

10. Go to **Simulators -> SMPP** and click on **Start**. The button will change to **Stop**.

![SMPP Simulator](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/SMPPSimulator.png)

## Final test: send SMS

1. In the PTE, go to **Clients -> Login** and press **Login** (green arrow). The button should change to **Logout** (red square).

![Client Login](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/login.png)

2. Go to **Messaging -> Short Messaging -> Application-initiated** and change the message to *Hello SaNE!*. Click on **Send** (green arrow).

![Send SMS](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/sendSMS.png)

3. Go to the **Map**, click on the second button over the phone **1234** and choose *Read messages*. Here it is!!

![SMS Sent](/images/Services-Gatekeeper-6-installed-in-fifteen-minutes-is-it-possible/SMS.png)

## Conclusion

Probably you have spent more than fifteen minutes to arrive here... but it's also true most of the actions are part of the configuration, not the installation. The process is straightforward and it can be easily explained. Even if you don't have advanced knowledge of Weblogic or Linux, it's possible to do it. So, as we can see in this article, OCSG is very easy to install now and it has a lot of features deployed out-of-the-box. Because it's a so extensive application supporting a huge number of business possibilities (Service API Exposure, Direct Carrier Billing, Policy Gateway, etc. ), a basic fresh installation is a very powerful way to focus in the functionality and forget problems with databases, OS and other technical questions and now we can have it in only 15 minutes!

