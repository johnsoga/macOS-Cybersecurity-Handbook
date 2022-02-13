# macOS Cybersecurity Handbook

Currently, Apple is in the process of transitioning their (computers) physical architecture away from Intel (x86) hardware to custom Apple Silicon (ARM) hardware. Even before this broad platform redesign Apple had been designinng and integrating other custom hardware into their machines. To cover all of that hardware there would be a large amount of infromation to cover in this guide. My goal is for this guide to remain as up-to-date, and brief, as possible. To reach this goal this guide will initially only reference Apple's latest hardware configurations. As the guide progresses in completion older platforms/hardware will be added as well. To learn what configurations are currently covered by this guide see the [supported hardware](#supported-hardware) section.

## Supported Hardware

Hardware/Machines currently covered by this guide

* MacBook Pro (M1 Pro/M1 Max) 2021 and Newer
* MacBook Pro (M1) 2020 and Newer
* MacBook Air (M1) 2020 and Newer
* Mac Mini (M1) 2020 and Newer
* iMac (M1) 2020 and Newer

## Security Posture

TODO
- [ ] Trust in procurement of device

### Frameworks

TODO
- [ ] [macOS Security Compliance Project](https://support.apple.com/guide/sccc/macos-security-compliance-project-sccc22685bb2/web): [Github](https://github.com/usnistgov/macos_security)/[NIST](https://csrc.nist.gov/Projects/macos-security)

## Installing macOS

By default, Apple devices come with macOS already pre-installed. Depending on your [security posture](#security-posture) it may be acceptable to use your device as is with this default install and going through the intial configuration setup. If your security posture is higher it may otherwise make more sense to overwrite this install with a new installation of the operating system. This section will cover these different scenarios

### Reinstalling macOS from a Recovery Partition

Apple includes a "[Recovery Partition](https://support.apple.com/guide/mac-help/macos-recovery-a-mac-apple-silicon-mchl82829c17)" which allows for several simple diagnostics tasks including [reinstalling](https://support.apple.com/en-us/HT204904) the operating system. 

### Reinstalling macOS from a Bootable Installer

While reinstalling from a recovery partition will provide you with a fresh install of the OS. It does not reinstall the "Recovery Partiion" itself, so, to have a completely clean platform to reinstall macOS on you will need to wipe the entire disk first. To do this you will need to have the OS image installer on a separate media to reinstall from. Apple provides [documentation](https://support.apple.com/en-us/HT201372) on how to do this. Effectively, you will be booting from that external device as if it was the "Recovery Partition" which will allow you to wipe internal disk of the machine and then reinstall macOS and the "Recovery Partition" on to it.

#### Verify the Installer

It is always best practice to validate any software package, if possible, before you install it to ensure the validity of the software. Usually, this is done by [hashing](https://en.wikipedia.org/wiki/File_verification) the bundle and comparing the result with the hash value provided by the software maintainer. Apple, however, chooses to use ["Code Signing"](https://support.apple.com/guide/security/app-code-signing-process-sec3ad8e6e53/web)[^note] instead to achieve a similar, albeit more complicated, result. It maybe worth noting that "Code Signing" is actually required of all software distributed via the App Store, this includes Apple's own OS Installer which is distributed in this manner. While Apple seems to have not properly signed their OS Installer app we can use 2 other pieces of information to provide a certain level of trust about the Installer app:

1. [Gatekeeper](https://support.apple.com/guide/security/gatekeeper-and-runtime-protection-sec5599b66df/web), by default, only allows software signed by valid developers to be run
2. We can verify the certificate chain used to sign the Installer app; see below

```console
$ pkgutil --verbose --check-signature /Applications/Install\ macOS\ Monterey.app
Package "Install macOS Monterey":
   Status: signed by a certificate trusted by macOS
   Certificate Chain:
    1. Software Signing
       Expires: 2026-10-24 17:39:41 +0000
       SHA256 Fingerprint:
           D8 4D B9 6A F8 C2 E6 0A C4 C8 51 A2 1E C4 60 F6 F8 4E 02 35 BE B1
           7D 24 A7 87 12 B9 B0 21 ED 57
       ------------------------------------------------------------------------
    2. Apple Code Signing Certification Authority
       Expires: 2026-10-24 17:39:41 +0000
       SHA256 Fingerprint:
           5B DA B1 28 8F C1 68 92 FE F5 0C 65 8D B5 4F 1E 2E 19 CF 8F 71 CC
           55 F7 7D E2 B9 5E 05 1E 25 62
       ------------------------------------------------------------------------
    3. Apple Root CA
       Expires: 2035-02-09 21:40:36 +0000
       SHA256 Fingerprint:
           B0 B1 73 0E CB C7 FF 45 05 14 2C 49 F1 29 5E 6E DA 6B CA ED 7E 2C
           68 C5 BE 91 B5 A1 10 01 F0 24
```
 
While it would be better if Apple would properly sign this Installer app these 2 pieces of information provide atleast a cautionary level of trust. If not, well, you did choose to support this company :cry:

## Setup

TODO
- [ ] Setup Configuration
- [ ] Filevault

## Post-Setup
### Firewalls
#### Inbound Firewalls
A normal firewall(L3/L4) is primarily used to control Ingress (Inbound)/Egress (Outbound) data flows into a network/device usually by looking at the port and protocol of the connection being attempted. An application firewall(L7) is concerned with "who" is trying to make a connection regardless, typically, of the port/protocol being used. As an example with a normal firewall I might want to block all inbound TCP connections on port 80 where as with an application firewall I would say perhaps block all inbound connections for Apache, or perhaps that might be more refined to block all HTTP connections to Apache.

As it applies to macOS Apple includes an application firewall which by default is turned off. You should turn this firewall on by navigating to System Preferences -> Security & Privacy -> Firewall. This firewall looks at inbound connections and there are further configurations that can be enabled by going to "Firewall Options", good defaults to enable would be:

* Automatically allow built-in software to receive incoming connections
    * i.e. iCloud, Find My Mac, etc.
* Automatically allow downloaded and signed software to receive incoming connections
    * i.e anything downloaded from the App Store or in general from a third party that is validly signed by Apple
* Enable stealth mode

Apple offers a bit more detail about these options [here](https://support.apple.com/en-us/HT201642)

TODO
- [ ] Firewall: [ref1](https://support.apple.com/en-us/HT201642)
- [ ] Third Party Firewalls: little snitch
- [ ] Remote Login (SSH)
- [ ] Remote Management
- [ ] AntiVirus/AntiMaleware
- [ ] User Accounts
- [ ] Passwords
- [ ] Locking Machine
- [ ] Guest Account
- [ ] OS/Security Updates
- [ ] Automatic Login

[^note]: see [Code Signing Guide](https://developer.apple.com/library/archive/documentation/Security/Conceptual/CodeSigningGuide/Introduction/Introduction.html) and [Technical Note TN2206](https://developer.apple.com/library/archive/technotes/tn2206)