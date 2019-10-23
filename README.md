# Authentication :key:

#### What is an SSH key?

The Secure Shell (SSH) system can be configured to allow the use of different types of authentication. In this case, by generating a SHH <i>key pair</i>, consisting of a <i>public key</i> and a <i>private key</i>.

###### Private Keys :closed_lock_with_key:

Is kept in your own system, or on the system you're connecting <i>from</i>.

###### Public Keys :unlock:

Is copied to the system you're connecting <i>to</i>.

Generating a key pair on your own system command, which will generate the pair in the .ssh directory (id_rsa and id_rsa.pub):
```
ssh-keygen -t dsa

```

Copy the public key file to the target system, use the following command:
```
scp ~/.ssh/id_rsa.pub user@xx-xx-xxx-xxx-xx.com:~
```

SSH into the target system as normal, and to append the contents of the file (public key) to SSH's authorized_keys file, which contains a list of all public keys that can authenticate to this user account. Use this command:
```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

Exit back to the target system. If this was done correctly, you won't be prompted for a password, as the public-key system will have authenticated you.

If unsuccessful, you may need to log in with a password and then change permission on the authorized_keys file, using the command:
```
chmod 600 ~/.ssh/authorized_keys
```

### Known hosts

Each server has its own public and private key pair, and the public keys of all the servers you've accessed are stored in the file known as known_hosts in your .ssh directory.

When connecting to a server, SSH checks to see if you have the server's public key, if not, it displays a prompt and allows you to verify that you want to connect to that server, and then stores the public key in the known_hosts file if you proceed with that connection.

###### Remedy

For unsuccessful decryption of challenge sent by the server encrypted with that server's private key:

- Edit the known_hosts file and remove the errant public key.

## SCP

Secure Copy Protocol (SCP) is a means of securely transferring computer files between a local host and a remote host or between two remote hosts. 

Copy file from local host to a remote host:
```
$ scp file.txt username@to_host:/remote/directory/
```

Copy directory from local host to a remote host:
```
$ scp -r /local/directory/ username@to_host:/remote/directory/
```
