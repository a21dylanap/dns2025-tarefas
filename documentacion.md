# 1.1 Instalación de zonas mestras primarias

### Instala o servidor BIND9 no equipo darthvader. Comproba que xa funciona coma servidor DNS caché pegando no documento de entrega a saída deste comando dig @localhost www.edu.xunta.es


```bash
root@darthvader:/var/cache/bind# dig @localhost www.edu.xunta.es

; <<>> DiG 9.20.11-4-Debian <<>> @localhost www.edu.xunta.es
; (2 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63029
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 69db2e54738afa9a0100000068e37b709f6ad117e6b59a7f (good)
;; QUESTION SECTION:
;www.edu.xunta.es.              IN      A

;; ANSWER SECTION:
www.edu.xunta.es.       1800    IN      CNAME   edu.xunta.es.
edu.xunta.es.           21423   IN      A       85.91.64.65

;; Query time: 63 msec
;; SERVER: 127.0.0.1#53(localhost) (UDP)
;; WHEN: Mon Oct 06 08:18:56 UTC 2025
;; MSG SIZE  rcvd: 103
```

### Configura o servidor BIND9 para que empregue como reenviador 8.8.8.8. pegando no documento de entrega contido do ficheiro /etc/bind/named.conf.options e a saída deste comando: dig @localhost www.mecd.gob.es 

```bash
root@darthvader:/var/cache/bind# dig @localhost www.mecd.gob.es

; <<>> DiG 9.20.11-4-Debian <<>> @localhost www.mecd.gob.es
; (2 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62120
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: c402996734e712c50100000068e37eec4cf5293eba641e3f (good)
;; QUESTION SECTION:
;www.mecd.gob.es.               IN      A

;; ANSWER SECTION:
www.mecd.gob.es.        21549   IN      A       212.128.114.116

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(localhost) (UDP)
;; WHEN: Mon Oct 06 08:33:48 UTC 2025
;; MSG SIZE  rcvd: 88
```

### 3. Instala unha zona primaria de resolución directa chamada "starwars.lan" e engade os seguintes rexistros de recursos (a maiores dos rexistros NS e SOA imprescindibles):

    Tipo A: darthvader con IP 192.168.20.10
    Tipo A: skywalker con IP 192.168.20.101
    Tipo A: skywalker con IP 192.168.20.111
    Tipo A: luke con IP 192.168.20.22
    Tipo A: darthsidious con IP 192.168.20.11
    Tipo A: yoda con IP 192.168.20.24 e 192.168.20.25
    Tipo A: c3p0 con IP 192.168.20.26
    Tipo CNAME palpatine a darthsidious
    TIPO MX con prioridade 10 sobre o equipo c3po
    TIPO TXT "lenda" con "Que a forza te acompanhe"
    TIPO NS con darthsidious
    Pega no documento de entrega o contido do arquivo de zona, e do arquivo /etc/bind/named.conf.local

```bash
$TTL 604800
@       IN      SOA     darthsidious.starwars.lan. admin.starwars.lan. (
                        2025100601 ; Serial
                        604800     ; Refresh
                        86400      ; Retry
                        2419200    ; Expire
                        604800 )   ; Negative Cache TTL

@       IN      NS      darthsidious.starwars.lan.
darthvader     IN      A       192.168.20.10
skywalker      IN      A       192.168.20.101
skywalker      IN      A       192.168.20.111
luke           IN      A       192.168.20.22
darthsidious   IN      A       192.168.20.11
yoda           IN      A       192.168.20.24
yoda           IN      A       192.168.20.25
c3p0           IN      A       192.168.20.26


palpatine      IN      CNAME   darthsidious

@              IN      MX 10   c3p0.starwars.lan.

lenda          IN      TXT     "Que a forza te acompanhe"
```




# Hacer la red
sudo vboxtun.sh tap0 br-a6314929999e

20.168.192