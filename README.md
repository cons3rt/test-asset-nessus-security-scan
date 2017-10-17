# test-asset-nessus-security-scan
Sample CONS3RT test asset that performs a Nessus security port scanning of all systems in the deployment.  Provide credentials for more a exploratory security scan.

Reference this [CONS3RT knowledge base article](https://kb.cons3rt.com/kb/elastic-tests/building-a-nessus-test) for more information about creating your own Nessus test asset.

### Recipe for using this sample Nessus Scan

* Clone this git repository
* If you'd like the more exploratory scans, update the the scripts/nessus-credentials.txt file with the credentials you plan to apply to your systems.
* If desired, edit the name and description and other info in the asset.properties file.
* Create a zip file containing the parent directory, this is your asset zip file/
* Follow [this article](https://kb.cons3rt.com/kb/assets/importing-your-asset-zip-file) to import your asset zip file into CONS3RT.
* Once your asset is imported, you will receive an email, and it will be available in CONS3RT under "Tests" from the main menu.
* Follow [this article](https://kb.cons3rt.com/kb/deployments/creating-a-deployment) to add your new Nessus Test to a deployment, and run a scan!

Please feel free to contact the CONS3RT community team with any questions: [support@cons3rt.com](mailto:support@cons3rt.com).

---

# **_Basic Nessus Security Scan_**

This test asset should be added to a deployment whenever a nessus scan is desired.  It is not bound to any particular system module configuration (virtual host, physical host, appliance, device).  It supports scanning multiple non-homogeneous host types (i.e linux, windows, etc).  

If this test asset is included within a deployment alongside other hosts, those hosts will be scanned for vulnerabilities, unless the scan is otherwise directed at a target by deployment properties. 

If login credentials for the hosts to be scanned are provided in the nessus-credentials.txt file, more exploratiry login security scans will be run.

This test can also be used in a test-only deployment to scan any desired target using the nessus.targets property.

## **Deployment Properties:**

* nessus.targets  :  Specifies the target host(s) to scan. For use with test-only nessus deployments

_Targets can be entered by single IP address (e.g., 192.168.0.1), IP range (e.g., 192.168.0.1-192.168.0.255), subnet with CIDR notation (e.g., 192.168.0.0/24), resolvable host (e.g., www.nessus.org), or a single IPv6 address (e.g., link6%eth0, fe80::2120d:17ff:fe57:333b, fe80:0000:0000:0000:0216:cbff:fe92:88d0%eth0)._ 

* nessus.format  :  Specifies the format of the report.

_options are <span class="s1">pdf</span>, <span class="s1">html</span>, and <span class="s1">db</span> (<span class="s1">nessus</span> and <span class="s1">csv</span> formatted reports will be generated in addition. **Default is pdf**)_

* nessus.chapters  :  Specifies the chapters to include in report

_expecting a <span class="s1">semi</span>-colon delimited string comprised of some combination of the following options: vuln_hosts_summary, vuln_by_host, compliance_exec, <span class="s1">remediations</span>, vuln_by_plugin, compliance _

**_Default: vuln_hosts_summary or vuln_hosts_summary;compliance if audit file is detected_**
