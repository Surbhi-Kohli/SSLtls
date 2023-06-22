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
