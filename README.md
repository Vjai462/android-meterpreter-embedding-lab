# android-meterpreter-embedding-lab
Professional penetration testing lab demonstrating advanced Android 13 exploitation using manual Meterpreter payload embedding into legitimate APK
# Android Meterpreter Embedding Lab

A practical cybersecurity lab demonstrating APK trojanization techniques by embedding a Meterpreter payload into a legitimate Android application for educational purposes.

## Lab Overview

This project documents the complete process of:
- Decompiling a legitimate Android APK (Pedometer app)
- Injecting a Meterpreter reverse TCP payload
- Recompiling and signing the trojanized APK
- Deploying to a target device
- Establishing remote control via Metasploit

## Environment Details

**Attacker Machine:**
- **OS:** Kali Linux 2024.4
- **IP Address:** 172.27.33.114
- **Platform:** VirtualBox VM
- **Tools:** APKTool 2.9.3, Metasploit Framework, APKSigner, Java JDK 21

**Target Device:**
- **Device:** Samsung M32
- **OS:** Android 13
- **IP Address:** 172.27.33.171
- **Connection:** Mobile hotspot network

**Network:**
- **Topology:** Direct connection via mobile hotspot (Oppo)
- **VirtualBox:** Bridged Adapter + NAT Network

## Lab Structure

01-setup/ # Environment configuration and network setup
02-payload-creation/ # Meterpreter payload generation with msfvenom
03-apk-decompilation/ # Decompiling legitimate and payload APKs
04-payload-injection/ # Merging Metasploit code into original app
05-recompilation-signing/ # Rebuilding and signing the trojanized APK
06-deployment/ # Hosting and installing the malicious APK
07-exploitation/ # Meterpreter session and post-exploitation


## Key Learning Outcomes

- Understanding APK structure and Smali bytecode
- Mastering APKTool for reverse engineering
- Payload injection techniques in Android applications
- APK signing and certificate management
- Metasploit Framework for Android exploitation
- Network configuration for penetration testing labs

## Ethical Considerations

This lab was conducted in a controlled environment with:
- Personal devices owned by the researcher
- Isolated network setup
- No unauthorized access to third-party systems
- Educational purpose only

## Prerequisites

- Basic understanding of Android architecture
- Familiarity with Linux command line
- Knowledge of networking concepts
- Understanding of penetration testing ethics

## Author

**Cybersecurity Researcher & AI Enthusiast**
- Location: Champapet, Telangana, India
- Domain: Android Security, Penetration Testing
- Completed: December 2025

---

**⚠️ Disclaimer:** This project is for educational purposes only. Unauthorized access to devices you don't own is illegal. Always obtain proper authorization before security testing.

