# SSH

## Alte Software

- rlogin
- rsh
- rcp
- rexec
- telnet

## Softwarepaket

- OpenSSH
- Serverbasiert
- Standardport 22
- Geöffneter Port

## Möglichkeiten

- Remote Login
- Dateiübertragung
- Porttunnel
- X11-Tunnel
- sshfs
- git

## Verschlüsselung

- ECDSA (Elliptic Curve DSA)
- ECDH (Elliptic Curve Diffie-Hellman)
- ED25519
- DSA
- RSA

## Login

- Unix-/Linux-User-Account
- Standard-Login-Shell -> /etc/passwd -

## Porttunnel

- Lokal: ssh -L \

  <ziel auf="" localhost\="">:\<locale adresse\="">:\<remote-port\>
  </remote-port\></locale></ziel>

- Remote: ssh -R

- Dynamic ssh -D

- Kompression: ssh -C

## Struktur

### Motivation

Warum sollte ssh benutzt werden?

- sichere Fernwartung
- besser als telnet, da vereschlüsselt
- Alternative zu rsh, rcp, rlogin, rexec

### Geschichte

- 1995: proprietäres Projekt [SSH Communications Security Corp.] (SSH-1) -> sicherheitsmängel
- 1996: zweite Version (SSH-2) [1996] -> inkompatibel zu SSH-1
- 1999: Abspaltung der Open Source Variante (OpenSSH)
- 2005: neue Version (SSH G3) proprietär
- 2006: IETF RFC 4250 und andere -> siehe Man-Page

### Einfürhrung und erstes Beispiel

- ssh -p 22 user@server mit Password
- (ssh server mit Key)

### Software(pakete)

- openssh auf den meisten Linux-Distributionen vorinstalliert
- auch teil von Proprietären Unixoiden (HP)
- alle BSDs
- auch auf Mac (auch sshd)
- putty für Windows (nicht nur ssh)

### SFTP und SCP und SSHFS

- scp Beispiel (statt rcp)
- sftp Ausführen (statt ftp)
- sshfs Beispiel (statt anderer Freigabe ohne Verschlüsselung)

### SFTP

- Benutzung wie ein FTP-client (nur in verschlüsselt)
- put, get, cd, ls, etc.
- als Dateibrowsererweiterung
- FileZilla (Windows, Mac OS X)

### SCP

- benutzung wie cp nur mit zusätzlichen Host
- scp user@host:/dir/file user2@host2:/dir/file
- oder eine lokale Datei

### SSHFS

- einbinden eines Ordners als Dateisystem über eine ssh Verbindung
- sshfs -o reconnect,ServerAliveInterval=15,ServerAliveCountMax=3 nas:/ ~innay/nasfs
- reconnect: verbindet sich nach einer Verbindungsunterbrechung wieder
- ServerAliveInterval: Zeit bis ein Aufrechterhaltungspaket gesendet wird
- ServerAliveCountMax: Zahl der verloren Pakete

### remote execution

- normaler ssh-Befehl mit zusätzlichem Parameter für auszuführenden Programm
- ssh -X Desktop-Anwendungen
- Performance -> X2GO

### Porttunnel

- ssh -L **BindAdresse**:_BindPort_:**ZielAdresse**:_ZielPort_ **jumpServer** auf dem lokalen Rechner wird der Port und die Adresse gebunden

- ssh -R **BindAdresse**:_BindPort_:**ZielAdresse**:_ZielPort_ **jumpServer** auf dem entfernten Rechner wird die Addresse und der Port gebunden

- ssh -D 22222 server -> SOCKS5 Proxy

- ssh -N ohne ein Command auszuführen

### Der Server

- /etc/ssh/sshd_config
- Standardport 22
- Root Login -

### SSH Key-generation

- ssh-keygen
- t: Typ
- E: Hash-Typ
- ssh-keygen
  - l: Fingerprint
  - f: Datei 


- ssh-keyscan

### Zusammenfassung

- weite Verbreitung
- scp, sftp, sshfs
- remote-execution (mit und ohne X forwarding)
- Porttunnel
- der Server
