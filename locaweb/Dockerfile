FROM alpine:3.11.5

MAINTAINER eduardo@fametec.com.br

ENV RELAY_USER postmaster@xxxxxxxxxxxxxxxxxxx

ENV RELAY_PASS xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

ENV RELAY_HOST smtplw.com.br

RUN apk update \
	&& apk upgrade \
	&& apk add --no-cache ca-certificates \
	&& apk add --no-cache postfix cyrus-sasl-plain mailx

RUN { \
      	echo ; \
	echo 'maillog_file = /dev/stdout' ; \
      	echo 'inet_interfaces = all' ; \
	echo 'smtpd_recipient_restrictions = permit_mynetworks' ; \
	echo 'mynetworks = 0.0.0.0/0' ; \
      	echo '#Set the relayhost' ; \
      	echo 'mydestination = localhost.localdomain, localhost' ; \
      	echo 'relayhost = [RELAY_HOST]:587' ; \
      	echo 'smtp_sasl_auth_enable = yes' ; \
      	echo 'smtp_sasl_password_maps = static:RELAY_USER:RELAY_PASS' ; \
      	echo 'smtp_sasl_security_options = noanonymous' ; \
      	echo ; \
      	echo '# TLS support' ; \
      	echo 'smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt' ; \
      	echo 'smtp_tls_security_level = may' ; \
      	echo 'smtpd_tls_security_level = may' ; \
      	echo 'smtp_tls_note_starttls_offer = yes' ; \
      	echo ; \
      	echo 'smtp_cname_overrides_servername=no' ; \
      	echo ; \
    } >> /etc/postfix/main.cf


RUN { \
        echo '#!/bin/sh' ; \
        echo ; \
        echo 'sed -i s/RELAY_USER/$RELAY_USER/g /etc/postfix/main.cf' ; \
        echo 'sed -i s/RELAY_PASS/$RELAY_PASS/g /etc/postfix/main.cf' ; \
        echo 'sed -i s/RELAY_HOST/$RELAY_HOST/g /etc/postfix/main.cf' ; \
        echo 'postfix start-fg' ; \
        echo ; \
   } > /entrypoint.sh && chmod +x /entrypoint.sh

VOLUME /var/spool/postfix

EXPOSE 25

CMD [ "/entrypoint.sh" ]
