# GPG Encryption

This guide outlines how to perform some of the most common tasks using GPG.

## Symmetric encryption

The simplest form of encryption using GPG is using a symmetric cipher (a password). With this method you will be prompted to enter a secret on the command line.

    gpg -c filename

If for some reason you wanted to create ascii encoded output, you can use the `-a` flag.

    gpg -d filename.gpg

Some versions of GPG will cache the password on creation so you are not prompted for it when decrypting. If available, you can disable this feature using the `--no-symkey-cache` flag.

### Selecting Cipher Algorithms

By default GPG will use AES-128 but you can select a different algorithm using the `--cipher-algo` switch.

    gpg -c --cipher-algo TWOFISH filename

A list of available algorithms can be viewed in the help output

    gpg -h
    ...
    Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
        CAMELLIA128, CAMELLIA192, CAMELLIA256

## Asymmetric Encryption

The most common use of GPG is to use asymmetric encryption using [public key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography). You use GPG to create both private and public key pairs.

Generate a key pair using full features.

    gpg --full-generate-key

Select the kind of key. The default is to use RSA for encryption and signing.

    Please select what kind of key you want:
        (1) RSA and RSA (default)
        (2) DSA and Elgamal
        (3) DSA (sign only)
        (4) RSA (sign only)
        (14) Existing key from card
    Your selection? 1

Select key size.

    RSA keys may be between 1024 and 4096 bits long.
    What keysize do you want? (3072) 4094

You will then be prompted for key expiry. This is useful if you want to rotate keys, but in terms of keeping it simple for personal use, you can leave this as zero (does not expire).

    Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
    Key is valid for? (0)

Continue through the steps to provide your name, email, comments and optional password.

    pub   rsa4096 2022-09-08 [SC]
          D644DA41300620DEF98A868C06C52DFD503E8B31
    uid                      Foobar <foo@example.com>
    sub   rsa4096 2022-09-08 [E]
