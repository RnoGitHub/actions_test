# encrypt and decrypt

If you devlop another environment, you may use api-key and api-password.  
These are secrets.

So this section introduces how to encrypt these secret file and use decrypting in GitHub.

## Refer

---
[GNU](https://www.gnupg.org/)
[Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

## Install GNU to Local Machine

Visit [GNU](https://www.gnupg.org/) and install local machine.

``` bash
sudo apt install gnupg
```

## make encrypt file

move your directory and make json file.

``` bash
gpg --symmentic --cipher-algo AES256 <file_full_path>

# enter passphras twice
```

`file_name.gpg` will be created.

```note
�
	�^�ڞ�A���z�g���oD����HA�ޕt�%g����,D�������[a=v��:���i/A��uMJLbqa�|��A��LO�E�)ox[���+�؅�\�e�-ֲ�]��V��u8e> ��U~��}p�
```

it was encrypted.
Next you push file_name.gpg to GitHub.

## Make workflow to decrypt in GitHub

``` yaml
name: encrypt and decrypt

on: [ push ]

jobs:
  decrypt:
    runs-on: ubuntu-20.04
    env :
      PASSPHRASE: ${{ secrets.PASSPHRASE }}
    steps:
      - uses: actions/checkout@v1
      - name: Decrypt file
        run : gpg --quiet --batch --yes --decrypt --passphrase=$PASSPHRASE --output $HOME/secret.json secret.json.gpg

      - name: Print out file content
        run: cat $HOME/secret.json
```

## gpg option

|option|contents|
|---|---|
|--quiet|no log|
|--batch| cmd line operation|
|--yes| several question from gpg but you answer yes|
|--decrypt| decrypt|
|--passphrase=$PASSPHRASE|passphrase is env|
|--output $HOME/secret.json| outptfile path|
|secret.json.gpg| input file|
