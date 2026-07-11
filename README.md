# Network Traffic Investigation Lab

## Overview

This project documents an end-to-end network traffic investigation using tcpdump, Wireshark, Zeek, and Splunk.

Traffic was generated from a Windows virtual machine and captured on an Ubuntu virtual machine. The packet capture was examined in Wireshark, processed with Zeek, and ingested into Splunk for correlation across connection, HTTP, and file metadata.

## Lab Environment

| System | Role | IP Address |
|---|---|---|
| Windows VM | Traffic source and Splunk server | `192.168.1.4` |
| Ubuntu VM | Web server, packet capture, and Zeek analysis | `192.168.1.5` |

Both virtual machines were connected to the same VirtualBox NAT Network named `TCM`.

## Tools Used

- tcpdump
- Wireshark
- Zeek 8.0.9
- Splunk Enterprise
- Python HTTP server
- Windows PowerShell and curl

## Scenario 1: HTTP Traffic Investigation

### Objective

The objective was to generate controlled HTTP traffic, capture it in a PCAP file, analyze it at the packet level, extract structured network metadata, and correlate the resulting logs in Splunk.

### Traffic Generated

The Windows VM performed the following activity against a Python web server hosted on Ubuntu:

```powershell
ping 192.168.1.5

curl.exe http://192.168.1.5:8000/

curl.exe http://192.168.1.5:8000/index.html `
-o "$env:USERPROFILE\Downloads\project2-index.html"

curl.exe http://192.168.1.5:8000/secret-document.txt

