---
title: Common Issues
excerpt: Troubleshooting common API or ecommerce integration issues
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Unable to create order / unable to send a request to CoinGate API

| Reason                                                                                                                                 | Solution                                                                                                                                                                                                   |
| :------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API credentials used in the wrong environment                                                                                          | Create separate users and separate API credentials for Sandbox (sandbox.coingate.com) or Live (coingate.com) environments                                                                                  |
| Incorrect API credentials                                                                                                              | Please check if you have entered them correctly; make sure that there are no spaces before or after the text.                                                                                              |
| API requests are coming from a different IP address(es) than the IPs that were whitelisted when creating API credentials when creating | If IP whitelisting is desired, log in to your CoinGate account, visit API » Apps and clicking Edit next to your API credentials; make sure the whitelisted IPs match the IPs your requests are coming from |
| Your server cannot reach coingate.com                                                                                                  | Check if coingate.com is available and if your server can reach it (also see [Status Page](https://status.coingate.com))                                                                                   |

You can see your API Request logs by locating API » Requests in the menu of your CoinGate account.

## Order status is not updated / CoinGate does not send Payment Callback (Payment Notification)

| Reason                                                                                                                                   | Solution                                                                                                                                                                             |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Your server is on a private network, for example localhost                                                                               | Make sure that your application is publicly accessible                                                                                                                               |
| Your website is disabled or in maintenance mode                                                                                          | Make sure your website is accessible                                                                                                                                                 |
| Your server firewall, third-party security service (Cloudflare, Incapsula, etc.) or your application is blocking CoinGate IP address(es) | Verify that [CoinGate IP address(es)](https://developer.coingate.com/reference/ip-addresses) are allowed by your server firewall, third-party security services and your application |

You can check the specific reason why Payment Callback was not sent by logging in to your CoinGate account and locating API » Payment Callbacks in the menu.