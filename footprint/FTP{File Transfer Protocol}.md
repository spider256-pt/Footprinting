#Ftp
ftp sign in procedure

common port 21(for sending) and port 20(establish the connection) over the server.

so ftp is the only know protocol which can handle both.

ftp <target> -p <port number>.

##Anonymous Login ((Dangerous Details))

1. anonymous_enable=YES  | allow anyone to login as anonymous.
2. anon_upload_enable=YES | allow anonymous to upload any files.
3. anon_mkdir_write_enable=YES | allow anonymous to make directory.
4. no_anon_password=YES | no password required to get in.
5. anon_root=/home/username/ftp | the directory for anonymous.
6. write_enable=YES

[[Nmap Basics]]