# CORP-RA01-TE123DA — SOC Incident Investigation

A cybersecurity portfolio project documenting an October 2026 investigation involving MySQL audit activity, Microsoft Defender for Endpoint telemetry, and an Azure Workbook for geolocating inbound Windows authentication sources.

## Contents

- [`reports/SOC-Incident-Response-Report.pdf`](reports/SOC-Incident-Response-Report.pdf) — incident response report and DFIR comparison, including evidence, IOC leads, timeline, ATT&CK assessment, and investigative limitations.
- [`workbooks/authentication-origins.json`](workbooks/authentication-origins.json) — Azure Monitor / Microsoft Sentinel Workbook JSON targeting `CORP-RA01-TE123DA` in `DeviceLogonEvents`.

- [Forensic Ransom Note Evidence](evidence/ransom-note/) — MySQL ransom note screenshots, extortion instructions, and cryptocurrency payment evidence.

## Import the Workbook

1. Open **Microsoft Sentinel → Workbooks** or **Azure Monitor → Workbooks**.
2. Create or edit a workbook and open **Advanced editor**.
3. Paste the contents of `workbooks/authentication-origins.json` and apply.
4. In each query item, select a Log Analytics workspace that actually contains the `DeviceLogonEvents` table. The bundled resource reference is environment-specific and may need replacing.
5. Select a time range covering **October 1, 2026** and run the queries.

### Requirements and caveats

- The workbook uses the `DeviceLogonEvents` table, the `geo_info_from_ip_address()` KQL function, and filters for `DeviceName =~ "CORP-RA01-TE123DA"`. It **does not** read MySQL authentication logs; those require separate ingestion and queries.
- The `DeviceLogonEvents` data must be accessible in the selected workspace. Microsoft Defender Advanced Hunting and Azure Log Analytics are not interchangeable query contexts.
- Geographic IP enrichment is approximate. Missing data, workspace permissions, or retention limits can produce empty maps.
- The PDF distinguishes observed events from hypotheses. Logged SQL commands alone do not establish that all commands succeeded or that data was exfiltrated.

## Responsible publication

This repository contains a report and investigation indicators. Before making the repository public, review the report for any organization-sensitive information, IP addresses, hostnames, account identifiers, or other details you do not want disclosed. Do not publish credentials, raw sensitive logs, or unredacted customer data.

## Project status

Portfolio investigation and workbook template. This repository does not claim a verified live deployment, successful ingestion, or confirmed attribution.
