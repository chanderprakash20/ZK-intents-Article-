# Zero-Knowledge Proofs (ZKPs): Ensuring Data Privacy

Zero-knowledge proofs (ZKPs) are cryptographic techniques that allow one party to prove the truth of a statement to another party without revealing any additional information beyond the statement's validity. They ensure privacy and security in digital interactions by preventing the leakage of sensitive data. ZKPs are widely used in applications like cryptocurrencies to enhance transaction privacy and in authentication systems to verify identity without exposing credentials. This powerful concept is revolutionizing privacy-preserving technologies across various fields.

## A Story: Lucas and Emma

In the town of Bakersville, the best baker, Lucas, had a secret recipe for a delicious pie. His apprentice, Emma, claimed she had learned the recipe. Lucas wanted proof without Emma revealing the recipe itself.

Emma baked a pie using the secret recipe and brought it to Lucas. He tasted it and confirmed it was indeed his special pie. Emma had proven she knew the secret recipe without disclosing the ingredients or steps, showcasing the essence of Zero-Knowledge Proofs.

## Types of Zero-Knowledge Proofs

Zero-knowledge proofs come in several types, each offering unique features and trade-offs:

- **Interactive Zero-Knowledge Proofs**: Require multiple rounds of communication between the prover and verifier, making them dynamic but less practical for some applications.

- **Non-Interactive Zero-Knowledge Proofs (NIZK)**: Eliminate the need for interaction, allowing a single proof to be verified multiple times, which is ideal for blockchain applications.

- **Succinct Non-Interactive Arguments of Knowledge (SNARKs)**: Provide short, easily verifiable proofs.

- **STARKs**: Offer similar benefits to SNARKs but rely on different cryptographic assumptions, emphasizing transparency and scalability.

Each type serves distinct use cases in enhancing security and privacy.

## A Simple Proof

Let's start simple and try to prove something without worrying about zero-knowledge, non-interactivity, its form, and applicability.

### Example: Proving All Bits are Set to 1

Imagine that we have an array of bits of length 10, and we want to prove to a verifier (e.g., a program) that all those bits are set to 1.

![Bits Array](assets/img5.jpg "Bits Array")

The verifier can only check (i.e., read) one element at a time. To verify the statement, one can proceed by reading elements in some arbitrary order and checking if they are truly equal to 1. If so, the confidence in that statement is 10% after the first check, or the statement is invalidated altogether if the bit equals 0. A verifier must proceed to the next round until they reach sufficient confidence. In some cases, one may trust a prover and require only 50% confidence, which means that 5 checks must be executed. In other cases, where 95% confidence is needed, all cells must be checked. The downside of such a proving protocol is that the number of checks is proportionate to the number of elements, which is impractical for arrays of millions of elements.

### Using Polynomials

Polynomials can be visualized as a curve on a graph, shaped by a mathematical equation:

![Polynomial Curve](assets/img1.jpg "Polynomial Curve")

The above curve corresponds to the polynomial: \(f(x) = x³ – 6x² + 11x – 6\). The degree of a polynomial is determined by its greatest exponent of \(x\), which in this case is 3.

Polynomials have an advantageous property: if we have two non-equal polynomials of degree at most \(d\), they can intersect at no more than \(d\) points. For example, let's modify the original polynomial slightly to \(x³ – 6x² + 10x – 5\) and visualize it in green:

![Modified Polynomial Curve](assets/img2.jpg "Modified Polynomial Curve")

This tiny change produces a dramatically different result. It is impossible to find two non-equal polynomials that share a consecutive chunk of a curve (excluding a single point chunk case).

To find intersections of two polynomials, we equate them. For example, to find where a polynomial crosses the x-axis (i.e., \(f(x) = 0\)), we equate \(x³ – 6x² + 11x – 6 = 0\). The solutions to such an equation will be those shared points: \(x = 1\), \(x = 2\), and \(x = 3\). You can clearly see that this is true on the previous graph, where the blue curve crosses the x-axis line.

Likewise, we can equate our original and modified version of polynomials to find their intersections:

![Intersection of Polynomials](assets/img4.jpg "Intersection of Polynomials")

The resulting polynomial is of degree 1 with an obvious solution \(x = 1\), hence only one intersection:

![Single Intersection](assets/img3.jpg "Single Intersection")

The result of any such equation for arbitrary degree \(d\) polynomials is always another polynomial of degree at most \(d\), since there is no multiplication to produce higher degrees. Example: \(5x³ + 7x² – x + 2 = 3x³ – x² + 2x – 5\), which simplifies to \(2x³ + 8x² – 3x + 7 = 0\). The Fundamental Theorem of Algebra tells us that a degree \(d\) polynomial can have at most \(d\) solutions (more on this in following parts), and therefore at most \(d\) shared points.

Thus, evaluating any polynomial at an arbitrary point is akin to representing its unique identity. Let us evaluate our example polynomials at \(x = 10\).

