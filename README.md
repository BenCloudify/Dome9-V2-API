#DOME9 API#

The Dome9 API enables developers to access Dome9 functionality by using an API key.
A description of the  resourses currently used in the beta version is as follows:

##URL 

The URL used in order to make requests is https://api.dome9.com/

##Authorization 

The authorization is made with an API key, which is generated by an [automatic tool](apiGenerator/README.md), by inserting the API key as a Basic Authentication, while the "id" is the username and the "API Key Secret" is the password.

##Supported Features 
 
1. [AWS Security Groups](#aws-security-groups)

2. [AWS Accounts](#aws-accounts)

3. [IP Lists](#ip-lists)

##<a name="aws-security-groups">AWS Security Groups</a>
1. [GET](#aws-security-groups-get)
2. [Create Security Groups](#aws-security-groups-create)
3. [Create Service](#aws-security-groups-create-service)
4. [Overwrite Security Group](#aws-security-groups-overwrite-security-group)
5. [Overwrite service](#aws-security-groups-overwrite-service)
6. [Delete service](#aws-security-groups-delete-service)
7. [Delete Security Groups](#aws-security-groups-delete-security-groups)

<h3><a name="aws-security-groups-get">GET</a></h3> 

The GET request return the entire cloud security groups, which are attached to Dome9.

URL: https://api.dome9.com/CloudSecurityGroup/{id} <br \>
METHOD: GET <br \> <br \>
ID: if the request is made without the security group id, then the entire security groups attached to Dome9 will be returned.

####Response:

```json
 {
   "securityGroupId": "integer",
   "externalId": "string",
   "isProtected": "boolean",
   "securityGroupName": "string",
   "vpcId": "string",
   "regionId": "string",
   "cloudAccountId": "string",
   "cloudAccountName": "string",
   "services": {},
   "tags": {}
 }
```

* securityGroupId (integer): The Security Group ID in dome9.
* externalId (string): The Security Group ID in AWS.
* isProtected (boolean, optional): will appear as "true" if it is in Full Protection or will appear as "false" if it is in Read Only mode.
* securityGroupName (string, optional): The name of the Security Group.
* description (string, optional): The description of the Security Group.
* vpcId (string, optional): The VPC of the Security Group.
* regionId (string, optional): Can be one of the following regions - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
* cloudAccountId (string, optional): Dome9 Cloud Account ID.
* services (object, optional) - The inbound and outbound services.
* tags (object, optional) - The security groups tags.

<h3><a name="aws-security-groups-create">Create Security Groups</a></h3>
Create a new Security Group on AWS.

URL: https://api.dome9.com/CloudSecurityGroup <br \>
METHOD: POST <br \>
BODY:
```json
{
  "isProtected": "boolean",
  "securityGroupName": "string",
  "description": "string",
  "vpcId": "string",
  "regionId": "string",
  "cloudAccountId": "string",
  "cloudAccountName": "string",
  "tags": {}
}
```

####Request Parameters

* isProtected (boolean, optional): if set as "true" it will be in Full Protection or if set as "false" it will be in Read Only mode.
* securityGroupName (string, optional): The name of the Security Group.
* description (string, optional): The description of the Security Group.
* vpcId (string, optional): The VPC of the Security Group.
* regionId (string, optional): Can be one of the next regions - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
* cloudAccountId (string, optional): Dome9 Cloud Account ID.
* services (object, optional)
* tags (object, optional)

####Response 


* securityGroupId (integer): The Security Group ID in dome9.
* externalId (string): The Security Group ID in AWS.
* isProtected (boolean, optional): will appear as "true" if it is in Full Protection or will appear as "false" if it is in Read Only mode.
* securityGroupName (string, optional): The name of the Security Group.
* description (string, optional): The description of the Security Group.
* vpcId (string, optional): The VPC of the Security Group.
* regionId (string, optional): Can be one of the following regions - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
* cloudAccountId (string, optional): Dome9 Cloud Account ID.
* services (object, optional) - The inbound and outbound services.
* tags (object, optional) - The security groups tags.

<h3><a name="aws-security-groups-create-service">Create Service</a></h3>

Create a new service for Security Group on AWS.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid}/services <br \>
METHOD: POST <br \>

note: The groupid in the URL can be either the internal id or the external id. <br \>

BODY:
```json
{
  "name": "string",
  "description": "string",
  "protocolType": "string",
  "port": "string",
  "openForAll": "boolean",
  "scope": [
    {
      "type": "string",
      "data": "object"
    }
  ],
  "inbound": "boolean",
  "icmpType": "string"
}
```

####Request Parameters 

* name (string): The service name.
* description (string, optional): The service description.
* protocolType (string): Can be one of the following protocols - 'HOPOPT', 'ICMP', 'IGMP', 'GGP', 'IPV4', 'ST', 'TCP', 'CBT', 'EGP', 'IGP', 'BBN_RCC_MON', 'NVP2', 'PUP', 'ARGUS', 'EMCON', 'XNET', 'CHAOS', 'UDP', 'MUX', 'DCN_MEAS', 'HMP', 'PRM', 'XNS_IDP', 'TRUNK1', 'TRUNK2', 'LEAF1', 'LEAF2', 'RDP', 'IRTP', 'ISO_TP4', 'NETBLT', 'MFE_NSP', 'MERIT_INP', 'DCCP', 'ThreePC', 'IDPR', 'XTP', 'DDP', 'IDPR_CMTP', 'TPplusplus', 'IL', 'IPV6', 'SDRP', 'IPV6_ROUTE', 'IPV6_FRAG', 'IDRP', 'RSVP', 'GRE', 'DSR', 'BNA', 'ESP', 'AH', 'I_NLSP', 'SWIPE', 'NARP', 'MOBILE', 'TLSP', 'SKIP', 'IPV6_ICMP', 'IPV6_NONXT', 'IPV6_OPTS', 'CFTP', 'SAT_EXPAK', 'KRYPTOLAN', 'RVD', 'IPPC', 'SAT_MON', 'VISA', 'IPCV', 'CPNX', 'CPHB', 'WSN', 'PVP', 'BR_SAT_MON', 'SUN_ND', 'WB_MON', 'WB_EXPAK', 'ISO_IP', 'VMTP', 'SECURE_VMTP', 'VINES', 'TTP', 'NSFNET_IGP', 'DGP', 'TCF', 'EIGRP', 'OSPFIGP', 'SPRITE_RPC', 'LARP', 'MTP', 'AX25', 'IPIP', 'MICP', 'SCC_SP', 'ETHERIP', 'ENCAP', 'GMTP', 'IFMP', 'PNNI', 'PIM', 'ARIS', 'SCPS', 'QNX', 'AN', 'IPCOMP', 'SNP', 'COMPAQ_PEER', 'IPX_IN_IP', 'VRRP', 'PGM', 'L2TP', 'DDX', 'IATP', 'STP', 'SRP', 'UTI', 'SMP', 'SM', 'PTP', 'ISIS', 'FIRE', 'CRTP', 'CRUDP', 'SSCOPMCE', 'IPLT', 'SPS', 'PIPE', 'SCTP', 'FC', 'RSVP_E2E_IGNORE', 'MOBILITY_HEADER', 'UDPLITE', 'MPLS_IN_IP', 'MANET', 'HIP', 'SHIM6', 'WESP', 'ROHC', 'ALL'.
* port (string, optional): The port (can be a port range).
* openForAll (boolean): if it is "true" it will be open for the entrie internet, and if it is "flase" it will be open for the internet according to the scope parameter. 
* scope (Array[ScopeElementViewModel], optional): The service scope. If the service is "closed" then the scope isn't necessary.
  * type (string): Can be one of the following - ['CIDR', 'DNS', 'IPList', 'MagicIP', 'AWS'],
  * data (object): For CIDR - "cidr":'IP', For IP-List - "id":"IP-LIST ID","name":"IP-LIST NAME"}
* inbound (boolean): If it is "true" it will be added to the "inbound rules" and if it is "false" it will be added to the "outbound rules".
* icmpType (string, optional): In case of ICMP - 'EchoReply', 'DestinationUnreachable', 'SourceQuench', 'Redirect', 'AlternateHostAddress', 'Echo', 'RouterAdvertisement', 'RouterSelection', 'TimeExceeded', 'ParameterProblem', 'Timestamp', 'TimestampReply', 'InformationRequest', 'InformationReply', 'AddressMaskRequest', 'AddressMaskReply', 'Traceroute', 'DatagramConversionError', 'MobileHostRedirect', 'IPv6WhereAreYou', 'IPv6IAmHere', 'MobileRegistrationRequest', 'MobileRegistrationReply', 'DomainNameRequest', 'DomainNameReply', 'SKIP', 'Photuris', 'All'

####Response

It is similar to the request parameters.
<h3><a name="aws-security-groups-overwrite-security-group">Overwrite Security Group</a></h3> 
Overwrite an existing Security Group, change protection mode, overwrite tags and services.

URL: https://api.dome9.com/CloudSecurityGroup/{groupid} <br \>
METHOD: PUT <br \>
groupid: the security group id, can be both of AWS and Dome9. <br \>
BODY:
```json
{
  "isProtected": "boolean",
  "services": {
    "inbound": [{
        "name": "string",
        "description": "string",
        "protocolType": "string",
        "port": "string",
        "openForAll": "boolean",
        "scope": [
          {
            "type": "string",
            "data": {
              "cidr": "string",
              "note": "string"
            }
          }
        ]
      }],
    "outbound": [{
        "name": "string",
        "description": "string",
        "protocolType": "string",
        "port": "string",
        "openForAll": "boolean",
        "scope": [
          {
            "type": "string",
            "data": {
              "cidr": "string",
              "note": "string"
            }
          }
        ]
      }]
  },
  "tags": {}
}
```
####Request Parameters

* name (string): The service name.
* description (string, optional): The service description.
* protocolType (string): Can be one of the following protocols - 'HOPOPT', 'ICMP', 'IGMP', 'GGP', 'IPV4', 'ST', 'TCP', 'CBT', 'EGP', 'IGP', 'BBN_RCC_MON', 'NVP2', 'PUP', 'ARGUS', 'EMCON', 'XNET', 'CHAOS', 'UDP', 'MUX', 'DCN_MEAS', 'HMP', 'PRM', 'XNS_IDP', 'TRUNK1', 'TRUNK2', 'LEAF1', 'LEAF2', 'RDP', 'IRTP', 'ISO_TP4', 'NETBLT', 'MFE_NSP', 'MERIT_INP', 'DCCP', 'ThreePC', 'IDPR', 'XTP', 'DDP', 'IDPR_CMTP', 'TPplusplus', 'IL', 'IPV6', 'SDRP', 'IPV6_ROUTE', 'IPV6_FRAG', 'IDRP', 'RSVP', 'GRE', 'DSR', 'BNA', 'ESP', 'AH', 'I_NLSP', 'SWIPE', 'NARP', 'MOBILE', 'TLSP', 'SKIP', 'IPV6_ICMP', 'IPV6_NONXT', 'IPV6_OPTS', 'CFTP', 'SAT_EXPAK', 'KRYPTOLAN', 'RVD', 'IPPC', 'SAT_MON', 'VISA', 'IPCV', 'CPNX', 'CPHB', 'WSN', 'PVP', 'BR_SAT_MON', 'SUN_ND', 'WB_MON', 'WB_EXPAK', 'ISO_IP', 'VMTP', 'SECURE_VMTP', 'VINES', 'TTP', 'NSFNET_IGP', 'DGP', 'TCF', 'EIGRP', 'OSPFIGP', 'SPRITE_RPC', 'LARP', 'MTP', 'AX25', 'IPIP', 'MICP', 'SCC_SP', 'ETHERIP', 'ENCAP', 'GMTP', 'IFMP', 'PNNI', 'PIM', 'ARIS', 'SCPS', 'QNX', 'AN', 'IPCOMP', 'SNP', 'COMPAQ_PEER', 'IPX_IN_IP', 'VRRP', 'PGM', 'L2TP', 'DDX', 'IATP', 'STP', 'SRP', 'UTI', 'SMP', 'SM', 'PTP', 'ISIS', 'FIRE', 'CRTP', 'CRUDP', 'SSCOPMCE', 'IPLT', 'SPS', 'PIPE', 'SCTP', 'FC', 'RSVP_E2E_IGNORE', 'MOBILITY_HEADER', 'UDPLITE', 'MPLS_IN_IP', 'MANET', 'HIP', 'SHIM6', 'WESP', 'ROHC', 'ALL'.
* port (string, optional): The port (can be port range).
* openForAll (boolean): if set as "true" it will be open for the entire internet, and if set as "false" it will be open for the internet according to scope parameter.
* scope (Array[ScopeElementViewModel], optional): The service scope. If the service is "closed" then the scope isn't necessary.
  * type (string): can be one of the following - ['CIDR', 'DNS', 'IPList', 'MagicIP', 'AWS'],
  * data (object): for CIDR - "cidr":'IP', For IP-List - "id":"IP-LIST ID","name":"IP-LIST NAME"}
* inbound (boolean): If set as "true" then the rule will be added to the inbound, and if set as "false" then the rule will be added to the outbound.
* icmpType (string, optional): in case of ICMP - 'EchoReply', 'DestinationUnreachable', 'SourceQuench', 'Redirect', 'AlternateHostAddress', 'Echo', 'RouterAdvertisement', 'RouterSelection', 'TimeExceeded', 'ParameterProblem', 'Timestamp', 'TimestampReply', 'InformationRequest', 'InformationReply', 'AddressMaskRequest', 'AddressMaskReply', 'Traceroute', 'DatagramConversionError', 'MobileHostRedirect', 'IPv6WhereAreYou', 'IPv6IAmHere', 'MobileRegistrationRequest', 'MobileRegistrationReply', 'DomainNameRequest', 'DomainNameReply', 'SKIP', 'Photuris', 'All'
* tags (object): the format is "key":"value".

####Response

It is similar to the request parameters.

<h3><a name="aws-security-groups-overwrite-service">Overwrite Service</a></h3>

Update an existing service.
note: the service will be fully overwritten.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid}/services <br \>
METHOD: PUT <br \>

note: The groupid in the URL can be either the internal id or the external id. <br \>

BODY:
```json
{
  "name": "string",
  "description": "string",
  "protocolType": "string",
  "port": "string",
  "openForAll": "boolean",
  "scope": [
    {
      "type": "string",
      "data": "object"
    }
  ],
  "inbound": "boolean",
  "icmpType": "string"
}
```

####Request Parameters

* name (string): The service name.
* description (string, optional): The service description.
* protocolType (string): Can be one of the following protocols - 'HOPOPT', 'ICMP', 'IGMP', 'GGP', 'IPV4', 'ST', 'TCP', 'CBT', 'EGP', 'IGP', 'BBN_RCC_MON', 'NVP2', 'PUP', 'ARGUS', 'EMCON', 'XNET', 'CHAOS', 'UDP', 'MUX', 'DCN_MEAS', 'HMP', 'PRM', 'XNS_IDP', 'TRUNK1', 'TRUNK2', 'LEAF1', 'LEAF2', 'RDP', 'IRTP', 'ISO_TP4', 'NETBLT', 'MFE_NSP', 'MERIT_INP', 'DCCP', 'ThreePC', 'IDPR', 'XTP', 'DDP', 'IDPR_CMTP', 'TPplusplus', 'IL', 'IPV6', 'SDRP', 'IPV6_ROUTE', 'IPV6_FRAG', 'IDRP', 'RSVP', 'GRE', 'DSR', 'BNA', 'ESP', 'AH', 'I_NLSP', 'SWIPE', 'NARP', 'MOBILE', 'TLSP', 'SKIP', 'IPV6_ICMP', 'IPV6_NONXT', 'IPV6_OPTS', 'CFTP', 'SAT_EXPAK', 'KRYPTOLAN', 'RVD', 'IPPC', 'SAT_MON', 'VISA', 'IPCV', 'CPNX', 'CPHB', 'WSN', 'PVP', 'BR_SAT_MON', 'SUN_ND', 'WB_MON', 'WB_EXPAK', 'ISO_IP', 'VMTP', 'SECURE_VMTP', 'VINES', 'TTP', 'NSFNET_IGP', 'DGP', 'TCF', 'EIGRP', 'OSPFIGP', 'SPRITE_RPC', 'LARP', 'MTP', 'AX25', 'IPIP', 'MICP', 'SCC_SP', 'ETHERIP', 'ENCAP', 'GMTP', 'IFMP', 'PNNI', 'PIM', 'ARIS', 'SCPS', 'QNX', 'AN', 'IPCOMP', 'SNP', 'COMPAQ_PEER', 'IPX_IN_IP', 'VRRP', 'PGM', 'L2TP', 'DDX', 'IATP', 'STP', 'SRP', 'UTI', 'SMP', 'SM', 'PTP', 'ISIS', 'FIRE', 'CRTP', 'CRUDP', 'SSCOPMCE', 'IPLT', 'SPS', 'PIPE', 'SCTP', 'FC', 'RSVP_E2E_IGNORE', 'MOBILITY_HEADER', 'UDPLITE', 'MPLS_IN_IP', 'MANET', 'HIP', 'SHIM6', 'WESP', 'ROHC', 'ALL'.
* port (string, optional): The port (can be port range).
* openForAll (boolean): if set as "true" it will be open for the entire internet, and if set as "false" it will be open for the internet according to scope parameter.
* scope (Array[ScopeElementViewModel], optional): The service scope. If the service is "closed" then the scope isn't necessary.
  * type (string): can be one of the following - ['CIDR', 'DNS', 'IPList', 'MagicIP', 'AWS'],
  * data (object): for CIDR - "cidr":'IP', For IP-List - "id":"IP-LIST ID","name":"IP-LIST NAME"}
* inbound (boolean): If set as "true" then the rule will be added to the inbound, and if set as "false" then the rule will be added to the outbound.
* icmpType (string, optional): in case of ICMP - 'EchoReply', 'DestinationUnreachable', 'SourceQuench', 'Redirect', 'AlternateHostAddress', 'Echo', 'RouterAdvertisement', 'RouterSelection', 'TimeExceeded', 'ParameterProblem', 'Timestamp', 'TimestampReply', 'InformationRequest', 'InformationReply', 'AddressMaskRequest', 'AddressMaskReply', 'Traceroute', 'DatagramConversionError', 'MobileHostRedirect', 'IPv6WhereAreYou', 'IPv6IAmHere', 'MobileRegistrationRequest', 'MobileRegistrationReply', 'DomainNameRequest', 'DomainNameReply', 'SKIP', 'Photuris', 'All'

####Response

It is similar to the request parameters.

<h3><a name="aws-security-groups-delete-service">Delete Service</a></h3>

Deletion an existing service.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid}/services/{serviceid}?inbound={boolean} <br \>
METHOD: DELETE <br \>

* serviceid: composed of the port and protocol type with the following structure "{port}-{protocol type}",for example in ssh case it will be "6-22".
* groupid: The groupid in the URL can be either the internal id or the external id.
* inbound: if set as "true" it will delete in the inbound and if set as "false" it will delete in the oubound.

####Response

When successful the response is null.

<h3><a name="aws-security-groups-delete-security-groups">Delete Security Groups</a></h3>

Delete an existing security group.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid} <br \>
METHOD: DELETE <br \>

* groupid: The groupid in the URL can be either the internal id or the external id. <br \>

####Response

When successful the response is null.

##<a name="aws-accounts">AWS Accounts</a>

###Add AWS Account.

Adding a new AWS account to your Dome9 account.

URL: https://api.dome9.com/CloudAccounts <br \>
METHOD: POST <br \>
BODY:
```json
{
  "name": "string",
  "credentials": {
    "arn": "string" /*required*/, 
    "secret": "string" /*required*/,
    "type": "RoleBased" /*required*/,
    "isReadOnly": "boolean"
  },
  "fullProtection": true
}
```

####Request Parameters

* name (string, optional): the account name on Dome9.
* credentials (object, required): AWS account credentials.
  * arn (string, required): the predefine AWS role for Dome9.
  * secret (string, required): the role External ID.
  * type (string, required): 'RoleBased'.
  * isReadOnly (boolean, optional): the attached policy type.
* fullProtection (boolean, optional): if set as "true" it will import the security groups in full protection, and if set as "false" it will appear in "read only" mode.

###Update AWS Account

Updating an existing attached AWS account.

URL: https://api.dome9.com/CloudAccounts/{id} <br \>
METHOD: PATCH <br \>
id: The Dome9 cloud account ID <br \>
BODY:
```json
{
  "name": "string",
  "credentials": {
    "arn": "string" , 
    "secret": "string" ,
    "type": "RoleBased" ,
    "isReadOnly": "boolean"
  },
  "fullProtection": "boolean",
  "netSec": {
      "regions": [
        {
          "region": "string",
          "hidden": "boolean",
          "newGroupBehavior": "boolean"
        }
      ]
    }
}
```

####Request Parameters

* name (string, optional): the account name on Dome9.
* credentials (object, required): AWS account credentials.
  * arn (string, required): the predefine AWS role for Dome9.
  * secret (string, required): the role External ID.
  * type (string, required): 'RoleBased'.
  * isReadOnly (boolean, optional): the attached policy type.
* fullProtection (boolean, optional): if set as "true" it will import the security groups in full protection, and if set as "false" it will appear in "read only" mode.
* regions: the region data. It is only possible to insert one region in each request.
  * region (string, optional): can be one of the following options - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
  * hidden (boolean, optional): if set as "true" then the security groups in the region will be displayed, and if set as "false" then the security groups in the region will be hidden. 
  * newGroupBehavior (string, optional): can be one of the following options - 'ReadOnly', 'FullManage', 'Reset'.

###Delete AWS Account -

Deletion of an existing AWS Account.

URL: https://api.dome9.com/CloudAccounts/{cloudAccountId} <br \>
METHOD: DELETE <br \>

cloudAccountId: The Dome9 cloudAccountId. 

##<a name="ip-lists">IP Lists </a>

###GET

The get request "pulls" all IP Lists, which are attached to the Dome9 account.
ID: If the request is made without the IP List id then all IP Lists will return.

URL: https://api.dome9.com/IpList/{id} <br \>
METHOD: GET <br \>

####Response
```json
[
  {
    "id": 0,
    "name": "string",
    "description": "string",
    "items": [
      {
        "ip": "string",
        "comment": "string"
      }
    ]
  }
]
```

* id (integer): the IP List Id.
* name (string): the IP List name.
* description (string): the IP List description.
* items (Array[IPDescriptor]): an array with the Ips.
  * ip (string): IP address.
  * comment (string): a comment on the ip if exist.

###Create IP List
Creating a new IP List.

URL: https://api.dome9.com/IpList <br \>
METHOD: POST <br \>
BODY:
```json
{
  "name": "string", /* required */
  "description": "string",
  "items": [
    {
      "ip": "string", /* required */
      "comment": "string"
    }
  ]
}
```

####Request Parameters 

* name (string): the IP List name.
* description (string): the IP List description.
* items (Array[IPDescriptor]): an array of IPs.
  * ip (string): IP address.
  * comment (string): a comment on the IP.


###Update IP List

Updating an existing IP List.
The Update is relevant for the data and the description.
It will overwrite the existing IP List.

URL: https://api.dome9.com/IpList/{id} <br \>
METHOD: PUT <br \>

BODY:
```json
{
  "name": "string",
  "description": "string",
  "items": [
    {
      "ip": "string",
      "comment": "string"
    }
  ]
}
```

####Request Parameters
* id (in the URL): the IP List ID.
* name (string): the IP List name.
* description (string): the IP List description.
* items (Array[IPDescriptor]): an array of IPs.
  * ip (string): IP address.
  * comment (string): a comment on the IP.
 
###Delete IP List

Deletion of an existing IP List.

URL: https://api.dome9.com/IpList/{id} <br \>
METHOD: DELETE <br \>

* id: The IP List Id.
  
