# Security Algorithms with the Dunder Mifflin Scranton

## Homomorphic Encryption

Homomorphic encryption is a cryptographic technique that allows mathematical operations on data to be performed on cypher text rather than the original data. The cypher text is a version of the input data that has been encrypted (also called plain text). To obtain the desired output, it is operated on and then decrypted. The fundamental condition of homomorphic encryption is that decrypting the operated cypher text should yield the same result as just operating on the starting plain text.

### Properties

Homomorphic encryption is designed to be malleable. Anyone may intercept a cypher text, change it into another cypher text, and then decode it into a plain text that makes sense. In a cryptographic system, malleability is typically seen as bad. Assume you're attempting to transmit the encrypted message "I love you" to a pal. You encrypt it and send it to the recipient. On the route, though, it gets intercepted by a hacker. They only see cypher text, but they can change it to something that decrypts to "I hate you" when your friend attempts to decrypt it. That is why malleability is rarely desired.

Homomorphic systems, on the other hand, should be changeable. Perhaps you'd like to create a system that just adds exclamation points to anything you give your friend. However, you don't want the system to know what you're sending your buddy because it's a private message. Your mail is encrypted and sent to your system. Because your system just sees the encrypted text, it has no idea what you're saying, but it can still change it. It converts the encryption into a text that decrypts to the same input message as before, plus a few exclamation points. As a result, it now appears as follows.

### Applications

In recent years, homomorphic encryption has witnessed a resurgence, owing in part to cloud computing. Many systems outsource their processing to corporations like Amazon or Microsoft and their massive data centres since computing resources are so inexpensive. Those systems, on the other hand, do not wish to expose that data to attack. As a result, they encrypt the data, transfer it to a data centre, where it is processed, and then return it to the original system for decryption.

In today's digital world, privacy is crucial. If private data that is utilised by several systems has to remain encrypted, homomorphic encryption is frequently employed. For example, homomorphic encryption might be used to safeguard vote privacy in e-voting.

E-cash systems may also employ homomorphic encryption. If you're sending money to a friend, you might not want the system to know how much money you're sending. The system may get access to both your and your friend's encrypted data, combine it, and return it to your buddy.

Finally, the bulk of these applications have been concerned with techniques of safeguarding data and communications. On the other hand, homomorphic encryption may be used to protect algorithms and code. In the most likely use case for such a device, both the incoming data and the algorithm that processes it would need to be safeguarded. Because fully homomorphic encryption methods are still a hot research topic, this application might be closer than previously thought.
