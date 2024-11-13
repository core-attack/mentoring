## setup different user for git
```
ssh/config:
Host company1
 Hostname github.com
 User git
 IdentityFile ~/.ssh/id_rsa_core-attack
Host company2
 Hostname github.com
 User git
 IdentityFile ~/.ssh/id_rsa2_core-attack
```

## generate with github login
```
ssh-keygen -t ed25519 -C "core-attack@github.com"
ssh-keygen -t rsa -b 4096 -C "pcore-attack@github.com"
```

## add to ssh agent
```
ssh-add c:/Users/nikol/.ssh/id_rsa_core-attack
ssh-add c:/Users/nikol/.ssh/id_ed25519_core-attack
```

## check that ok (compare with github ssh)
```
$ ssh-add -l -E sha256
4096 SHA256:REMZG_KQc core-attack@github.com (RSA)
256 SHA256:0SLy_1kkDg core-attack@github.com (ED25519)
```

## look deeper
```
ssh -vT git@github.com

git remote set-url origin git@github.com:core-attack/mentoring.git

ssh-add c:/Users/nikol/.ssh/id_ed25519

/c/Users/nikol/.ssh/id_rsa_core-attack

ssh-add -l -E ed25519

ssh-add c:/Users/nikol/.ssh/id_rsa_core-attack
ssh-add c:/Users/nikol/.ssh/id_ed25519_core-attack
```
