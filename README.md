# postfix

Postfix SMTP Relay

## run

    docker run --rm -d --name postfix \
    -e RELAY_USER=postmaster@domain \
    -e RELAY_PASS=xxxxxxxxx \
    -e RELAY_HOST=email-smtp.us-west-2.amazonaws.com \
    fametec/postfix:ses

## docker-compose

    version: '3.2'
    services:
      relay:
        image: fametec/postfix:ses
        restart: unless-stopped
        volume: 
         - postfix-volume:/var/spool/postfix
        ports:
         - "30025:25"
        environment:
         RELAY_USER: postmaster@XXXXXXXXXXXXXXXX
         RELAY_PASS: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
         RELAY_HOST: email-smtp.us-west-2.amazonaws.com
    volumes:
      postfix-volume:
      
      

 # testing

    echo "Email Test" | mail -s "This is a simple test" contato@fametec.com.br
 
 