![Polynomial Evaluation](assets/img6.jpg "Polynomial Evaluation")

Out of all choices of \(x\) to evaluate, only at most 3 choices will have equal evaluations in those polynomials, and all others will differ.

#### Verification Protocol

If a prover claims to know some polynomial (no matter how large its degree is) that the verifier also knows, they can follow a simple protocol:

1. The verifier chooses a random value for \(x\) and evaluates the polynomial locally.
2. The verifier gives \(x\) to the prover and asks them to evaluate the polynomial in question.
3. The prover evaluates their polynomial at \(x\) and gives the result to the verifier.
4. The verifier checks if the local result equals the prover’s result. If so, the statement is proven with high confidence.

If we consider an integer range of \(x\) from 1 to \(10^{77}\), the number of points where evaluations are different is \(10^{77} – d\). The probability that \(x\) accidentally “hits” any of the \(d\) shared points is negligible:

![Probability Formula](assets/img7.jpg "Probability Formula")

Note: The new protocol requires only one round and gives overwhelming confidence (almost 100% assuming \(d\) is sufficiently smaller than the upper bound of the range) in the statement compared to the inefficient bit check protocol. This is why polynomials are at the core of zk-SNARK, although other proof mediums may also exist.

## Use of Zero Knowledge in Blockchain

Zero-knowledge proofs (ZKPs) are pivotal in enhancing privacy and security in blockchain technology. They enable users to verify transactions without revealing sensitive information, thus maintaining confidentiality while ensuring data integrity. In cryptocurrencies like Zcash, ZKPs allow transactions to be verified without disclosing the sender, receiver, or transaction amounts, ensuring privacy without compromising the trustless nature of blockchain systems. ZKPs also facilitate private smart contracts, enabling complex computations on blockchains while keeping inputs and outputs private. These capabilities make ZKPs essential for developing secure, privacy-preserving blockchain applications.

## Definition of zk-Rollups

zk-Rollups are a layer 2 scaling solution for blockchains that bundle multiple transactions into a single proof, known as a zero-knowledge proof, which is then submitted to the main blockchain. This reduces the amount of data that needs to be processed on-chain, improving transaction throughput and reducing costs while maintaining security and privacy.

### The Analogy Behind zk-Rollups

Think of zk-Rollups like compressing multiple documents into a single zip file. You send the zip file instead of individual documents, saving space and making the process more efficient, but the recipient can still verify the contents without extracting them.

#### Example: Theme Park Tickets

Imagine you are at a theme park with a group of friends. Instead of each person showing their ticket individually at every ride, you gather all the tickets and create a single list of names that the park staff can quickly verify once. This way, everyone gets on the rides faster, saving time for both the staff and your group, without compromising on security checks. Similarly, zk-Rollups bundle multiple blockchain transactions into one proof, speeding up the verification process and reducing the workload on the main blockchain.

## The Future of Zero-Knowledge Proofs in Blockchain

Zero-knowledge proofs (ZKPs) are increasingly becoming integral to blockchain technology, offering solutions to key privacy and scalability challenges. Current usage of ZKPs in blockchain primarily focuses on enhancing transaction privacy and enabling private smart contracts. Cryptocurrencies like Zcash and Monero utilize ZKPs to allow transactions without revealing details about the sender, receiver, or transaction amount, thereby addressing privacy concerns inherent in public blockchains. Additionally, ZKPs are used in layer 2 scaling solutions, such as zk-Rollups, which improve scalability by bundling multiple transactions into a single proof that is verified on the main blockchain, reducing data processing loads.

Despite these advantages, there are challenges in the widespread adoption of ZKPs in blockchain systems. The complexity of ZKP algorithms leads to significant computational requirements, potentially affecting transaction speeds and increasing costs. Additionally, many ZKP protocols, like SNARKs, require a trusted setup, which poses a security risk if not managed correctly. Another concern is the cryptographic assumptions underlying ZKPs, which could be vulnerable to advances in cryptanalysis or quantum computing.

### Future Outlook

The future outlook for ZKPs in blockchain is promising, as ongoing research aims to address these challenges. Innovations such as STARKs, which eliminate the need for a trusted setup, and advancements in cryptographic techniques aim to enhance both security and efficiency. As the technology matures, ZKPs are expected to play a crucial role in enabling secure and scalable blockchain applications, fostering wider adoption across industries. The development of more efficient ZKP protocols and increased integration into blockchain ecosystems will likely drive the evolution of decentralized systems, balancing privacy, security, and performance.

## Example dApp Using Zero Knowledge Proof

You can explore an example decentralized application (dApp) using zero-knowledge proof:

[GitHub Repository: zk_example_dapp](https://github.com/ytham/zk_example_dapp)

## References

1. [Writing a Zero-Knowledge DApp](https://medium.com/@yujiangtham/writing-a-zero-knowledge-dapp-fd7f936e2d43)
2. [Zero-Knowledge Proofs: Survey of Practical Applications](https://arxiv.org/abs/1906.07221)
