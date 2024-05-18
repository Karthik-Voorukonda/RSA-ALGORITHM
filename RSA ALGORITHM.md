import java.math.BigInteger; import java.util.Random; import
java.util.Scanner;

public class RSA {

public static void main(String\[\] args) { Scanner scanner = new
Scanner(System.in);

// Step 1: Generate keys System.out.println(\"RSA Key Generation:\");
BigInteger p = generateLargePrime(); BigInteger q =
generateLargePrime();

BigInteger n = p.multiply(q); // modulus BigInteger phi =
p.subtract(BigInteger.ONE).multiply(q.subtract(BigInteger.ONE)); //
Euler\'s totient function

BigInteger e = BigInteger.valueOf(65537); // Common public exponent
value

// Calculate private key (d) BigInteger d = calculatePrivateKey(e, phi);

// Step 2: Encryption System.out.println(\"\\nEncryption:\");
scanner.nextLine(); // Consume newline System.out.print(\"Enter the
plaintext: \"); String plaintext = scanner.nextLine(); BigInteger
plaintextNum = new BigInteger(plaintext.getBytes()); BigInteger
ciphertext = encrypt(plaintextNum, e, n);
System.out.println(\"Ciphertext: \" + ciphertext);

// Step 3: Decryption System.out.println(\"\\nDecryption:\");
System.out.println(\"Private key (d) is automatically calculated: \" +
d); System.out.print(\"Enter the ciphertext: \"); BigInteger
encryptedMessage = scanner.nextBigInteger(); BigInteger
decryptedMessageNum = decrypt(encryptedMessage, d, n); String
decryptedMessage = new String(decryptedMessageNum.toByteArray());
System.out.println(\"Decrypted Message: \" + decryptedMessage); }

// Generate a large prime number public static BigInteger
generateLargePrime() { Random rnd = new Random(); return
BigInteger.probablePrime(1024, rnd); }

// Encryption function public static BigInteger encrypt(BigInteger
plaintext, BigInteger e, BigInteger n) { return plaintext.modPow(e, n);
}

// Decryption function public static BigInteger decrypt(BigInteger
ciphertext, BigInteger d, BigInteger n) { return ciphertext.modPow(d,
n); }

// Calculate private key (d) using public exponent (e) and Euler\'s
totient (phi) public static BigInteger calculatePrivateKey(BigInteger e,
BigInteger phi) { return e.modInverse(phi); } }
