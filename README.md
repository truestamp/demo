# Truestamp

## About Us

Truestamp, formed in San Francisco, CA, now operating from Ashburn, VA, provides
a SaaS platform for anyone to independently claim, and verify, the integrity,
timestamp, and provenance of their most important data. By submitting privacy
preserving hashes, and provenance info, to our API, we create cryptographic
Commitments immutably linking their data to the Stellar blockchain. We do this
efficiently, at enterprise scale, storing at most a single photo's worth of
on-chain data per year.

## Learn More

Watch our [intro video](https://scf11.truestamp.com/video) or visit our [website](https://www.truestamp.com) to learn more.

## The Demo

This repository contains the same [content](content) used to create the demo material below. You should feel free to clone this repo if you want to try out the verification URL, and the drag-and-drop file verification for yourself.

https://staging-verify.truestamp.com/truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC

### Get the hash of the files you want to submit

#### Using `sha256sum`

Most operating systems and programming languages include hashing tools that are installed by default. Here are two that you can try on your system. If you have both available, you'll see that they both generate the same hash values.

```sh
❯ cd content/

❯ sha256sum sdf-logo.png
9ebdddcbd756efac1d9a70d8f3ea2239e7b538a55ce847b92fc3eb245a1183f2  sdf-logo.png

❯ sha256sum science.md
284b8b69bfd6cb6d673e399fa28e83a1383ef591e7c2d484be9368f1d3d0fc0a  science.md
```

#### Using `openssl`

```sh
❯ cd content/

❯ cat sdf-logo.png | openssl sha256
9ebdddcbd756efac1d9a70d8f3ea2239e7b538a55ce847b92fc3eb245a1183f2

❯ cat science.md | openssl sha256
284b8b69bfd6cb6d673e399fa28e83a1383ef591e7c2d484be9368f1d3d0fc0a
```

### Submit an Item to Truestamp

There are several different ways to submit an Item to Truestamp as a customer. The easiest way is to drag-and-drop a file or folder in our web UI, and click the create item button.

https://user-images.githubusercontent.com/117/192169019-02905e65-f4ae-46f7-aa61-9ec7ad7a08cd.mov

Alternatively, you can use the CLI to submit an Item. The simplest Item represents only a single hash. By submitting a JSON file you can send both structured and unstructured metadata. See the sample [item.json](item.json) file in this repo. You'll see it contains the hashes of our test files.

```sh
❯ cat ./item.json | truestamp items create --input json --stdin
truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC
```

That command returned an ID that we can use, or share, to retrieve or verify a Commitment.

```txt
truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC
```

### Save the Commitment

Optionally, you can use the ID returned to download your Commitment to store alongside a pristine copy of your hashed files.

Here is the [commitment.json](commitment.json) file for this Item. The commitment is what provides the cryptographic proof that your data is included in the Merkle root stored in a blockchain transaction.

### Verify the Item We Submitted

No matter which verification tool you use, the process is the same. It will cryptographically verify that the entirety of the Item data you submitted, including hashes and other metadata, is cryptographically bound via Merkle trees to the transactions listed in the Commitment. This verification irrefutably proves that you content is bound to that transaction. The timestamp, as recorded in the ledger, proves that your Item was submitted prior to that time. At no time is any data in the Commitment trusted without calculating its hashes, and reaching out to the public API's of transaction ledgers for confirmation of Merkle roots and timestamp.

#### Using the Web UI

Anyone can view the verification results for a Commitment using the Truestamp verification web page as long as they have the ID. Here's the link to the ID we created above. You'll notice that there is quite a bit of information that is provably associated with this Commitment.

Please note, this is a test ID, and it will no longer work once Stellar does its quarterly test environment reset.

https://user-images.githubusercontent.com/117/192169657-c114d51c-64a5-44c8-bbed-4cf949b87d26.mov

You can try it out yourself at this verification URL:

[https://staging-verify.truestamp.com/truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC](https://staging-verify.truestamp.com/truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC)

#### Using the CLI

Another way to verify a Commitment is to use the Truestamp CLI. Here we're verifying the same ID as above.

```sh
❯ truestamp commitments verify --id truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC
Verification Results

  Verified?               Yes
  Verify URL              https://staging-verify.truestamp.com/2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC
  ID                      truestamp-2SF5MvJNqaNJZKQoPSjeeD7RjWDyeTdAUQwSspscj6uyYs9owGZuaXJhUPBtC
  Submitted After         2022-09-25T21:15:27.250Z
  Submitted At            2022-09-25T21:18:44.220Z
  Submitted Before        2022-09-25T21:20:09Z
  Submitted Window (ms)   281750
  Observable Entropy Hash e0673ac46df86b967b864e11eed6927ffb358ae7c529d9a2d0e34eaf87cf29bc
  Hashes                  284b8b69bfd6cb6d673e399fa28e83a1383ef591e7c2d484be9368f1d3d0fc0a [sha-256]
                          9ebdddcbd756efac1d9a70d8f3ea2239e7b538a55ce847b92fc3eb245a1183f2 [sha-256]
```

## Thank You

Thanks for exploring this quick demo. If you have any questions please let us know.

Glenn Rempe
Founder & CEO
Truestamp Inc.
support@truestamp.com
