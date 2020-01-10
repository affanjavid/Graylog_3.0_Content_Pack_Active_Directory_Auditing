# Active Directory Auditing Content Pack
It's  reighnman 's & aydnyldrm 's Active Directory Auditing Content Pack for Graylog 2.x and updated and tested for Graylog 3 
You can find original content pack at https://marketplace.graylog.org/addons/750b88ea-67f7-47b1-9a6c-cbbc828d9e25
Tested with nxLog/Windows Server 2012, nxLog/Windows Server 2012R2, nxLog/Windows Server 2016 Domain Controllers/Graylog 3.1.3

This content pack provides several useful dashboards for auditing Active Directory events:
* DNS Object Summary - DNS Creations, Deletions
* Group Object Summary - Group Creations, Modifications, Deletions, Membership Changes
* User Object Summary - Account Creations, Deletions, Modifications, Lockouts, Unlocks
* Computer Object Summary - (in progress)
* Logon Summary - Failed Authentication Attempts, Interactive Logins

## Includes

* Input (GELF udp 5414)
* Failed Logon Stream (unconfigured)
* Dashboards 

## Requirements

* NXLog collecting windows logs, other log collectors will work but may require modifying the searches to match the different fields outputted by other collectors
* Domain Controller secuirty policy with the following enabled:
** Audit Account Logon Events
** Audit Account Managmenet
** Audit Logon Events
** Audit Object Access
** Audit Policy Change
** Audit System Events
* Leading Wildcard Searches enabled in graylog.conf:  allow_leading_wildcard_searches = true

## NXLog Example
```
define ROOT C:\Program Files (x86)\nxlog

Moduledir %ROOT%\modules
CacheDir %ROOT%\data
Pidfile %ROOT%\data\nxlog.pid
SpoolDir %ROOT%\data
LogFile %ROOT%\data\nxlog.log

<Extension gelf>
    Module xm_gelf
</Extension>
<Input in>
    # For windows vista/2008 and above use:
    Module      im_msvistalog

    # For windows 2003 and earlier use the following:
    #   Module      im_mseventlog
</Input>

<Output out> 
    Module      om_udp
    Host        graylog.server.com
    Port        5414
    OutputType  GELF
</Output>

<Route 1>
    Path        in => out
</Route>
```

## Screenshots

![Dashboard](http://www.ohjeah.net/wp-content/uploads/2015/09/ad_audit.png)
