# Manage Shares

After creation, you can view the list of shares that are associated with a Network File Storage cluster. You can also delete an existing one if it is no longer required. 

To view the list of shares, follow these steps: 

{% include "../../../includes/network-file-storage/network-file-storage-dcd-navigation.md" %} 

2\. Select **Manage Shares** from the **OPTIONS** column to view the shares associated with the respective cluster.

![Manage shares](../../../images/network-file-storage/nfs-manage-shares.png)  

Alternatively, you can also click on the cluster's **NAME** and select the **Manage Shares** tab in the **Manage shares** window.

![Manage Shares tab](../../../images/network-file-storage/nfs-manage-shares-tab.png)  

{% hint style="success" %}
**Result:** A list of all shares associated with the respective cluster are displayed. You can view the following details:

* **Directory Name:** Displays the name of the share. Select the name to view its details.
*  **QUOTA:** Displays the respective share's quota in MiB.
* **Group Id:** Displays the respective share owner's group ID.
* **User Id:** Displays the respective share owner's user ID.
*  **CLIENT GROUPS:** Displays the number of client groups that are associated with the respective share.

* **ACTIONS:** Select ![](../../../images/three-dots.png) to perform the following: 
  * **View/Edit Share:** Select the option to either view or edit its [<mark style="color:blue;">**Properties**</mark>](create-nfs-share.md#define-share-properties) or [<mark style="color:blue;">**Client Groups**</mark>](create-nfs-share.md#add-client-groups) through the **View / Edit Share** window. Click **Save** to save the updates.
  * **Copy ShareId:** Select the option to copy the corresponding share ID.
  * **x Delete Share:** Select the option to delete the chosen share and select **Delete** in the dialog box to confirm deletion. For more information, see [<mark style="color:blue;">Delete a Share</mark>](delete-nfs-share.md).
{% endhint %}

# Mount a NFS share on a linux machine

For mounting an NFS share the IP (ie. 10.7.228.5) of the cluster and the UUID (ie. 7b1ef56d-dfc6-51fe-aff0-7af2d6747868) of the share is needed.

`mount -t nfs 10.7.228.5:7b1ef56d-dfc6-51fe-aff0-7af2d6747868 /my/local/folder`

The format is:

`mount -t nfs <cluster-ip>:<share-uuid> <local-mount-path>`





