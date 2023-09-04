# ssh-keygen
- `ssh-keygen` is a command-line utility used to generate SSH (Secure Shell) key pairs, which consist of a public and a private key. SSH keys are used for secure authentication and communication between computers over a network, most commonly used for remote login sessions or transferring files securely.
- Here's a brief overview of the two key types:
  - **Public Key**: This is meant to be shared with other systems or servers that you want to connect to securely. The public key is used by the remote server to verify your identity when you attempt to log in.
  - **Private Key**: This key must be kept secure and never shared with anyone. It acts as your personal authentication token, allowing you to prove your identity to the remote server that holds the corresponding public key.
- When you generate an SSH key pair using `ssh-keygen`, you'll typically get two files:
  - **id_rsa**: This is your private key and should be protected and kept secure on your local machine.
  - **id_rsa.pub**: This is your public key, which can be shared with remote servers.
- To generate an SSH key pair using `ssh-keygen`:
```bash
ssh-keygen -t rsa
```
- This will generate a new RSA key pair. During the process, you can specify the file names for the keys and set an optional passphrase to protect your private key with an additional layer of security.
- Once you have your key pair, you can add the public key (`id_rsa.pub`) to the `~/.ssh/authorized_keys` file on the remote server to enable passwordless SSH login or use it for other SSH-related tasks like setting up Git repositories with secure access.