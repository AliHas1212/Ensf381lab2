Q1: License Implications
(a) GPLv3 as the main license means the whole project must follow its copyleft rules, even if a sub-component is MIT-licensed.
(b) The container might be affected by GPLv3 if its key scripts or components are under that license, requiring source code availability.

Q2: Docker Command
(a) Runs Grype to scan an SBOM file for vulnerabilities. Mounts the current directory, disables auto-updates, and removes the container after execution.
(b) Simplified command:

sh
Copy
Edit
docker run --rm -it -v ${PWD}:/data -e GRYPE_DB_AUTO_UPDATE=false anchore/grype sbom:/data/alpine.spdx.json
Q3: VEX Justifications & Fixing a CVE
(a) Allowed justifications for marking a vulnerability as not_affected:

Vulnerable code isn't present or not executed

Code can't be exploited

Mitigations already exist

(b) Command to mark CVE-2022-0563 as fixed:

sh
Copy
Edit
grype sbom:/data/alpine.spdx.json --exclude-vuln CVE-2022-0563
Q4: BusyBox & musl Licenses
(a) BusyBox is GPLv2, musl is MIT.
(b) No licensing issues—GPLv2 just requires source availability, and MIT is permissive.

Q5: SBOM Creation & Scanning
(a) Generate SBOM for FOSSology in CycloneDX XML:

sh
Copy
Edit
syft fossology:4.4.0 -o cyclonedx-xml > fossology-4.4.0.sbom.xml
(b) Scan SBOM with Grype without using a cache:

sh
Copy
Edit
grype sbom:fossology-4.4.0.sbom.xml --only-fixed --skip-db-update
