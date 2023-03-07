## Steps of creating a VPC peering connection in AKS managed  and pinging one cluster from another:
- ### Create Virtual Network:
  - Go to Azure Portal (Home page)
  - Click on "Create a resource" on the left-hand side of the page.
  - Search for "Virtual Network" in the search bar and select "Virtual Network" from the list of results.
  - Click on the "Create" button on the Virtual Network page.
  - Fill in the required information, such as the name of the virtual network, the address space, and the subnet details.
  - Choose the subscription, resource group, and location for the virtual network.
  - Click on the "Create" button to create the virtual network.
- ### Create Cluster:
  - Create cluster using this command:
  ```bash
  az aks create --resource-group mygroup --name test-cluster --node-count 3 --generate-ssh-keys --network-plugin azure --vnet-subnet-id /subscriptions/1bfc9f66-316d-433e-b13d-c55589f642ca/resourceGroups/mygroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
  ```
  - Replace ``myVnet`` with your virtual network name and ``mySubnet`` with your subnet name.
- ### Create VPC Peering:
    - Create Clusters
    - Create a virtual network peering: Create a virtual network peering: In the Azure portal, navigate to the "Virtual network" section and select the virtual network for the first AKS cluster. Under "Settings," select "Peerings" and then "Add."
    - Configure the peering: Give the peering a name, select the second AKS cluster's virtual network as the remote virtual network, and set the peering type to "Allow virtual network access."
    - Accept the peering: (Skip if the peering is already showing status connected_ In the virtual network for the second AKS cluster, repeat step 3 to create a peering, but instead of creating a new peering, accept the peering created in step 4.
- ### Now Ping 