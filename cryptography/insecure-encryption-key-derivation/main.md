# Autocomplete Enabled
> **Vulnerability ID:** `LWV <ID-Given>`
> **Control Group:** `<control-group>`
> **Tentative Severity:** `severity`


## Description
During source code review it is found that the application uses the same symmetric key for multiple users' sensitive data encryption.

## Impact

### Technical Impact
In scenarios where same encryption key used for all the users. Compromise of encryption key can affect all the users. The attacker can obtain the encryption key from his/her own account and can use the same to decrypt sensitive details of other user accounts.
### Business Impact
Business Impacts goes here


## Recommendations
It is recommended that the application should derive user specific keys using Password Based Key Derivation(PBKDF2) instead of using the same encryption keys for all the users. The following are some key guidelines for implementation of PBKDF2:

1. It is recommended that the passphrase and the salt for the key derivation should not be hardcoded in the application source code.

2. It is recommended that the application must have strong password policy to prevent decryption of sensitive data through brute-force attacks.

3. It is recommended that the salt should be derived from cryptographically secure random number. The specification suggests that the salt be a 64 bit pseudo random value.

4. Due to advancement in the computation, modern guides such as the OWASP password storage cheat sheet (2015) recommends the 10,000 iterations.

The code snippet shown below is the reference for the implementation of PBKDF2 for encryption key derivation:


### PHP
NA
### .NET
NA

### Java
    public static SecretKey generateKey(char[] passphraseOrPin, byte[] salt) throws NoSuchAlgorithmException,       InvalidKeySpecException {
    // Number of PBKDF2 hardening rounds to use. Larger values increase
    //computation time. You should select a value that causes computation
    // to take >100ms.
    final int iterations = 10000; 

     Generate a 256-bit key
    final int outputKeyLength = 256;

    SecretKeyFactory secretKeyFactory = SecretKeyFactory.getInstance(""PBKDF2WithHmacSHA1"");
    KeySpec keySpec = new PBEKeySpec(passphraseOrPin, salt, iterations, outputKeyLength);
    SecretKey secretKey = secretKeyFactory.generateSecret(keySpec);
    return secretKey;
     }


## Classification
Classification goes here

## References
  https://www.owasp.org/index.php/Cryptographic_Storage_Cheat_Sheet#Rule_-
  https://medium.com/@kasunpdh/how-to-store-passwords-securely-with-pbkdf2-204487f14e84

### PHP
PHP References go here
### .NET
.NET References go here
### Java
Java References go here

