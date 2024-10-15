# Docker Compose uitvoeren

Je hoeft (voorlopig) niks aan te passen.

Start docker compose van uit deze folder op.

```
docker compose up --build
```

Deze app heeft meerdere containers, daar zal je nu de logs van zien.
1 daarvan is een nginx reverse proxy, hiermee gaan we de app een hostname geven: `node-app.local`.

Om dit te laten werken moet je het volgende doen:

### MacOS
```
sudo vi /etc/hosts
```
_vim is niet noodzakelijk, sudo is hier het voornaamste, als je niet gewend bent van met vim te werken, vraag hulp_


Voeg het volgende toe
```
127.0.0.1 node-app.local
```
Sla op.

### Windows
Open jouw favoriete texteditor als adminstrator.

Open `c:\windows\system32\drivers\etc\hosts.file`

Voeg deze lijn
```
127.0.0.1 node-app.local
```
Sla op

----
Als je dit hebt gedaan, surf je naar [http://node-app.local](http://node-app.local)
Refresh de pagina en aantal keren om de counter te zien stijgen.

## Docker compose watch
Om lokaal development toe te laten hebben moeten we docker compose jouw lokal folder laten watchen. 

Stop de huidige run met `CTRL+C`

Start opnieuw op met:
```
docker compose watch
```

Surf naar [http://node-app.local](http://node-app.local)

Pas vervolgens in app.py de "Hello World" tekst aan. Sla op.
De container zal nu herstarten, dit is noodzakelijk omwille van Flask.

Soms kan het zijn dat een simpele sync voldoende is (bijvoorbeeld bij een gewone HTML pagina).

Refresh [http://node-app.local](http://node-app.local), je zal nu je aangepaste tekst zien.

Sluit af met `CTRL + C`

## Clean up

```
docker rm docker-compose-app-1 docker-compose-redis-1 docker-compose-nginx-proxy-1
```
