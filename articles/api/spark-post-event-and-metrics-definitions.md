---
title: "SparkPost Event and Metrics Definitions"
redirect_from: "https://support.sparkpost.com/customer/portal/articles/2232381-sparkpost-event-and-metrics-definitions"
description: "Spark Post Event Definitions The follow table contains the definition of each type of event that exists for activity through Spark Post and Spark Post Enterprise NOTE Inbound relay events are only available in Spark Post Enterprise i e they are not available in Spark Post Individual events are provided..."
---

## SparkPost Event Definitions 

### The follow table contains the definition of each type of event that exists for activity through SparkPost and SparkPost Enterprise. NOTE: Inbound relay events are only available in SparkPost Enterprise, i.e., they are not available in SparkPost.Individual events are provided via the webhook data stream and can be retrieved on an on-demand basis using the Message Events API.

| **Event Name**      | **Belongs to the following Event Group**                              | **Other Names for this Event**                      | **Event Generated When:**                 |
| Injection | Injection | Reception | Message is received by or injected into SparkPost/SparkPost Elite. |
| Delivery | Delivery | 250 OK | The remote mail server (of the recipient) acknowledges receipt of message. |
| Policy_Rejection | Bounce | In Band Bounce: Admin type failure | Due to policy, SparkPost rejects message or fails to generate message. (This is most often due to suppression list activity.)  |
| Delay | Delay | Tempfail/Transfail, 4xx error code | The remote mail server (of the recipient) temporarily rejects a message (asks for delivery to be tried again later). |
| Bounce | Bounce | Permfail, 5xx error code | The remote mail server (of the recipient)  **permanently** rejects message (delivery should not be attempted later) |
| out_of_band | Bounce | Asynchronous Bounce | Remote mail server (of the recipient) initially reported acceptance of a message, but now reports that the message cannot be delivered. |
| spam_complaint |   | Complaints/FBL | The message was classified as spam by the recipient. |
| Open | Engagement | Views/Renders | Recipient opens a message in a mail client, thus rendering a tracking pixel. |
| Click | Engagement | Actions, Clickthrough | Recipient clicksa tracked link in a message, thus prompting a redirect through the SparkPost click-tracking server to the link's destination. |
| generation_failure | Bounce |   | Message generation fails for a given recipient. |
| generation_rejection | Bounce |   | SparkPost rejects message generation due to policy. |
| list_unsubscribe | Unsubscribe |   | Recipient unsubscribes by using the ISP list unsubscribe feature. |
| link_unsubscribe | Unsubscribe |   | User clicks a specifically tagged unsubscribe link. |
| relay_delivery | Inbound Relay |   | Remote HTTP endpoint acknowledgesreceipt of a relayed message. |
| relay_injection | Inbound Relay |   | Relayed message is received by or injected into SparkPost. |
| relay_rejection | Inbound Relay |   | SparkPost rejects a relayed message or fails to generate a relayed message. |
| relay_tempfail | Inbound Relay |   | Remote HTTP endpoint fails to accept a relayed message. |
| relay_permfail | Inbound Relay |   | Relayed message has reached the maximum retry threshold without delivery to the HTTP endpoint and will be removed from the system. |

**SparkPost Metrics Definitions**                    
The following contains the definition for each metric that is displayed in the SparkPost and SparkPost Elite UI. The Metrics API uses these same definitions, so results from the Metrics API will match the data displayed in the UI for the same date-time range interval.

