# test-asset-nessus-security-scan
Sample CONS3RT test asset that performs a Nessus security port scanning of all systems in the deployment.  Provide credentials for more a exploratory security scan.

Reference these [CONS3RT Knowledge Base articles](https://kb.cons3rt.com/kb/testing) for more information about creating your own test asset.

### Recipe for using this sample Nessus Scan

* Clone this git repository
* If you'd like the more exploratory scans, update the the scripts/nessus-credentials.txt file with the credentials you plan to apply to your systems.
* If desired, edit the name and description and other info in the asset.properties file.
* Create a zip file containing the parent directory, this is your asset zip file/
* Follow [this article](https://kb.cons3rt.com/kb/assets/importing-your-asset-zip-file) to import your asset zip file into CONS3RT.
* Once your asset is imported, you will receive an email, and it will be available in CONS3RT under "Tests" from the main menu.
* Follow [this video](https://www.youtube.com/watch?v=kL7P2s_eyLo) to add your new Nessus Test to a deployment, and run a scan!

Please feel free to contact the CONS3RT community team with any questions: milcloud@jackpinetech.com.
