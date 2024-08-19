# <center>Security</center>

<br></br>



## Encryption
To encrypt data, you use storage client library to first create a content encryption key (CEK). You then encrypt data on your end by CEK. This key is then encrypted through a key encryption key (KEK). A KEK can be either one you already have or one that's stored in Key Vault. Finally, the encrypted data can be stored in Azure Storage. This process is called envelope encryption.

![](./Images/cek1.svg)

<br></br>



## Shared Access Signatures
A shared access signature (SAS) is a signed URI that points to one or more storage resources and includes a token that contains a special set of query parameters. The token indicates how the resources might be accessed. One of the query parameters, the signature, is constructed from SAS parameters and signed with the key that was used to create SAS. This signature is used by Azure Storage to authorize access to storage resource.

Azure Storage supports three types of shared access signatures:
1. User delegation SAS: secured with Entra credentials and also by the permissions specified for SAS. A user delegation SAS applies to Blob storage only.
2. Service SAS: secured with storage account key. A service SAS delegates access to Blob storage, Queue storage, Table storage, or Azure Files.
3. Account SAS: secured with storage account key. An account SAS delegates access to resources in one or more of the storage services. All of the operations available via a service or user delegation SAS are also available via account SAS.

When you use a SAS to access data stored in Azure Storage, you need two components. The first is a URI to the resource you want to access. The second is a SAS token that you've created to authorize access to that resource. In a single URI, such as `https://medicalrecords.blob.core.windows.net/patient-images/patient-116139-nq8z7f.jpg?sp=r&st=2020-01-20T11:42:32Z&se=2020-01-20T19:42:32Z&spr=https&sv=2019-02-02&sr=b&sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D`, you can separate the URI from SAS token as follows:
- URI: `https://medicalrecords.blob.core.windows.net/patient-images/patient-116139-nq8z7f.jpg?`
- SAS token: `sp=r&st=2020-01-20T11:42:32Z&se=2020-01-20T19:42:32Z&spr=https&sv=2019-02-02&sr=b&sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D`