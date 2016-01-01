

Go to domain_name > OCSG > server_name > Communication Services > Plugin_app_subscription

If not, domain_name -> Deployments -> Install and select in the path /opt/ocsg510/ocsg_5.1/applications ,  wlng_nt_app_subscription.ear

check Install this deployment as an application and Next and Finish.

Repeat the process for the EAR file wlng_at_app_subscription_rest.ear

And go to domain_name > OCSG > server_name > Container Services > Plugin Manager. Select Operations tab and choose Create Plugin Instance

Fill the fields:
* PluginServiceId: Plugin_app_subscription
* PluginInstanceId: Plugin_app_subscription_instance

Invoke, you should receive an "Operation invoked successfully" message.

Now go to Domain_name > OCSG > server_name > Communication Services > Plugin_app_subscription_instance#5.1.0.3.0

The plugin is correctly deployed.

Fo to domain_name > OCSG > server_name > Container Services > Plugin Manager. Select Operations tab and choose Add Route.

PluginInstanceId: Plugin_app_subscription_instance
AddressExpression: .*

Go to

Download the WADL:

wget http://domain_user:domain_u@localhost:8001/subscription/application.wadl

Now, in SoapUI: File > New SoapUI Project .

* Initial WSDL/WADL: choose application.wadl
* Project Name: Subscription API




NOTE: I've discovered http://0.0.0.0:8001/wls-cat/

http://docs.oracle.com/cd/E36135_01/doc.51/e37526/com_asm.htm#autoId0

http://docs.oracle.com/cd/E36135_01/doc.51/e37533/rst_asm.htm#autoId0
