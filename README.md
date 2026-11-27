![JS Miner Banner](assets/header.jpg)

# Burp JS Miner

**JS Miner** is a Burp Suite extension designed to automate initial reconnaissance on static web resources—primarily **JavaScript (`.js`)** and **JSON (`.json`)** files—to uncover sensitive data, hidden attack surfaces, and misconfigurations.

> **Note:** Like any static analysis tool, JS Miner may produce false positives. It is intended to assist and accelerate manual security assessments, not replace manual review.

---

## Overview

Modern web applications ship substantial logic, configuration, and metadata to the client side inside JavaScript bundles and JSON files. During a security assessment, manually inspecting every static asset is time-consuming. JS Miner integrates directly into Burp Suite's passive and active scanning workflows to flag high-value findings automatically.

---

## Features

### 1. Secrets & Credentials Detection (Passive)
- Scans static files for hardcoded API keys, tokens, and credentials.
- Uses **Shannon entropy** analysis to reduce noise and improve confidence levels.
- Useful reference for validating discovered keys: [streaak/keyhacks](https://github.com/streaak/keyhacks).

### 2. Subdomain Discovery (Passive)
- Extracts potential subdomains referenced inside JavaScript and JSON responses.

### 3. Cloud URLs Enumeration (Passive)
- Identifies cloud storage and service URLs across major providers:
  - AWS, Azure, Google Cloud, CloudFront, DigitalOcean, Oracle, Alibaba, Firebase, Rackspace, and DreamHost.

### 4. Dependency Confusion Detection (Passive + Registry Lookup)
- Extracts package/dependency names and verifies them against the **NPM registry**.
- Reports **critical** issues when an internal/unregistered dependency or organization is missing from NPM.
- Reports **informational** findings for identified public dependencies.

### 5. JS Source Mapper (Passive & Active)
- **Passive:** Parses inline base64-encoded JavaScript source maps.
- **Active:** Probes common `.map` file locations to reconstruct original source code when exposed.

### 6. Static Files Dumper (Manual)
- **One-click** export of static files from one or multiple targets in Burp's Site Map.
- Ideal for running external/custom regexes, grep, or local analysis pipelines on collected assets.

### 7. API Endpoints Finder (Passive)
- Extracts potential `GET`, `POST`, `PUT`, `DELETE`, and `PATCH` API endpoints referenced in client-side code.

---

## Installation & Usage

### Option 1: Pre-built JAR
1. Download the latest `.jar` file from the **Releases** page (or from the BApp Store).
2. In Burp Suite, go to **Extensions → Installed → Add**.
3. Select **Extension type: Java** and load the `.jar` file.

### Option 2: Build from Source
Requires **JDK 8–19** (Gradle 7.6):
```bash
git clone https://github.com/0xRh4ps00dy/js-miner.git
cd js-miner
./gradlew fatJar
```
The compiled JAR will be generated at `build/libs/js-miner-all.jar`.

### Running Scans
- **Passive scans** run automatically as you browse your target and static files appear in Burp's Site Map.
- **Active scans** (such as guessing `.map` files or dumping static files) are triggered manually by right-clicking a target domain in **Burp's Site Map → Extensions → JS Miner**.
- No extra Burp tab or complex configuration is required.

---

## Disclaimer

This tool is provided for **educational and authorized security testing purposes only**.  
It is the user's sole responsibility to obey all applicable local, state, and federal laws and to obtain proper authorization before testing any target. The author and contributors assume no liability and are not responsible for any misuse or damage caused by this tool.

---

## License

This project is licensed under the **Apache 2.0** open-source license. See [LICENSE.md](LICENSE.md) for the full terms.
