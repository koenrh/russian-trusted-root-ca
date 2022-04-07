# Russian Trusted Root CA

Raw files related to the newly introduced Russian national certificate authority.

Read my blog post: [Russia's certificate authority for sanctioned organizations]()

## Certificates

* [`root-ca_rsa-2022.pem`](root-ca_rsa-2022.pem) - Russian Trusted Root CA certificate
* [`sub-ca_rsa-2022.pem`](sub-ca_rsa-2022.pem) - Russian Trusted Sub CA certificate
* [`certificates.tsv`](cerrtificates.tsv) - All issued and identified leaf certificates

## Yandex

Encrypted configuration files can be decrypted as follows.

```bash
cd ./yandex

key=".5I(oR[LGJ7gGr4*Q-Tw90M8VNa6D^io"

# first block is the IV
iv="$(head -c16 ./custom_root_certs.enc)"

# skip the first block and decrypt
tail -c +17 ./custom_root_certs.enc | \
    openssl aes-256-cbc -d -K "$(echo -n $key | xxd -p -c32)" -iv "$(echo -n $iv | xxd -p)" | jq
```
