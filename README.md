# Salesforce Embedded Service Chat Module for Titanium (iOS & Android)

This module is based on Salesforce Embedded Service Chat SDK:
[iOS SDK](https://developer.salesforce.com/docs/atlas.en-us.service_sdk_ios.meta/service_sdk_ios/servicesdk_ios_dev_guide.htm)
[Android SDK](https://developer.salesforce.com/docs/atlas.en-us.noversion.service_sdk_android.meta/service_sdk_android/servicesdk_android_dev_guide.htm)

It allows you to use the Embedded Service Chat from Salesforce (Einstein bots and real agents chat transfer) which requires a Salesforce account and some backend work to enable bots, design flows and customise UX experience.

This module is a start point. It was created with a specific use case in mind, but I hope it may help if you need to support ESC or more complex Salesforce features. 

# Use the module

    const SFChat = require('com.inzori.salesforcechat');

Required IDs from Salesforce account:

    const podName = 'x.yy-zz-www.salesforceliveagent.com';
    const orgId = 'YOU_ORGANIZATION_ID';
    const deploymentId ='YOUR_DEPLOYMENT_ID';
    const buttonId = 'YOUR_BUTTON_ID';

Listen to events:

    SFChat.addEventListener("salesforce_chat:session_info", onSessionInfo);
    SFChat.addEventListener("salesforce_chat:session_state", onStateChange);
    SFChat.addEventListener("salesforce_chat:session_end", onSessionEnd);
    SFChat.addEventListener("salesforce_chat:session_error", onSessionError);
    SFChat.addEventListener("salesforce_chat:session_event", onSessionEvent);

Define the Contact and Case data you will send to Salesforce in order to find/create an existent or new Contact. A new Case will be created and associated with this contact if you want.

    // Contact
    const firstName = 'Jack';
    const lastName = 'Sparrow';
    const email = 'jack@blackpearl.com';
    const phone = '555-PIRATES';

    // Case
    const subject = 'Lost my treasure';
    const origin = 'Black Pearl mobile app';
	
A few options, all of them work except `showPrechatFields` because I don't need this UI and I haven't implemented it on the code. It allows the user to enter Name, Email and all the fields you need before trying to connect to the chat. I already have these data from the logged in user. 

    defaultToMinimized (true/false) // start chat UI minimized
    allowURLPreview (true/false) // allow URLs in the chat
    allowMinimization (true/false) // allow the UI to be minimized
    createSalesforceCase (true/false) // create a CASE associated with Contact
    debug (true/false) // debug logs on Salesforce backend
    showPrechatFields (true/false) // show UI so the user enters name, email, etc (doesn't work yet)

	
Launch standard Live Chat UI:

    SFChat.launchChat({
    	podName,
    	orgId,
    	deploymentId,
    	buttonId,
    	firstName,
    	lastName,
    	email,
    	phone,
    	subject,
    	caseOrigin,
    	defaultToMinimized,
    	allowURLPreview,
    	allowMinimization,
    	showPrechatFields,
    	createSalesforceCase,
    	debug
    });

