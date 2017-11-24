# docs/ssh-keygen/generating-a-new-ssh-keypair.md

## Create a very strong pass phrase.

Before generating a keypair you will want to select an excellent passphrase. Diceware is a great way to generate an excellent pass phrase.

## Generating an SSH keypair.

* Open the terminal application
* Paste the following text substituting your own email address or an appropriate comment as the comment:

Example of generating an SSH keypair for a human user:

```shell
ssh-keygen -t rsa -b 4096 -C "sandra@gmail.com"
```

Example of generating an SSH Keypair for a non-human user account with no associated email address:

```shell
ssh-keygen -t rsa -b 4096 -C "deployment user"
```

Example generating a keypair with a custom file name:

```shell
ssh-keygen -f ~/.ssh/id_rsa_deployment_user -t rsa -b 4096 -C "deployment user"
```

