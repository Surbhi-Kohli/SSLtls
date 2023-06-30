A certificate is used primarily for establishing trust between Web browser and Web server.But the certificate is not used itself for encryption 
of data between Web browser and web server.And that's where SSL and the TLS protocols come in.

**SSL**: Secure Sockets Layer, **TLS**: Transport Layer Security.Both of these are cryptographic protocols.And that means that they are used primarily for encryption of data.These protocols are used in HTTPsBut what is the connection between SSL/TLS and certificate? 

**Does certificate depend on SSL, TLS and does it require which protocol exactly must be used?**  
Ans:A certificate does not dependent on protocol and does not say exactly which protocol either SSL or TLS must be used for data encryption.It means that the same certificate may be used either for SSL or TLS.

Sometimes you may hear term as SSL certificate, TLS certificate, or SSL/TLS certificate.Its better to just use the term certificate.
But if you want to be more specific and tell others that you are talking about digital certificates, you can use term SSL/TLS certificate.

Very often , they are termed as SSL certificates,This is wrong and we will see in next notes about why.


 ## History and versions of SSL and TLS

 <img width="993" alt="Screenshot 2023-06-30 at 1 50 59 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/0646d47f-a303-476d-8032-2f5310cf4624">

 As per the image above, we see various versions of SSL and TLS certificates.We see that SSL protocols are depricated and that is why the term ssl certificate is incorrect, and we should use the term TLS certificates.  
<img width="504" alt="Screenshot 2023-06-30 at 2 02 08 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/997d2532-6fe7-4f5e-a581-3e5257a9292c">
Protocol support is configured on web servers.If you are responsible for certificate setup and configuration of ssl and tls protocol, you should setup list of supported cryptographic protocols on the server.Prefer disabling the older depricated protocols and have the TLS 1.2 and TLS 1.3 
as enabled.
Never use SSL protocols and they have lot of vulnerabilities and are prone to attacks..

## Why RSA is not used in for data encryption in HTTPS?
Recap that RSA is assymetric key crypto system, where you encrypt data using public key of the ower and receiver(owner) decrypts it using it using its private key.Following are the reasons why rsa is not used for encryption of data in HTTPs:

 1. RSA encryption is slow:Encrption via RSA takes more time than any other symmetric key encrption algorithms.
 2. Bi-directional data encrpytion requires RSA key pairs on both sides:Communication between Web browser and web server is is always bidirectional.That means that the encrypted data must be sent from web browser to web server and vice versa.If you want to use RSA , you need to setup prublic and private key pairs both on web browser and web server..

