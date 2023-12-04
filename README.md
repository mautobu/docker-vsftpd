# mautobu/vsftpd

### Examples

* test server via command line
```
docker run --rm -e PASSWORD=FSBhuNOR -p 21000:21 -p 20000:20000 mautobu/vsftpd:latest
```

* push file
```
touch test.txt
lftp ftp://files:FSBhuNOR@localhost:21000 -e "set ssl:verify-certificate false; put test.txt; ls; exit"
```

* docker-compose.yaml
```
version: '3.6'

volumes:
  files:

services:

  ftp:
    image: mautobu/vsftpd
    environment:
      - PASSWORD=FSBhuNOR
    ports:
      - '21000:21'
      - '20000:20000'
    volumes:
      #- /path/to/cert.pem:/etc/vsftpd/vsftpd.pem
      - files:/home/files
```

* genereate custom cert
```
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout custom_vsftpd.pem -out custom_vsftpd.pem -subj "/C=RU/O=vsftpd/CN=example.org
```

### References
- https://github.com/delfer/docker-alpine-ftp-server
- https://github.com/JetBrains/phpstorm-docker-images/tree/master/ftps
- https://github.com/loicmathieu/docker-vsftpd
