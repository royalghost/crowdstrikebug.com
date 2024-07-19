---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---
![Windows Blue Screen](bluescreen.jpg "Windows Blue Screen")

# What is CrowdStrike bug

## Live Updates
[Reddit](https://old.reddit.com/r/crowdstrike/comments/1e6vmkf/bsod_error_in_latest_crowdstrike_update/)

[Hacker News](https://news.ycombinator.com/item?id=41002195)


## Company

CrowdStrike provides cloud workload protection and endpoint security, threat intelligence, and cyberattack response services.

## Summary

CrowdStrike software updates leading to crashes on Windows hosts related to the Falcon Sensor.

## Details

Symptoms include hosts experiencing a bugcheck\blue screen error related to the Falcon Sensor.

Windows hosts which have not been impacted do not require any action as the problematic channel file has been reverted.

Windows hosts which are brought online after 0527 UTC will also not be impacted

Hosts running Windows 7/2008 R2 are not impacted

This issue is not impacting Mac- or Linux-based hosts

Channel file "C-00000291*.sys" with timestamp of 0527 UTC or later is the reverted (good) version.

Channel file "C-00000291*.sys" with timestamp of 0409 UTC is the problematic version.
    Note: It is normal for multiple "C-00000291*.sys files to be present in the CrowdStrike directory - as long as one of the files in the folder has a timestamp of 0527 UTC or later, that will be the active content.


# How to fix Crowdstrike bug

## Workaround Steps for individual hosts:

    Reboot the host to give it an opportunity to download the reverted channel file. If the host crashes again, then:
        Boot Windows into Safe Mode or the Windows Recovery Environment
            NOTE: Putting the host on a wired network (as opposed to WiFi) and using Safe Mode with Networking can help remediation.
        Navigate to the %WINDIR%\System32\drivers\CrowdStrike directory
        Locate the file matching “C-00000291*.sys”, and delete it.
        Boot the host normally.

        Note: Bitlocker-encrypted hosts may require a recovery key. 

## Workaround Steps for public cloud or similar environment including virtual:
### Option 1:

    ​​​​​​​Detach the operating system disk volume from the impacted virtual server
    Create a snapshot or backup of the disk volume before proceeding further as a precaution against unintended changes
    Attach/mount the volume to to a new virtual server
    Navigate to the %WINDIR%\System32\drivers\CrowdStrike directory
    Locate the file matching “C-00000291*.sys”, and delete it.
    Detach the volume from the new virtual server
    Reattach the fixed volume to the impacted virtual server

### Option 2:

    ​​​​​​​Roll back to a snapshot before 0409 UTC.

## AWS-specific documentation:

[To attach an EBS volume to an instance](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-attaching-volume.html#:~:text=To%20attach%20an%20EBS%20volume,and%20choose%20Actions%2C%20Attach%20volume
)

[Detach an Amazon EBS volume from an instance](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-detaching-volume.html)

Note: Use a different OS version for the VirtualMachine used as the recovery VM to the Virtual Machine you are trying to recover.

## Azure environments:

[Please see this Microsoft article](https://azure.status.microsoft/en-gb/status)

## Google Cloud
[https://status.cloud.google.com/incidents/DK3LfKowzJPpZq4Q9YqP](https://status.cloud.google.com/incidents/DK3LfKowzJPpZq4Q9YqP)

## User Access to Recovery Key in the Workspace ONE Portal

When this setting is enabled, users can retrieve the BitLocker Recovery Key from the Workspace ONE portal without the need to contact the HelpDesk for assistance. To turn on the recovery key in the Workspace ONE portal, follow the next steps. Please see this [Omnissa article](https://techzone.omnissa.com/enabling-bitlocker-encryption-remote-windows-devices-workspace-one-operational-tutorial#user-access-to-recovery-key-in-the-workspace-one-portal) for more information.

## Bitlocker recovery-related KBs:

[BitLocker recovery in Microsoft Azure](https://www.crowdstrike.com/wp-content/uploads/2024/07/BitLocker-recovery-in-Microsoft-Azure.pdf)

[BitLocker recovery in Microsoft environments using SCCM](https://www.crowdstrike.com/wp-content/uploads/2024/07/CS-BitLocker-recovery-in-Microsoft-environments-using-SCCM.pdf)

[BitLocker recovery in Microsoft environments using Active Directory and GPOs](https://www.crowdstrike.com/wp-content/uploads/2024/07/CS-BitLocker-recovery-in-Active-Directory.pdf)

[BitLocker recovery in Microsoft environments using Ivanti Endpoint Manager](https://www.crowdstrike.com/wp-content/uploads/2024/07/CS-BitLocker-recovery-in-Microsoft-environments-using-Ivanti-Endpoint-Manager_.pdf)


# References
[https://en.wikipedia.org/wiki/CrowdStrike](https://en.wikipedia.org/wiki/CrowdStrike)

[https://www.crowdstrike.com/blog/statement-on-falcon-content-update-for-windows-hosts/](https://www.crowdstrike.com/blog/statement-on-falcon-content-update-for-windows-hosts/)
