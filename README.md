# test-asset-nessus-security-scan

Sample CONS3RT test asset that performs a Nessus security port scanning 
of either of all systems in the deployment, or systems identities with the 
`nessus.targets` custom property.  For a credentialed scan, edit the
`scripts/nessus-credentials.txt` file in this asset, or try the sample 
[Windows credentialed scan](https://github.com/cons3rt/test-asset-nessus-windows-credentialed-scan).  

## Build your own Nessus Scan Asset

Use this as a sample for building your own Nessus Test Asset.  This 
asset will not work out of the box, it will take some configuration as 
described in the steps below.  

* Clone or download this git repository
* If not using credentials, remove the `nessus.credentials` property in `config/nessus-config.properties`
* If you need a credentialed scan, update credentials in the `scripts/nessus-credentials.txt` file
* For Windows, remove the `nessus.audit` property in `config/nessus-config.properties`
* Set the `nessus.audit-category` property in `config/nessus-config.properties` to either `Unix` or `Windows`
* Updated the `name` and `description` to the `asset.properties` file
* If not using credentials, remove the `scripts/nessus-credentials.txt` file
* If using Windows, remove the `scripts/test.audit` file
* Create a zip file and import your Test Asset under the "Tests" category in CONS3RT

### Specifying Credentials

In order to run a credentialed Nessus scan, first ensure that the credentials 
exist and are valid on the target virtual machine(s).  Second, use the 
`scripts/nessus-credentials.txt` file to specify those credentials.  Multiple 
credentials may be specified with a `--break--` in between as shown in the 
sample `nessus-credentials.txt` provided in this sample asset.

```
# Windows credentials example:

credential_type=WINDOWS_PASSWORD
username=administrator
password={REPLACE_WINDOWS_ADMIN_PASSWORD}

# Linux/Unix SSH credentials example:

credential_type=SSH_PASSWORD
username=root
password={REPLACE_SSH_PASSWORD}

# Linux/Unix SSH credentials with an escalation password to become 
# root via "sudo su -"

credential_type=SSH_SUDO
username=cons3rt
password={REPLACE_SSH_USER_PASSWORD}
escalation_account=root
escalation_password={REPLACE_SUDO_PASSWORD}

# Linux/Unix SSH credenitals with a separate root user password to
# become root via "su root"

credential_type=SSH_SU
username=cons3rt
password={REPLACE_SSH_USER_PASSWORD}
escalation_account=root
escalation_password={REPLACE_ROOT_PASSWORD}


```

## Launch a Nessus Scan

There are two options for launching a scan.  First, include your Nessus Test
Asset in a deployment that includes one or more scenarios.  In this case, the 
Nessus Scanner will automatically target all systems included in the 
deployment.  Secondly, you can deploy the Nessus Test Asset on its own in 
your cloudspace, and target systems by IP address using the `nessus.targets` 
deployment property as described below.

For scanning one or more scenarios:

* Navigate to your scenario, click "Add to Deployment Builder"
* Navigate to other scenarios as needed, and click "Add to Deployment Builder"
* Navigate to your imported Nessus Test Asset, and click "Add to Deployment Builder"
* Specify custom properties as needed (see below), excluding `nessus.targets`
* Launch your deployment, and the systems is the scenario are included as targets in the scan results

For scanning specific targets:

* Navigate to your imported Nessus Test Asset, and click "Add to Deployment Builder"
* Specify custom properties as needed (see below), include `nessus.targets`, this is required
* Launch your deployment, and the targets included in `nessus.targets` are included in the scan results

## Test Results

Download the Nessus Scan results on the run page, under the "Test Results" tab.
By default, the results include a PDF file, a CSV file, and a ".nessus" file. 
A downloadable zip file is available that contains all results files.  The 
test result format is customizable 

## Custom Properties

Custom properties can be added in two places in CONS3RT.  First, as a step when saving
a deployment, or secondly, as the has step before submitting a deployment run.
Custom properties take the format of `key=value` pairs in the custom properties 
page when creating and/or launching a deployment.  For customizing your Nessus 
scan, you can set any of the properties defined below.  If a property is ommitted, 
the default value will be used.  Or particular importance, is the `nessus.targets` 
custom property.  This property is required to be set on Nessus scans, if there 
are no other scenarios included in the deployment to scan.  In addition, if you 
are scanning systems included in the deployment, do not set the `nessus.targets` 
property.

* `nessus.targets`: Specifies the target host(s) to scan. For use with test-only 
nessus deployments where there is no a scenario included in the deployment. Examples 
below.  Default is none, which scans systems in the deployment.

```
# Scan a single target by IP
nessus.targets=172.16.11.100

# Scan a target range
nessus.targets=172.16.11.1-172.16.11.255

# Scan a range by CIDR
nessus.targets=172.16.11.0/24

# Scan a resolvable host
nessus.targets=www.nessus.org

# Scan a single IPv6 host
nessus.targets=fe80::2120d:17ff:fe57:333b
```

* `nessus.format`: Specify the format of the report (`html`, `pdf`, `db`, `nessus`, 
`csv`).  Default is `pdf`.

* `nessus.chapters`: Specifies the chapters to include in report. A Semi-colon delimited 
string comprised of some combination of the following options: `vuln_hosts_summary`, 
`vuln_by_host`, `compliance_exec`, `remediations`, `vuln_by_plugin`, and `compliance`.
The default is either `vuln_hosts_summary` or `vuln_hosts_summary;compliance` if an 
audit file is detected.
