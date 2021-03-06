---
title: "After Receiving a 250 OK, Why Are Messages Being Rejected?"
redirect_from: "https://support.sparkpost.com/customer/portal/articles/1929982-after-receiving-a-250-ok-why-are-messages-being-rejected-"
description: "Q I receive a 250 OK when injecting into the system through SMTP but the message shows up as rejected in the reports Why is my message being rejected A The 250 OK response indicates that the connection was properly authenticated and that the message was accepted by Spark Post..."
---

Q: I receive a 250 OK when injecting into the system through SMTP, but the message shows up as rejected in the reports. Why is my message being rejected? 

A: The 250 OK response indicates that the connection was properly authenticated and that the message was accepted by SparkPost. The subsequent rejection of the message may be due to:

1.  An unconfigured Sending Domain: The message will be rejected if you are sending from a domain that you have not yet added or configured.  Please go to [https://app.sparkpost.com/#/account/sending-domains](https://app.sparkpost.com/#/account/sending-domains) to configure your domain.
2.  Unverified Sending Domain: The message will be rejected if you are sending from a domain that has been configured but not yet verified.