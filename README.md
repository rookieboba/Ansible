## CentOS 7 패키지 설치

```bash
sudo yum install http://vault.centos.org/7.9.2009/extras/x86_64/Packages/epel-release-7-11.noarch.rpm
sudo yum install https://repo.ius.io/ius-release-el7.rpm
sudo yum install ansible
```

---

## Ansible 버전 확인

```bash
ansible --version
```

---

SSH Key 생성

Controller 서버에서 SSH Key 생성

```bash
[root@master1 ~] #ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:jl0fHfafU/aMOkZfYpmDKKqzOgqyeNy85PS9WMQZp00 root@master1
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|        . E   o  |
|       . B   o o |
|        S o....o+|
|       =....o.*+*|
|o. oo ..+. ..o.*+|
|+.+++..+    o.. .|
|+o.o==o o. ...   |
+----[SHA256]-----+

```

생성된 Key 를 원격 서버에 복사

`$ ssh-copy-id [원격서버계정ID]@[원격서버IP]`

```bash
[root@master1 ~]# ssh-copy-id root@worker1
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@worker1's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@worker1'"
and check to make sure that only the key(s) you wanted were added.

```

## 인벤토리 설정

### Ansible Inventory 파일 수정
```bash
vi /etc/ansible/hosts
--- 가장 하단에 아래 내용 추가
[worker]       #그룹 만들기 
192.168.98.111  # 연결할 IP 추가
192.168.98.112
192.168.98.113
```

나머지 notion 링크:
https://rookieboba.notion.site/Ansible-4c6a3ea220ef4c01bddcd2bb4a9c7202
