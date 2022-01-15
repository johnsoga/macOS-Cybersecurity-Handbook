# macOS Cybersecurity Handbook

Currently, Apple is in the process of transitioning their (computer) devices from using Intel based hardware to custom ARM based Apple Silicon. Even before this process Apple had been integrating other custom hardware modules into their machines. Given the large amount of infromation this would require encompassing and due to my desire for this guide to remain as up-to-date as possible initially this guide will only reference Apple's latest hardware configurations. As the guide progresses in completion older platforms/hardware will be added as well. To learn what configurations are currently covered by this guide see the [supported hardware](#supported-hardware) section

## Supported Hardware

Hardware/Machines currently covered by this guide

* MacBook Pro (M1 Pro/M1 Max) 2021 and Newer
* MacBook Pro (M1) 2020 and Newer
* MacBook Air (M1) 2020 and Newer
* Mac Mini (M1) 2020 and Newer
* iMac (M1) 2020 and Newer

## Security Posture

TODO Outline
* Trust in procurement of device

## Installing macOS

By default Apple devices come with macOS already pre-installed on them. Depending on your [security posture](#security-posture) it maybe acceptable to use the machine as is with this default setup and simply go through the intial configuration. Otherwise, it may make more sense to overwrite this install with a brand new installation of the operating system. This section will cover these different scenarios

### Reinstalling macOS from a Recovery Partition

By default Apple includes a [Recovery Partition](https://support.apple.com/guide/mac-help/macos-recovery-a-mac-apple-silicon-mchl82829c17) which allows for several simple diagnostics tasks including [reinstalling](https://support.apple.com/en-us/HT204904) the OS. 

### Reinstalling macOS from a Bootable Installer

While reinstalling from a recovery partition will provide you with a fresh install of the OS. It does not reinstall the Recovery Partiion itself, so, to have a completely clean platform to reinstall macOS on you will need to wipe the entire disk first. To do this you will need to have the OS image installer on a separate media to reinstall from. Apple provide [instructions](https://support.apple.com/en-us/HT201372) on how to do this. Effecitvely, you will be create booting from that external device like was the "Recovery Partition" which will allow you to wipe and reformat the whole internal disk and then reinstall macOS and the "Recovery Partition" on it.