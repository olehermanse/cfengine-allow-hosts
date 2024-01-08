This module uses `cfbs` module input to let you decide which hosts (specified by IP addresses and subnets) are allowed to connect to your hub, authenticate, fetch policy, etc.

Note that in CFEngine, these things can be configured individually:

* The `default:def.acl` variable is used to determine which hosts have access to copy policy files from the policy server.
  * **Default:** `$(sys.policy_hub)/16`.
  * **Recommendation:** Edit this variable (using this module) to only allow the IP addresses and subnets which you expect.
* The `default:def.allowconnects` variable controls which hosts are allowed to connect to the policy server (and after this attempt to authenicate using their key).
  * **Default:** If not specified, this variable defaults to the same as the variable above (`default:def.acl`).
  * **Recommendation:** Similar to `default:def.acl` - use this variable to only allow connections from IPs / subnets you expect.
* The `default:def.trustkeysfrom` allows hosts to perform automatic bootstrap, having their key autoatically become trusted by the hub.
  * **Default:** If not specified, this variable defaults to the same as the 2 variable above.
  * **Recommendation:** Set this variable to an empty list to stop trusting new keys automatially.
    [See our documentation for details about how to securely bootstrap hosts over potentially unsafe networks.](https://docs.cfengine.com/docs/master/getting-started-installation-secure-bootstrap.html)

This module edits the value of the first variable, `default:def.acl`, meaning the 2 others, if left untouched, will default to the same.

**Note:** Although using hostnames is supported, it's generally recommended to use IP addresses and subnets, rather than hostnames.
