![Burp JS Hunter Banner](assets/header.jpg)

# Burp JS Hunter

**Burp JS Hunter** is a Burp Suite extension focused on automated reconnaissance of client-side static assets—specifically **JavaScript (`.js`)** and **JSON (`.json`)** responses—to surface exposed credentials, hidden endpoints, cloud infrastructure references, and supply-chain risks.

> **Note:** Static analysis inherently produces false positives. Burp JS Hunter is built to speed up initial reconnaissance and should always be paired with manual verification.

---

## Capabilities

| Module | Mode | Description |
| :--- | :--- | :--- |
| **Secrets & Credentials** | Passive | Detects hardcoded API keys, tokens, and secrets using pattern matching and Shannon entropy filtering. |
| **API Endpoints** | Passive | Extracts potential `GET`, `POST`, `PUT`, `DELETE`, and `PATCH` routes from client-side code. |
| **Cloud Storage & Services** | Passive | Flags URLs belonging to AWS, Azure, GCP, CloudFront, DigitalOcean, Oracle, Alibaba, Firebase, Rackspace, and DreamHost. |
| **Subdomains** | Passive | Harvests subdomain references embedded in static files. |
| **Dependency Confusion** | Passive + Lookup | Identifies package names and checks the public NPM registry for unregistered/missing packages or organizations. |
| **Source Maps** | Passive & Active | Decodes inline base64 source maps passively and actively probes common `.map` paths to reconstruct source code. |
| **Static Asset Dumper** | Manual | Exports all static files for selected targets from Burp's Site Map for offline analysis. |

---

## Getting Started

### Loading the Pre-built Extension
1. Download `burp-js-hunter.jar` from the **Releases** section.
2. Open Burp Suite and navigate to **Extensions → Installed → Add**.
3. Choose **Extension type: Java**, select the `.jar` file, and click **Next**.

### Building from Source
Requires **JDK 8–19**:
```bash
git clone https://github.com/0xRh4ps00dy/burp-js-hunter.git
cd burp-js-hunter
./gradlew fatJar
```
The compiled JAR will be output to `build/libs/burp-js-hunter.jar`.

### Usage
- **Passive modules** run automatically while you browse your target and static files populate Burp's Site Map.
- **Active modules** (source map probing and static file dumping) are launched by right-clicking a host in **Site Map → Extensions → Burp JS Hunter**.

---

## Disclaimer

This software is intended strictly for **authorized security testing and educational use**.  
You are solely responsible for complying with all applicable laws and obtaining explicit permission before scanning any target. The author assumes no liability for any misuse or damage resulting from this tool.

---

## License

Licensed under the **Apache License 2.0**. See [LICENSE.md](LICENSE.md) for details.
