A cryptosystem is an implementation of cryptographic techniques and their accompanying infrastructure to provide information security services. A cryptosystem is also referred to as a cipher system.

The various components of a basic cryptosystem are Plaintext, Encryption Algorithm, Ciphertext, Decryption Algorithm, Encryption Key and, Decryption Key.

Where,Encryption Key is a value that is known to the sender. The sender inputs the encryption key into the encryption algorithm along with the plaintext in order to compute the cipher text.

Decryption Key is a value that is known to the receiver. The decryption key is related to the encryption key, but is not always identical to it. The receiver inputs the decryption key into the decryption algorithm along with the cipher text in order to compute the plaintext.

Fundamentally there are two types of keys/cryptosystems based on the type of encryption-decryption algorithms.

### Symmetric Key Encryption
The encryption process where same keys are used for encrypting and decrypting the information is known as Symmetric Key Encryption.

The study of symmetric cryptosystems is referred to as symmetric cryptography. Symmetric cryptosystems are also sometimes referred to as secret key cryptosystems.

Following are a few common examples of symmetric key encryption −

1. Digital Encryption Standard (DES)
2. Triple-DES (3DES)
3. IDEA
4. BLOWFISH

### Asymmetric Key Encryption
The encryption process where different keys are used for encrypting and decrypting the information is known as Asymmetric Key Encryption. Though the keys are different, they are mathematically related and hence, retrieving the plaintext by decrypting cipher text is feasible.


The Keys and certificates used/generated are stored in a data base called as keystore. By default this database is stored in a file named .keystore.

You can access the contents of this database using the KeyStore class of the java.security package. This manages three different entries namely, PrivateKeyEntry, SecretKeyEntry, TrustedCertificateEntry.

PrivateKeyEntry
SecretKeyEntry
TrustedCertificateEntry

## Storing a Key in keystore
In this section, we will learn how to store a key in a keystore. To store a key in the keystore, follow the steps given below.

### Step 1: Create a KeyStore object
The getInstance() method of the KeyStore class of the java.security package accepts a string value representing the type of the keystore and returns a KeyStore object.

Create an object of the KeyStore class using the getInstance() method as shown below.

//Creating the KeyStore object
KeyStore keyStore = KeyStore.getInstance("JCEKS");

### Step 2: Load the KeyStore object
The load() method of the KeyStore class accepts a FileInputStream object representing the keystore file and a String parameter specifying the password of the KeyStore.

In general, the KeyStore is stored in the file named cacerts, in the location C:/Program Files/Java/jre1.8.0_101/lib/security/ and its default password is changeit, load it using the load() method as shown below.
```java
//Loading the KeyStore object
char[] password = "changeit".toCharArray();
String path = "C:/Program Files/Java/jre1.8.0_101/lib/security/cacerts";
java.io.FileInputStream fis = new FileInputStream(path);
keyStore.load(fis, password);
```

### Step 3: Create the KeyStore.ProtectionParameter object
Instantiate the KeyStore.ProtectionParameter as shown below.

```java
//Creating the KeyStore.ProtectionParameter object
KeyStore.ProtectionParameter protectionParam = new KeyStore.PasswordProtection(password);
```
### Step 4: Create a SecretKey object
Create the SecretKey (interface) object by instantiating its Sub class SecretKeySpec. While instantiating you need to pass password and algorithm as parameters to its constructor as shown below.

```java
//Creating SecretKey object
SecretKey mySecretKey = new SecretKeySpec(new String(keyPassword).getBytes(), "DSA");

```

### Step 5: Create a SecretKeyEntry object
Create an object of the SecretKeyEntry class by passing the SecretKey object created in the above step as shown below.

```java
//Creating SecretKeyEntry object
KeyStore.SecretKeyEntry secretKeyEntry = new KeyStore.SecretKeyEntry(mySecretKey);
```

### Step 6: Set an entry to the KeyStore
The setEntry() method of the KeyStore class accepts a String parameter representing the keystore entry alias, a SecretKeyEntry object, a ProtectionParameter object and, stores the entry under the given alias.

Set the entry to the keystore using the setEntry() method as shown below.

```java
//Set the entry to the keystore
keyStore.setEntry("secretKeyAlias", secretKeyEntry, protectionParam);
```

```java
import java.io.FileInputStream;
import java.security.KeyStore;

import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;

public class StoringIntoKeyStore{
   public static void main(String args[]) throws Exception {
      //Creating the KeyStore object
      KeyStore keyStore = KeyStore.getInstance("JCEKS");

      //Loading the KeyStore object
      char[] password = "changeit".toCharArray();
      String path = "c:\\java\\jre\\lib\\security\\cacerts";
      java.io.FileInputStream fis = new FileInputStream(path);
      keyStore.load(fis, password);
      
      //Creating the KeyStore.ProtectionParameter object
      KeyStore.ProtectionParameter protectionParam = new KeyStore.PasswordProtection(password);

      //Creating SecretKey object
      SecretKey mySecretKey = new SecretKeySpec("myPassword".getBytes(), "DSA");
      
      //Creating SecretKeyEntry object
      KeyStore.SecretKeyEntry secretKeyEntry = new KeyStore.SecretKeyEntry(mySecretKey);
      keyStore.setEntry("secretKeyAlias", secretKeyEntry, protectionParam);

      //Storing the KeyStore object
      java.io.FileOutputStream fos = null;
      fos = new java.io.FileOutputStream("newKeyStoreName");
      keyStore.store(fos, password);
      System.out.println("data stored");
   }
}
```
