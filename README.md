# postfix

Postfix SMTP Relay

## run

    docker run --rm -d --name postfix \
    -e RELAY_USER=postmaster@domain \
    -e RELAY_PASS=xxxxxxxxx \
    fametec/postfix:gmail

## docker-compose

    version: '3.2'
    #
    ### Services
    #
    services:
    #
    # MAILGUN
    #
      relay:
        image: fametec/postfix:gmail
        restart: unless-stopped
        volume: 
         - postfix-volume:/var/spool/postfix
        ports:
         - "30025:25"
        environment:
         RELAY_USER: postmaster@XXXXXXXXXXXXXXXX
         RELAY_PASS: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    #
    ### Volumes
    #
    volumes:
      postfix-volume:
      
      

 # testing

    echo "Email Test" | mail -s "This is a simple test" contato@fametec.com.br
 
 
