# postfix

Postfix SMTP Relay

## run

    docker run --rm -d --name postfix \
    -e RELAY_USER=apikey \
    -e RELAY_PASS=xxxxxxxxx \
    fametec/postfix:sendgrid

## docker-compose

    version: '3.2'
    services:
      relay:
        image: fametec/postfix:sendgrid
        restart: unless-stopped
        volume: 
         - postfix-volume:/var/spool/postfix
        ports:
         - "30025:25"
        environment:
         RELAY_USER: apikey
         RELAY_PASS: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    volumes:
      postfix-volume:
      
      

 # testing

    echo "Email Test" | mail -s "This is a simple test" contato@fametec.com.br
 
 
