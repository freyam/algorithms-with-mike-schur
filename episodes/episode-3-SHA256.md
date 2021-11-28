# Security Algorithms w/ the Dunder Mifflin Scranton

## SHA 256

Secure Hash Algorithms, or SHA, are a group of cryptographic algorithms that are used to keep data secure. It operates by converting data with a hash function, which is a bitwise operations, modular additions, and compression functions-based method. The hash function then generates a fixed-length string that bears no resemblance to the original. These methods are one-way functions, which means that it's very hard to change them back into their original data once they've been transformed into their hash values. SHA-1, SHA-2, and SHA-3 are three algorithms of interest, each of which was built with ever better encryption in response to hacker attempts. Because of its widely known flaws, SHA-0 is currently considered outdated.

SHA-1 and SHA-2 differ in several ways; mainly, SHA-2 produces 224- or 256-sized digests, whereas SHA-1 produces a 160-bit digest; SHA-2 can also have block sizes that contain 1024 bits, or 512 bits, like SHA-1.

### Code

```cpp
#include <stdio.h>
#include <stdlib.h>

char message[] = "freyam";
unsigned long int ml = sizeof(message);

// Initial values of SHA-1 variables
unsigned int h0 = 0x67452301;
unsigned int h1 = 0xEFCDAB89;
unsigned int h2 = 0x98BADCFE;
unsigned int h3 = 0x10325476;
unsigned int h4 = 0xC3D2E1F0;

int *oneChunkCreator() {
    int *ptr = (int *)calloc(80, sizeof(int));
    return ptr;
}

int *chunkInitializer() {
    int *chunk = oneChunkCreator();
    int i = 0;

    for (int i = 0; i < 14; ++i) {
        for (int j = 0; j < 4; ++j) {
            int c = i * 4 + j;
            if (c < ml) {
                chunk[i] = chunk[i] | (message[c] << (24 - 8 * j));
            } else if (c == ml) {
                chunk[i] = chunk[i] | (0x80 << (24 - 8 * j));
            } else {
                chunk[i] = chunk[i] | (0x00 << (24 - 8 * j));
            }
        }
    }
    chunk[15] = ml * 8;
    return chunk;
}

int rightCircularShift(int x, int n) {
    return (x >> n) | (x << (32 - n));
}

int leftCircularShift(int x, int n) {
    return (x << n) | (x >> (32 - n));
}

void preProcessChunk(int *chunk) {
    for (int i = 16; i < 80; i++) {
        chunk[i] = leftCircularShift((chunk[i - 3] ^ chunk[i - 8] ^ chunk[i - 14] ^ chunk[i - 16]), 1);
    }
}

void helper_SHA256(int *chunk) {
    unsigned int a = h0;
    unsigned int b = h1;
    unsigned int c = h2;
    unsigned int d = h3;
    unsigned int e = h4;

    for (int i = 0; i < 80; i++) {
        unsigned int f;
        unsigned int k;
        if (i < 20) {
            f = (b & c) | ((~b) & d);
            k = 0x5A827999;
        } else if (i < 40) {
            f = b ^ c ^ d;
            k = 0x6ED9EBA1;
        } else if (i < 60) {
            f = (b & c) | (b & d) | (c & d);
            k = 0x8F1BBCDC;
        } else {
            f = b ^ c ^ d;
            k = 0xCA62C1D6;
        }
        unsigned int temp = leftCircularShift(a, 5) + f + e + k + chunk[i];
        e = d;
        d = c;
        c = leftCircularShift(b, 30);
        b = a;
        a = temp;
    }

    h0 += a;
    h1 += b;
    h2 += c;
    h3 += d;
    h4 += e;
}

int *hashValue() {
    int *hash = (int *)calloc(5, sizeof(int));
    hash[0] = h0;
    hash[1] = h1;
    hash[2] = h2;
    hash[3] = h3;
    hash[4] = h4;
    return hash;
}

void printHash(int *hash) {
    printf("%08X%08X%08X%08X%08X\n", hash[0], hash[1], hash[2], hash[3], hash[4]);
}

int *SHA1() {
    int *chunk = chunkInitializer();
    preProcessChunk(chunk);
    helper_SHA256(chunk);
    free(chunk);
    int *hash = hashValue();
    printHash(hash);
    return hash;
}

int main() {
    int *hash = SHA1();
    free(hash);
    return 0;
}
```

### References

1. https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Hash_function.svg/2000px-Hash_function.svg.png
2. http://blog.tanyakhovanova.com/2010/11/one-way-functions/
