# A collection of Elliptic Curves for ZkCrypto traits

This library provides efficient and flexible implementations of various halo2-friendly elliptic curves, originally implementing the BN256 curve with traits from the `zkcrypto` ecosystem,

* [`zkcrypto/ff`](https://github.com/zkcrypto/ff)
* [`zkcrypto/group`](https://github.com/zkcrypto/group)
* [`zkcrypto/pairing`](https://github.com/zkcrypto/pairing)

The implementations were originally ported from [matterlabs/pairing](https://github.com/matter-labs/pairing/tree/master/src/bn256) and [zkcrypto/bls12-381](https://github.com/zkcrypto/bls12_381), but have been extended and optimized to cover a broader set of curves and use cases. Since its initial release, the library has expanded to include additional curves, along with the following features:

* `secp256k1`, `secp256r1`, and `grumpkin` curves, enhancing its usability across a range of cryptographic protocols.
* Assembly optimizations leading to significantly improved performance.
* Various features related to serialization and deserialization of curve points and field elements.
* Curve-specific optimizations and benchmarking capabilities.

## Benchmarks

Benchmarking is supported through the use of Rust's built-in test framework. Benchmarks can be run without assembly optimizations:

```
$ cargo test --profile bench test_field -- --nocapture
```

or with assembly optimizations:

```
$ cargo test --profile bench test_field --features asm -- --nocapture
```


## Additional Features

1. **Derivation of Serialize/Deserialize**: The library supports Serde's `Serialize` and `Deserialize` traits for field and group elements, making it easier to integrate curve operations into serialization-dependent workflows.

2. **Hash to Curve**: For the `bn256::G1` and `grumpkin::G1` curves, `hash_to_curve` is implemented, enabling more efficient hash-and-sign signature schemes.

3. **Lookup Table**: A pre-computed lookup table is available for `bn256::Fr`, accelerating conversion from `u16` to montgomery representation.

## Structure

The library's top-level directories are organized as follows:

* `benches`: Contains benchmarking tests.
* `script`: Contains utility scripts.
* `src`: Contains the source code of the library, further subdivided into modules for each supported curve (`bn256`, `grumpkin`, `secp256k1`, `secp256r1`, `pasta`) and additional functionalities (`derive`, `tests`).
