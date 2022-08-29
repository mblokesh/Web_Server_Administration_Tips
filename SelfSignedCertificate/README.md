# How to create a self signed certificate on a Windows Server

```
New-SelfSignedCertificate `
   -CertStoreLocation Cert:\LocalMachine\My `
   -DnsName "remote.itechki.com" -Verbose
```

**Add a password to the certificate**

```
$pwd = ConvertTo-SecureString -String "pwd@123" -Force -AsPlainText
```

**Export**

**Replace the below Thumbprint from the results of the "New-SelfSignedCertificate"**

```
Export-PfxCertificate -cert cert:\localMachine\my\'336255C639B92978BDAA5144B92A540859932A8A' -FilePath root-authority.pfx -Password $pwd
```

**Ex:Output**

```
PS C:\Windows\system32> New-SelfSignedCertificate `
>>    -CertStoreLocation Cert:\LocalMachine\My `
>>    -DnsName "remote.itechki.com" -Verbose
VERBOSE: Performing the operation "Create a new self-signed certificate" on target "Cert:\LocalMachine\My".


   PSParentPath: Microsoft.PowerShell.Security\Certificate::LocalMachine\My

Thumbprint                                Subject
----------                                -------
336255C639B92978BDAA5144B92A540859932A8A  CN=remote.itechki.com


PS C:\Windows\system32> $pwd = ConvertTo-SecureString -String "pwd@123" -Force -AsPlainText
PS C:\Windows\system32> Export-PfxCertificate -cert cert:\localMachine\my\336255C639B92978BDAA5144B92A540859932A8A -FilePath root-authority.pfx -Password $pwd


    Directory: C:\Windows\system32


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        29-08-2022     12:23           2653 root-authority.pfx
```