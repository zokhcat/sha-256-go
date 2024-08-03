An attempt to implement SHA-256 from scratch using golang and do low-level programming.

Algorithm:

- Intialization of Hash Values(H0-H7) and the constants (K0-K63)
- Padding to ensure the message is near a 512 bits multiple.
  -- workflow of padding:
  1. add one "1" after converting the message to binary
  2. add "0"s till it satisfies _448(bits) mod 512(bits)_. In layman terms, there must be 64 bits space left after adding "0"s in the nearest 512 mulitple.
  3. In the end appending the 64-bit representation to the message we received.
- Parsing the message by sptlitting it into 512-bit blocks. W[0]-W[63]
- Scheduling the message:
  -- workflow of scheduling:
  1. W[0]-W[15] are extracted directly.
  2. Rest(W[16] - W[63]) are generated using this formula below:
     ![Scheduling Formula](https://i.postimg.cc/xd2772bJ/Untitled-2024-06-30-1457.png)
- Compression Function
  -- workflow of compression:

  1. Intialize a,b...h as the first H0-H7 values respectively
  2. For each 64 rounds, following manipulations are done:
     ![Compression](https://i.postimg.cc/YCv3ryQr/Untitled-2024-06-30-1457-1.png)
     where:
     ![helper Functions](https://i.postimg.cc/Bvg0BgnK/Untitled-2024-06-30-1457-3.png)

- Updating Hash after every 512-bit round:
  ![Updating hash](https://i.postimg.cc/qMQrVQTM/Untitled-2024-06-30-1457-4.png)

- Finally, Cocatenate the hash values to get the final 256-bit hash.
