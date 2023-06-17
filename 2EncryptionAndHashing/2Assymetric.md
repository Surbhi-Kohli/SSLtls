 <img width="466" alt="Screenshot 2023-06-16 at 11 17 09 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/9f609c60-8407-42bc-ad1d-7b5fcd1b954e">  

Pair of 2 keys:private and public,which usually have same length.

**Private key** is always kept secret and only the owner of private key has its info.  
**Public Key** can be shared with anyone.
But what is the purpose of 2 keys??  

 * The pair can be used for encryption,where public key is used to encrypt data which can only be decrypted by a private key.  
 * Signing data using private key:Owner of keys signs data, or creates a hash in other words, using the private key .And then anyone who has public key ,may 
       verify the signature.

## Encrption using Assymetric keys:     

<img width="675" alt="Screenshot 2023-06-16 at 11 33 59 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/3bb59a6d-cce7-467b-8601-31988edeb842"> 

Here as per the above image, only owner has the private key.Data is encrypted by public key.It can be decrypted only by private key which is there only with the owner

## Signing data using assymetric keys:
In the following scenario , data is sent along with encrypted hash.(This is how **data signing** is done)Hash is encrypted using a private key.
The below scenario is used when we want the receiver to be sure that the data they received was from a genuine owner,who owned the private key.This means ,no one else would be able to send data and hash as what the owner sends..Thats because only genuine owner has the private key to encrypt a has h that can be decrypted by the public key that the owner has.This also imposes data integrity so that no one on the way mutates data or hash, or else the receiver would get to know it when he decrypts hash with key and finds that it is different from hash he himself generates using the data.
**Signing** is just a way to ensure that we received data from correct sender.
<img width="635" alt="Screenshot 2023-06-17 at 1 03 52 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/87f79f70-6276-45ae-8102-adeca55a0584">

But here, we have not encrypted the data and hence it can be viewed on the way, if not tempered.Here we are just talking about signing.We will talk about signing and encrypting data later.

This process is very important because that's what exactly happens when server sends a certificate to the client.Each certificate contains signature of the owner of certificate and the signature is verified exactly in the above mentioned way.

Q.how a Client gets a public key in a first place? If a Client downloads a public key from somewhere then how it can be sure that the key was not substituted by someone else in middle of the road?  

a.if we talk about establishment of the TLS session, then public key is located in the TLS certificate that is presented by the server to the client at the beginning of the TLS session setup.And the browser trust the certificate if and only if it's been issued by CA.

## RSA overview: 
The single main protocol that is primarily used in modern networks and cert communications is called RSA protocol.
 <img width="685" alt="Screenshot 2023-06-17 at 1 33 03 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/ae6a1c34-c36f-41ac-a777-fb105f3b93ef">  
  RSA is not just a simple protocol, it is actually public-key crypto system.
 With RSA , you can create private, public key pairs,create pairs with different lengths,perform encryption, decryption ,sign data and so on.Lengths of RSa keys is between 1024 and 4096, but primarily 2048 bits keys are used.And please note that the key length is always the same for private and public key, because each time when you generate Key pair, both keys are generated together and you are not able to generate only private key or only public key.

Private key must always be kept a secret and if you feel that the private key got compromised,you can generate a new pair.And if you need a certificate based on that pair, you need to recreate certificate as well.

RSA is system that allows you to perform different actions based on assymetric keys.
## PKI - Public Key Infrastructure overview

PKI is public key infrastructure and the PGI is actually a set of different protocols, algorithms,and its certificates that allow you to perform communication based on certificates, based on trust.And using those trust relations, you could perform encryption of data, you can perform authentication
of the server you are communicating with and so on.  
<img width="622" alt="Screenshot 2023-06-17 at 2 04 19 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/8d8cc276-5b6a-4930-ad2a-2dee6e63da8b">
There are many elements in PKI infrastructure eg CA= Certification Authority.The role of CA is to either sign certificates or delegate trust to other entities and those entities are called Intermediate CA.Usually the main responsibility of Intermediate CAs is signature of new certificates that are issued for other entities eg for your website.And of course, there are different owners of certificates .  
You can use a certificate for different purposes, for example, you can use certificate for SSL encryption ,ssltls encryption to secure your website.Or you can use certificate to build a VPN virtual private network and send data over internal security
So there are many different use cases for certificates.

But what is a certificate?
Certificate is a set of data And most important information that are stored by any certificate is public key of the owner of certificate.
It means that every entity in PKI infrastructure has its own public key and this public key is always included in every certificate(as shown in image below, intermediaate CA also has its public key).

<img width="571" alt="Screenshot 2023-06-17 at 2 17 47 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/bef76ef5-0403-4989-a6b9-6600f0973d13">
 Goal of PKI infrastructure is to ensure that public key for every entity in PKI infrastructure is trusted by other entities. And that's why we need CAs, intermediate CS and so on.

 ## Certificate Overview:
 <img width="428" alt="Screenshot 2023-06-17 at 2 22 48 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/4273573a-b7df-4f11-9aba-9b9a8443471f">
 Certificate is a digital entity, infact it is a file with some data.Following info is included in the certificate:
  * Info about the owner of the cert:Usually it may be company name, company address, website and so on. Sometimes even serial number of cert is included  
       here in this section.
  *Info about issuer:Find information about entity that signed this certificate and usually here you will find information about certification authority 
  or intermediate certification authority. Entity that, again, has signed this certificate.
  *Signature(it is hash encrypted using private key). If certificate was issued by any certification authority or intermediate certification authority, 
    this signature is made by that authority and based on the signature, we can build a chain of trust.If a certificate is signed by a CA and we trust the 
   CA,we trust the owner of the certificate too.  **Self signed certificates**:Certificate issued and signed by the owner.The signature is made using the private key of the owner of certificate.  
* Public Key: And most important information that is stored in each certificate, is public key.So entire goal of certificate is to store public  and this public is owned by owner of certificate,not by the issuer.And of course, in certificate you will not find the private key because private key must always be kept secret.

And every certificate is usually available for public and you can be free to download certificate of any entity in the world.
Based on certificates, we can build chains of trust.
