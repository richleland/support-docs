---
title: "Dedicated IP Pools"
redirect_from: "https://support.sparkpost.com/customer/portal/articles/2002977-dedicated-ip-pools"
description: "Dedicated IP addresses are available for any account with the exception of the FREE plan with no credit card details on file Any new dedicated IP address added to your account will have a neutral initial reputation which means that you will be responsible for properly warming up your new..."
---

Dedicated IP addresses are available for any account with the exception of the FREE plan with no credit card details on file. Any new dedicated IP address added to your account will have a neutral initial reputation, which means that you will be responsible for properly warming up your new IP. You can refer to our <u>[IP Warmup Overview](https://support.sparkpost.com/customer/en/portal/articles/1972209-ip-warm-up-overview?b_id=7411)</u> for a comprehensive guide to warming up your new IP.

## Purchasing Dedicated IPs 

You can provision new dedicated IPs directly to your Account via the UI.

1\. Select Account **->** Billing and then press the orange "Purchase Sending IPs" Button.
2\. You will then be prompted to choose:

*   Quantity: the number of dedicated IPs***** (additional monthly charges of $20.00 / IP Address / Month apply)
*   IP Pool: whether you would like to assign these addresses to an existing IP pool or create a new IP Pool
    *   If you choose to create a new pool, note that IP Pool names are limited to at most 20 letters and/or numbers. The resulting pool will also have an IP Pool Id that you will use at the transmission level.

3\. Once finished, click the "Confirm Purchases" button to purchase your dedicated IPs.
4\. The Billing page will then reflect your new purchase and your monthly invoice will be updated to reflect the charge for the dedicated IP(s). The dedicated IP(s) charge will be prorated by month.

****NOTE: Each Account is limited to a maximum of 4 dedicated IPs at any one time***                                                                          

## Managing Dedicated IP Pools

You can view and manage your dedicated IPs and their associated IP Pools in the UI by selecting Account **->** IP Pools

From here, you can create, delete, or edit IP Pools. You can also move dedicated IPs between pools. Read this article to understand more about <u>[managing your existing dedicated IP pools](https://support.sparkpost.com/customer/en/portal/articles/2460212-managing-dedicated-ips)</u>. 

## Using Your Dedicated IPs

In order to route messages through a specific IP Pool, you will need to include the appropriate "ip_pool" value at the transmission level.

SMTP header example:

| X-MSYS-API: { "options" : { "ip_pool" : "my_new_ip_pool" } } |

REST transmission example:

| {
  "options" : {
    "ip_pool" : "my_other_new_ip_pool"
  },
  "recipients" : [ ... ],
  "content" : { ... }
} |

If you have one or more IP pools, and you do **not** provide an "ip_pool" value for your transmission, then messages will be routed through the IP(s) in the "Default" IP Pool. If the "Default" IP pool has no sending IPs then the traffic will be sent through the SparkPost shared IP pools.

## Using Your Dedicated IPs with Subaccounts

To assign an IP Pool to a subaccount, click Account **->** Subaccounts. Edit the appropriate subaccount, select the IP Pool Id in the IP Pool Id picklist, and press Update Subaccount.

Note that you cannot have more than one IP Pool assigned to the same subaccount.  The IP pool assigned to the subaccount acts as the default IP pool for that subaccount.  All messages injected by the subaccount will then automatically use that IP Pool. This means that subaccount transmissions do not need to specify the ip_pool value.  

To bypass an assigned IP Pool, you can specify sp_shared at the transmission level. This will route traffic through the SparkPost shared IP Pool instead of the subaccount’s assigned IP Pool.

## Queued Messages

Messages queued for delivery have the sending IP attached to the message.   So the message will still deliver via the correct dedicated IP, even if that IP is unassigned from the account.   That logic is not specific to IP unassignment.  Same holds true if you move that IP to a different pool, or delete the pool entirely.  SparkPost behaves the same in all of those cases.  As long as the message is already queued, it will still go out on the original assigned IP/Pool. 

## Scheduled Transmissions

Scheduled transmissions have a slightly different behavior.  If at the scheduled time, SparkPost sees that the selected IP Pool either doesn't exist or is empty, it will attempt fallback to your account's default pool if it exists.  If not, it falls back to the shared pools.