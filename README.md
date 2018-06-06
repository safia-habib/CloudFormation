# CloudFormation
Cloudformation templates

This respository contains the Cloudformation templates for Installing Dynatrace Managed Nodes and its components.

## ManagedClusterMaster.yaml
This CF template creates a VPC, Subnet, Security Group for a 3 Node Managed Cluster with the default size of t2.2xlarge with a 50Gb of EBS volume. 
**You will need to input the following parameters:**
1. Wget URL for Dynatrace Managed node: This is available in the email you receive from Dynatrace Managed Team
2. License Key: The license key for the Managed installer, also available in the email 
3. Initial First name: First name of the admin of Dynatrace Managed Cluster
4. Initial Last Name: Last name of the admin of the Dynatrace Managed Cluster
5. Initial Email: The email address for admin, all Dynatrace Managed Events are sent to this email 
6. Password: The password for the internal admin account which is created

**However just note that the Public Key is currently hard coded in the script to USEAST1. You will have to change this before deployment or the deployment will fail** 

Once all the parameters are input the Master node of the Dynatrace Managed cluster is created and joined to Dynatrace Mission Control 

**This template also outputs the following parameters:** 
1. VPCManagedNodeID: The ID of the VPC created for Dynatrace Managed Cluster
2. SubnetManagedNodeB: The ID of the subnet for second node
3. SubnetManagedNodeC: The ID of the subnet for third node
4. ManagedSecurityGroupID: The ID of the SG group created 
5. PublicIPMasterNodeOut: The Public IP of the created Master node

## ManagedClusterSecondaryNodes.yaml
This template uses the output from ManagedClusterMaster.yaml to add two additional nodes to the Dynatrace Managed Cluster
**Input parameters**
The name of the Stack used for creation of ManagedclusterMaster.yaml 

This template creates the Managed Nodes B and C and registers them to the Dynatrace Managed Cluster created. 
**Currently this file uses the hardcoded password. The user will need to update/ add the password parameter either from output of Master file or hardcode it in the User Data section Curl command** 
