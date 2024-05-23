Unable to configure HTTPS endpoint. No server certificate was specified, and the default developer certificate could not be found

https://stackoverflow.com/questions/53300480/unable-to-configure-https-endpoint-no-server-certificate-was-specified-and-the

Solution
(for Windows, not sure if there's an equivalent issue/solution for other OSs)

In a command prompt or Powershell terminal:

Run certmgr.msc and delete all localhost certificates under both Personal\Certificates and Trusted Root Certification Authorities\Certificates.
Then run dotnet dev-certs https -t a single time to create and trust a new development certificate.
Verify by running dotnet dev-certs https --check --verbose, or just try debugging your ASP.NET app again.
You may also need to run dotnet dev-certs https --clean before creating the new certificate.
