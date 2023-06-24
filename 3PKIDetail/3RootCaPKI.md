## What is root certification authority?
<img width="520" alt="Screenshot 2023-06-22 at 10 19 36 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/fe289edb-4555-40d9-b7e1-f344630b428c">     

For the root CA, the subject and the issuer are the same and that means that the certificate is **self signed**.For the following example, it would mena that GTS Root R1 has issued certificate for itself.Even the signature is made by the GTS Root R1 itself.

<img width="486" alt="Screenshot 2023-06-22 at 10 20 09 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/78632e75-8765-45ae-85ab-1bc379c13943">

<img width="525" alt="Screenshot 2023-06-22 at 10 20 17 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/550a2aac-f240-46f9-89e7-ed86ba9f1003">
 
## How does the web browser trust the self signed certificate of the Root CA??  
 
Any company might create a self signed certificate and so how could we trust their sellf signed certificates??.
A.Every operating system such as Mac OS or Windows ships with a list of all certificates of Root CAs and this(as shown above) certificate isn't an exception.

 To check the list of certificates of famous root CAs in ur mac,open keychain access app and go to System Roots.You will find the certificates of all Root CAs. 

 <img width="862" alt="Screenshot 2023-06-22 at 10 28 25 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/bce2adea-c48d-4d04-b5bb-20fa27078dd3">
<img width="869" alt="Screenshot 2023-06-22 at 10 28 12 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/71a5a586-6bcb-499a-bc5c-5c7e6303ea15">
The certificates get updated when u update your operating system. 
Lets explore the certificate of GTS Root R1
 <img width="500" alt="Screenshot 2023-06-22 at 10 33 46 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/b929c0ab-b388-47a4-a48a-11844eb02a32">
The details are same as that found from google.com's certificate.
These certificates are trusted by OS and by web browser by default.

## Does this list of trusted Certificates includes the certificate of intermediate CAs??
No those certificates are not there.Thats because, if there is trust between Root CA and OS , Root CA and intermediate CA, then there is trust between Intermediate CA and OS.

## How chain of trust is build??
At the top level of every chain ,there is rootCA, then comes usually intermediate CA.But actually in this chain , there may be several intermediate CAs one after the other.
At the end of every chain, there is end user certificate that may be used for webserver,or vpn or something else.


So let's have a look at this diagram where I have outlined how chain of trust is built.At the left, you see rootCA and its certificate.Then comes intermediate CA and its certificate and finally comes end user certificate that was issued by Intermediate CA. 

 <img width="1203" alt="Screenshot 2023-06-24 at 1 46 08 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/0cc4dca3-4bc9-4b11-896f-3bd716592345">  
   
**1.First go through the RootCA**:It has a self signed certificate.It means that it used its private key and using this private key sha hash of this certificate was
encrypted and the signature was added to this self signed certificate.Owner info and issuer info in self signed certificate is same.
Also , keep in mind, that every entity in the Public Key Infrastructure has a pair of keys: public key and private key.  

**2 Intermediate CA**:Signature of the intermediate CA certificate is made using the private key of the root CA.Also the owner info and the issuer info are different.Issuer info is about the Root CA info.The signature is created as follows: so firstwe take intermediate ca certificate, create a hash based on
 this certificate and after that we encrypt that hash using the private key of the Root CA.When the root CA signs, it tells that it trusts the intermediate CAs.As a sign of trust, the signature is added.Also the root CA adds issuer info.

**3 The end user certificate**: This may be used for webservers, vpns ,etc.End user certificate is signed by the intermediate CA(not by root ca).Again ,the issuer info is added by the intermediate CA to the end user's certificate.


**Question**:How end user certificate gets securely signed by the private key of the intermediate CA.
**Answer**:Signing occurs on the intermediate CA's server.With it's private key, intermediate CA securely signs CSR(Certificate Signing request) received from the end user.

A CSR(Certificate signing request) is created on end user machine and after that sent to Intermediate CA server.The intermediate CA signs the certificate, adds all required info and finally sends it back to the server.It means that signing process always occurs on a machine where private key is located.It means that signing process is secure and reliable 

## Verifiying Chain of trust:How is a certificate verified?

So when you open up any Web page and you see HTTPS sign near it, Web server sends you as an ssl certificate.It infact sends its own certificate as well as the certificates of all Intermediate CAs.And then the verification process starts on your end with end user certificate .Your computer looks at current date and compares the validity period of the certificate with your current date.  

Next check is the check of signature.Your computer finds the issuer info from the certificate and tries to find a certificate with that issuer as owner.(Remember that webserver did send certificates of intermediate CAs).Once the certificate with the said owner is found,u look for the public key for that certificate . 
 
1.This key is used to decrypt your end user certificate's signature.  
2.Web browser then generates hash from the contents of the web server certificate and compares it to the hash retrieved on the step 1.  
3. If they match - signature is verified

Thats how trust between intermediate CA and end user certificate is established.
Now you will look at the Issuer info in intermediate certificate.This will give info about the root ca.We will find this certificate in our OS.This root ca's public key will be used to decrypt signature of the intermediate ca certificate.If the match happens as illustrated before,the trust between Root CA and intermediate CA is established.

<img width="1275" alt="Screenshot 2023-06-24 at 10 35 59 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/5703371d-67b1-4fbb-9f2e-cdf1433100b8">


That means that entire chain of trust was verified by our computer, and that means that we can proceed and build secure a tunnel with the web server that has offered us this certificate.And at this moment, Web browser will show you here this look icon and it will show that certificate is valid.


q. whats is the use of intermediate certificate in chain of trust. Can't the same thing(trust) is achived only with root and domain certificate.
A.It can be achieved but root certificates must be as secure as possible and have long validity period and be trusted by operating systems all over the world.
That's why they are not used for signing of domain certificates.


<img width="741" alt="Screenshot 2023-06-24 at 11 16 00 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/06a4a711-4fb5-4b19-b358-b82e96d4d166">
Cost of Single domain certificates<Cost of wildcard < Cost of multi domain certificates
