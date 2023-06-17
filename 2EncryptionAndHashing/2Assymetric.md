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
The below scenario is used when we want the receiver to be sure that the data they received was from a genuine owner,who owned the private key.This means ,no one else would be able to send data and hash as what the owner sends.This also imposes data integrity so that no one on the way mutates data or hash, or else the receiver would get to know it when he decrypts hash with key and finds that it is different from hash he himself generates using the data.
**Signing** is just a way to ensure that we received data from correct sender.
<img width="635" alt="Screenshot 2023-06-17 at 1 03 52 PM" src="https://github.com/Surbhi-Kohli/SSLtls/assets/32058209/87f79f70-6276-45ae-8102-adeca55a0584">

But here, we have not encrypted the data and hence it can be viewed on the way, if not tempered.Here we are just talking about signing.We will talk about signing and encrypting data later.



Q.how a Client gets a public key in a first place? If a Client downloads a public key from somewhere then how it can be sure that the key was not substituted by someone else in middle of the road?
a.if we talk about establishment of the TLS session, then public key is located in the TLS certificate that is presented by the server to the client at the beginning of the TLS session setup.And the browser trust the certificate if and only if it's been issued by CA.
