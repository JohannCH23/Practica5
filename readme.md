<h3> #Practica 5 - Johan Erazo </h3>

<h2>Configura un contenedor coa imaxe oficial de bind9 usando docker-compose.</h2>

Ao configurar un contedor con imaxe de **bind**, imos á carpeta **composetest** que foi creada anteriormente na práctica 4. Usamos o comando: `(nano compose.yaml)` para modificar o arquivo co seguinte:

version: '3.0'

services:

  bind9:
    image: internetsystemsconsortium/bind9:9.18
    container_name: bind9-serverJohan
    ports:
      - "54:53/udp"
      - "54:53/tcp"
      - "172.18.0.1:953:953/tcp"
    volumes:
      - ./etc-bind:/etc/bind
      - ./var-lib-bind:/var/lib/bind
      - ./var-cache-bind:/var/cache/bind
      - ./var-log:/var/log
    environment:
      - TZ=Europe/Madrid
    restart: unless-stopped

<h2>Usa os volumes como se explica no setup da imaxe</h2>

Usamos para crear os volumes: `(mkdir -p etc/bind var/cache/bind var/lib/bind var/log)`. 
Agora imos á carpeta **etc/bind/** con: `(cd etc/bind/)`.

Creamos un ficheiro con: `(touch named.conf)` e editámolo con: `(nano named.conf)`.

E colocamos o que indica a páxina de Docker para configurar o **Authoritative DNS server** dentro do ficheiro `named.conf`.

options {
        directory "/var/cache/bind";
        listen-on { 127.0.0.1; };
        listen-on-v6 { ::1; };
        allow-recursion {
                none;
        };
        allow-transfer {
                none;
        };
        allow-update {
                none;
        };
};

zone "example.com." {
        type primary;
        file "/var/lib/bind/db.example.com";
        notify explicit;
};

<h2>Unha comprobado que o contenedor funciona, sube a GitHub o ficheiro nun repo.</h2>

Para comprobar que funciona, é tan sinxelo como facer un **ping** á IP ou usar **dig** para verificar a configuración.




