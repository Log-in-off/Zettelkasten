create key
```bash
ssh-keygen -t ed25519 -f ~/.ssh/key_file -C "comment"
```

## .ssh/authorized_keys
`~/.ssh/authorized_keys` - is file, that contains public keys of host, which can have access without password.

How to add new
```bash
cat key_file.pub > `~/.ssh/authorized_keys` #do on target host
#or
ssh-copy-id -i ~/.ssh/key_file.pub -p target_host_port target_host_user@target_host_ip
```

## .ssh/config
`~/.ssh/config` - is file for a quick access to hosts

```
Host target
	HostName target_host_ip
	Port target_host_port
	User target_host_user
	StrictHostKeyChecking no	
	IdentityFile ~/.ssh/key_file

Host target2_without_key
	HostName target2_host_ip
	User target2_host_user

```

access before
```ssh
ssh user@ip -p number
```
quick access after
```bash
ssh target
```

## ssh-add
__ssh-add__ adds new ssh key.
```bash
ssh-add -l #show list added keys

ssh-add  ~/.ssh/some_key
```

I don't know why, but you also have to run ssh-agent previously (in advance)
```bash
eval "$(ssh-agent -s)" > /dev/null
```