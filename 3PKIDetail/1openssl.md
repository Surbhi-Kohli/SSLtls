
## Installing Openssl
Now it's time to install a tool that will allow us to generate RSA keys,to create certificate signing,request, the request for new certificate and so on, and the best tool here is the open SSL.On mac, openssl is already installed.
The OpenSSL Project develops and maintains the OpenSSL software - a robust, commercial-grade, full-featured toolkit for general-purpose cryptography and secure communication.

# Using Openssl for RSA keys generation
Type `openssl` in terminal,if you get the following prompt,it means openssl is installed.
<img width="541" alt="Screenshot 2023-06-17 at 9 24 23 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/2d699090-f83f-4d22-97ff-6d2f865e5e1b">  

To generate rsa key ,type `openssl genrsa`.A private key will be generated which is 2048 bits long.  

<img width="528" alt="Screenshot 2023-06-17 at 9 17 51 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/2933f5f5-ccb6-4a1f-aa3e-1ea1afb59f89">  
 
But this is compromised as it is not encrypted.To encrypt the key,use `opensll genrsa -aes256` .You will be asked for a passphrase and this passphrase will be used for encryption of private key.  You will now get a private key that is encrypted using aes256 algo. 

<img width="506" alt="Screenshot 2023-06-17 at 9 32 06 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/2fbf5fd1-0b70-402a-88a5-c73304854d22">  

You can also encrypt using other algorithms.
For example you might use obsolete algorithm like des or 3des.    
 
<img width="512" alt="Screenshot 2023-06-17 at 9 41 06 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/9fa4954a-6e82-4ebd-87e4-bf095f922731"> 
 
You can have the private key written in a file via command `openssl genrsa -aes256 -out <filename>.pem`.  This will generate a private key and create a private.pem file and add the private key to that file. 

<img width="593" alt="Screenshot 2023-06-17 at 9 46 49 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/0c13d1a2-3f55-4b47-b637-a369c58f1037">  
 
You can see the contents of the file using `cat private.pem` 
 
<img width="488" alt="Screenshot 2023-06-17 at 9 53 24 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/2df3ed90-7003-46c1-b17b-50069c6affbe">

What is .pem??,.pem is an extension that is used for files that include certificates or private keys.

We generated private key , but what about public key.We initially studied that private key and public key are always generated together.So where is public key??Public key also encoded here within the private key.You can access that using command `openssl rsa -in private.pem -outform PEM -pubout -out public.pem`   
 
<img width="814" alt="Screenshot 2023-06-17 at 10 40 20 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/f0c84b41-be58-4d73-92cf-4b8fef689941">

After `-in` option, we specify file where our private key is stored(here it is private.pem).Next, we should specify format in which we want to extract the public key, and for that we should use option `-outform` and type PEM here in capital letters.After that comes another option(-pubout) that tells openssl that we want to extract the public key.And finally, we want to extract the public key into separate file called public.pem. 
And for that we should add one more option `-out` and then specify name of the file.
You will be prompted for passphrase.You have to enter the same passphrase that you used when creating private key.
You can finally see the public key that you can share with the world and any person could use this publicly for encryption of the data that is sent to you and only you are able to decrypt it using your private key. 

<img width="561" alt="Screenshot 2023-06-17 at 10 46 45 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/3ba9b569-ccfb-4a2c-bba9-ebaf084abc95">    

Public and private key are bound together, and if you want to create another public, you must create another key pair and after that create public key based on your private key.

Lets now create an rsa key of another length.By default the length is  2048bits.    
<img width="622" alt="Screenshot 2023-06-17 at 10 51 58 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/6332ce9c-d515-4190-a1c0-cb96fd55072b">

We generated the key, but we didnt encrypt it.Not a good practice.
