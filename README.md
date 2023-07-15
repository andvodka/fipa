# Follow IP address

## Usecase.sh

```
#!/bin/sh

API_TOKEN=
ZONE_IDENTIFIER=
RECORD_IDENTIFIER=
RECORD_NAME=

fipa -d 1 -i ppp0 -v 4 | while read a
do
  set -- $a
  if [ $# -gt 0 ]
  then
    curl -X PUT "https://api.cloudflare.com/client/v4/zones/$ZONE_IDENTIFIER/dns_records/$RECORD_IDENTIFIER" \
      -H 'Authorization: Bearer '$API_TOKEN \
      -H 'Content-Type: application/json' \
      -d '{"type":"A","name":"'$RECORD_NAME'","content":"'$1'","proxied":false}'
  fi
done
```
