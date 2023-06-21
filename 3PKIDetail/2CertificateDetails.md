<img width="542" alt="Screenshot 2023-06-18 at 10 35 26 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/83c78732-5bb6-453c-8fe5-5fcf9642c83d"> 

## CA Details
 <img width="544" alt="Screenshot 2023-06-18 at 10 51 33 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/94a701f6-768e-4294-9a76-9eac0756bac1">  

## Subject Details
<img width="517" alt="Screenshot 2023-06-18 at 10 46 35 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/694ff056-8134-47e4-8bd0-47b31b4d08a1">

## Signature details of certificate
<img width="526" alt="Screenshot 2023-06-18 at 10 57 11 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/b99c4b0b-8506-4bdd-a797-67d0b13fed13">     

Considering this diagram,our data here is the certificate for which we created the hash  
 
<img width="454" alt="Screenshot 2023-06-18 at 11 01 36 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/43af3eff-b0cd-4eec-a895-620d5b801d56"> 

The private key of intermediate ca was used to encrypt the hash.You can see the signature below  

<img width="476" alt="Screenshot 2023-06-18 at 11 04 17 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/e1d2d6ce-7c49-49ef-aea1-ec2d985917f3">

## Public Key
<img width="544" alt="Screenshot 2023-06-21 at 9 20 06 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/a29d7987-25c7-48dd-a81a-02ed0d37493d">


## Extension
<img width="525" alt="Screenshot 2023-06-21 at 9 29 19 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/1c3205e3-987e-4e11-bba5-8e23cd5ca119">

## Fingerprints
<img width="565" alt="Screenshot 2023-06-21 at 9 35 02 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/a8493083-d852-46fa-947d-01df06d5afb3">


Q.The Signature was encrypted using intermediate CA's private key.
Does it mean that during the establishment of the TLS session, the client (web browser) needs to first request the public key of the intermediate CA in order to validate the integrity of the certificate of the webserver?
A.yes.When client initiates connection, web server sends its own certificate and entire chain of certificates of the CAs that were used to sign certificate of the web server.

Q.There is only one public key mentioned in the certificate, but we have 2 tasks to do, (both needing public keys from different entitites):

1) First is to verify the encrypted signature to determine that the certificate has indeed been sent by the CA. For this, we need the public key of the CA.

2) Second is to encrypt information to be sent to owner server, so that general app related information movement can happen between client and server. For this, we need the public key of the owner, in this case, instagram.

As per what you said here, I understand that the public key mentioned is of the owner, i.e Instagram. So we can only do the second functionality but not the first. So how do we verify the authenticity of the certificate, if we don't have the public key of the CA?

A.root CA keys are already saved in the browsers as they are trusted by all over the world & few so browsers come up with their keys pre-installed

if you are using google chrome go to settings

Settings -> privacy & security -> Security -> Manage Certificates
Root CA certificates are built-in into the most operation systems and web browsers. Therefore all certificates signed by those root CAs or their subordinate CAs (intermediary CAs) are trusted.

Fake CAs are not trusted.
