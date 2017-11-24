# adding-ssh-keys-using-ssh-agent.md

## Description

ssh-agent is a program to hold private keys used for public key authentication (RSA, DSA, ECDSA, Ed25519). ssh-agent 
can be located using environment variables and automatically used for authentication when logging in to other machines using ssh.

Keys are added to the ssh-agent using ssh-add. Multiple identities may be stored in ssh-agent concurrently and ssh will automatically use them if present. ssh-add is also used to remove keys from ssh-agent and to query the keys that are held in ssh-agent.

## Adding an SSH key to the ssh-agent

### Ensure that ssh-agent is running

#### Check to see if ssh-agent is already running

```shell
sudo ps -ef | grep agent
```

#### Starting ssh-agent

If ssh-agent is not running you can start it with something like the following:

```shell
eval "$(/usr/bin/ssh-agent -s)"
```

Running the command above will return the PID of the ssh-agent and set up some environment variables.

Output example:

```shell
    Agent pid 59566
```

Environment variables that the above command creates:

```shell
SSH_AUTH_SOCK=/tmp/ssh-XgZbOtiJmp9q/agent.7210; export SSH_AUTH_SOCK;
SSH_AGENT_PID=7211; export SSH_AGENT_PID;
```

## Adding your SSH private key to the ssh-agent using ssh-add.

```shell
/usr/bin/ssh-add ~/.ssh/id_rsa
```

