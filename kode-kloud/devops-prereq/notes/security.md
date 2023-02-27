# Security

## SSL and TLS Basics

A certificate is used to guarantee trust between two users during a transaction

Scenario:
- User accessing online banking w/o security
  - Credentials open to hackers sniffing on network
  - Encryption basically converts data to random numbers providing a key for decryption
    - W/o key, attacker can't decrypt
    - User must send key over same network w/ symmetric encyption
  - Asymmetric encryption
    - Pair of keys
      - Private key
      - Public lock
        - Encrypting w/ lock can only be unlocked w/ private key
        - Lock can be shared w/ others
        - Private key not shared
Other scenario:
- Encrypting access to servers

Generate public and pribade keypairs (two files created):
```sh
ssh-keygen
#=> id_rsa id_rsa_pub
```

Secure servers by shutting down all acces to it through an entry in lock file.

```sh
cat ~/.ssh/authorized_keys
#=> ssh-rsa AAAAB3NzaC1yc_khtUBfoTz1BqR usr1

# Specify location of pribate key when sshing
ssh -i id_ras user1@server1
```

How to secure more than one server in environment w/ key pair?
- Create copies of public lock and place them on as many servers as desired.

What if other users need access to a single system?
- They can generate their own public and private key pairs as the only one who has access to those servers, the admin (you) can provide them access/a door and lock them w/ their public locks.

Copy third party public locks to all servers:

```sh
cat ~/ssh/authorized_keys
#=> ssh-rsa AAAAB...

# ssh-rsa AAAXC...
```

Securely transfer symmetric key to server w/ assymetric encryption.
```sh
openssl genrsa -out my-bank.key 1024
#=> my_bank.key

openssl rsa -in my-bank.key -pub > mybank.pem
#=> my-bank.key mybank.pem
```

Scenario: __transfer user's _symmetric key_ to server__

When the user first accesses the web server using https, he gets the asysmetric public key from the server, and one can assume a sniffig attacker also gains access to the public key.

- The user's browser encrypts locally stored the _symmetric_ key using the public key provided by the server.
- Symmetric key sent to server
- Attacker gains access to symmetric key but can't decrypt
  - Attacker does not have private key to decrypt and retrieve symmetric key
  - __Server _only_ has assymetric _private key_ __
- Symmetric key now only available to user and server