| **Metric** | **Definition** | **Formula** | **Notes** |
| --- | --- | --- | --- |
| Targeted | Messages successfully injected into SparkPost as well as rejected by it | Injected + Rejected |   |
| Injected | Messages either injected into or received by SparkPost | Sum (Injected) |   |
| Rejected | Messages either rejected due to policy or failed to generate | Sum (Policy Rejection + Generation Failure + Generation Rejection) |   |
| Policy Rejection | Messages rejected by SparkPost due to policy | Sum (Rejected) | Note: These are also counted as Admin Bounces.
Rejected metrics includes not only the Rejection events but also include Generation Fail and Generation Rejection events |
| Rejection Rate |   | Rejected / Targeted |    |
| Generation Failure | Message generation failed for an intended recipient | Sum (Generation Failed) | When a message generation fails due to missing data or some technical reason.  This event occurs instead of a Rejection event.
Note: These are also counted as Admin Bounces. |
| Generation Rejection | Messages rejected by SparkPost due to policy | Sum (Generation Rejection) | When a message generation fails due to Policy.  This event occurs instead of a Rejection event.
Note: These are also counted as Admin Bounces. |
| Sent | Messages that SparkPost attempted to deliver, which includes both Deliveries and In-band Bounces | Deliveries + In Band Bounces |   |
| Accepted | Messages an ISP or other remote domain accepted (less Out-of-Band Bounces) | Sum (Deliveries - Out of Band Bounces) | Accepted = Sent - Bounced (EEC definition) |
| Delivered 1st Attempt | Messages delivered that required a single attempt. | Sum (Deliveries where attempt=1) |   |
| Delivered 2+ Attempts | Messages delivered that required more than one delivery attempt. | Sum (Deliveries where attempt>1) |   |
| Avg Latency 1st Attempt | Average delivery time milliseconds (latency) for messages delivered on the first attempt. | Avg (Delivery Times where attempt=1) |   |
| Avg Latency 2+ Attempts | Average delivery time in milliseconds (latency) for messages delivered that required more than one attempt. | Avg (Delivery Times where attempt>1) |   |
| Avg Delivery Message Size | Average size of delivered messages, in bytes (including attachments) | Avg (Delivery Message Size) |   |
| Delivery Message Volume | Total size of delivered messages, in bytes (including attachments) | Sum (Delivery Message Size) |   |
| Accepted Rate | Percentage or Targeted messages that were Accepted | Accepted / Targeted |   |
| Delayed | Total number of delays due to any temporary failure | Sum (Delays) | Delays are transfails; may be more than one per message.   |
| Delayed 1st Attempt | Messages delayed on the first delivery attempt | Sum (delays where attempt=1) |   |
| Delayed Rate | Percentage of Accepted messages that were delayed on the first delivery attempt | Delayed First Attempt / Accepted | Percent of messages delayed on the first attempt / Accepted * 100 |
| Bounced | Total number of bounced messages which includes both In-band and Out-of-Band bounces | Sum (Bounces)  |   |
| Soft Bounced | Total number of Bounced messages due to soft bounce classification reasons | Sum (Soft Bounces) |   |
| Hard Bounced | Total number of Bounced messages due to hard bounce classification reasons | Sum (Hard Bounces) |   |
| Block Bounced | Total number of Bounced messages due to an IP block | Sum (Block Bounces) |   |
| Admin Bounced | Total number of Bounced messages due to admin bounce classification reasons, also includes Rejected | Sum (Admin Bounces) | Includes rejections, generation failures, and generation rejections |
| Undetermined Bounced | Total number of Bounced messages due to undetermined bounce reasons | Sum (Undetermined Bounces) |   |
| All Bounce Rate | Percentage of Targeted messages that Bounced | Sum (Bounces / Targeted) * 100 |   |
| Soft Bounce Rate | Percentage of Targeted messages that Soft Bounced | Sum (Soft Bounces / Targeted) * 100 |   |
| Hard Bounce Rate | Percentage of Targeted messages that Hard Bounced | Sum (Hard Bounces / Targeted) * 100 |   |
| Block Bounce Rate | Percentage of Targeted messages that Block Bounced | Sum (Block Bounces / Targeted) * 100 |   |
| Admin Bounce Rate | Percentage of Targeted messages that Admin Bounced | Sum (Admin Bounces / Targeted) * 100 |   |
| Undetermined Bounce Rate | Percentage of Targeted messages that Undertermined Bounced | Sum (Undetermined Bounces / Targeted) * 100 |   |
| Spam Complaints | Number of spam complaints received from an ISP | sum (spam) |   |
| Clicks | Total number of times that links were selected across all messages | Sum (clicks) | Total number of clicks (non-unique click events) |
| Raw Clicks | Total number of links selected at least once across all messages | Sum (distinct links clicks per message) | 

*   Number of tracking links times the number of Recipients who clicked on them.
*   e.g. 4 recipients clicking on 2 different tracking links = 8 Raw Clicked, even if they clicked 20 times on the same link
*   Number of unique tracking links clicked **per unique message**               

 |
| Unique Clicks (approx.) | The estimated number of messages, within a 5% variance, which had at least one link selected one or more times. |   |   |
| Unique Clicks | Total number of messages which had at least one link selected one or more times. (This metric may take longer to display.) | Sum (distinct messages clicked at least once) | Number of **unique messages**          that had a clicked link |
| Click-through Rate (approx.) | Click-through Rate using the Unique Clicks (approx.) metric | Unique Clicks (approx.) / Targeted |   |
| Click-through Rate | Percentage of Targeted messages that had at least one link selected | Unique Clicks / Targeted |   |
| Unique Rendered (approx.) | The estimated number of messages, within a 5% variance, that were rendered at least once. |   |   |
| Unique Rendered/Opened | Total number of messages that were rendered at least once.(This metric may take longer to display.) | Sum (distinct messages opened at least once) | 

*   The unique number of Recipients that an message is displayed (whether fully opened or within the preview pane) and recorded using a tracking pixel. I.e. **unique messages**          opened.
*   If a user opens the message multiple times or multiple tracking pixel requests are recorded due to forwarding, only one is counted per unique email address.
*   This metric applies to HTML formatted emails only. (EEC Definition)

 |
| Rendered/Opens | Total renderings of a message | Sum (messages opened) | 

*   The total number of times a **message** is displayed (whether fully opened or within the preview pane) and recorded using a tracking pixel for a unique subscriber address. If the Recipient opens the email multiple times, one email render is counted for each occurrence.   Non-distinct.
*   This metric applies to HTML formatted emails only.

 |
| Unique Confirmed Opens (approx.) | The estimated number of messages, within a 5% variance, that were either rendered or had at least one link selected. |   |   |
| Unique Confirmed Opens | Total number of messages that were either rendered or had at least one link selected. (This metric may take longer to display.) | Sum (unique messages opened or clicked) | The unique number of **unique messages**          opened (whether fully opened or within the preview pane) and recorded using a tracking pixel OR if images are blocked and the user clicks any link including the unsubscribe link.  Includes Opened OR Clicked unique messages. |
| Open Rate (approx.) | Open Rate using the Unique Confirmed Opens (approx.) metric | Unique Confirmed Opens (approx.) / Targeted |   |
| Open Rate | Percentage of Targeted messages that were either rendered or had at least one link selected | Unique Confirmed Opens / Targeted |   |