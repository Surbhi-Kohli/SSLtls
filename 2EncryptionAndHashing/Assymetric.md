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

Here as per the above image, only owner has the private key.
