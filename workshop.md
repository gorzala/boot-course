# Boot tut gut, Lit macht fit


![SI-Logo](si-logo.svg) 

## Ein Workshop auf der Signal Iduna Entwickler Konferenz 2022

 - Dominik Bruhn (SDA)
 - Marc Gorzala (EAM)

---
# Agenda

- Projekt vorstellen
- Technische Voraussetzungen überprüfen
- Spring Boot anwenden
   - Projekt initialisieren
   - Endpunkte anbieten
   - Datenbank anbinden

---

# Was das Projekt macht ...

wirst Du einen [Link Shortner (siehe Wikipedia)](https://de.wikipedia.org/wiki/Kurz-URL-Dienst) bauen.

Damit können lange und unhandliche Links wie z.B.

`https://dancelake.dancier.net/app/discover#/?_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-15m,to:now))&_a=(columns:!(),filters:!(),index:'4abc5890-1a1b-11ed-8adb-b3d20577e6cb',interval:auto,query:(language:kuery,query:''),sort:!(!('@timestamp',desc)))`

in leichter zu handhabende überführt werden wie z.B.

`https://silish.signal-iduna.de/1`


[Demo](http://foo.bar)

---

# Die Architektur
![Silish-Logo](high-level-architecture.svg)

 - [Single Page Application (SPA) mit Lit](https://de.wikipedia.org/wiki/Single-Page-Webanwendung)
 - [Backend mit Boot](https://spring.io/projects/spring-boot/)
 - [Datenbank mit PostgreSQL](https://www.postgresql.org/)


![Lit-Logo](lit-logo.svg)
![Boot-Logo](boot.png)

---

# Checke Deine Umgebung (1/4)

- [X] Bauen des Backends
- [ ] Aufrufen der Endpunkte
- [ ] Bauen des Frontend
- [ ] Aufrufen des Projekts

Im Terminal:

    !bash
    java -version

überprüfen ob Java 11 genutzt wird. Sonst mit dem SDK-Man konfiguieren.

dann im geclonten Projekt

    !bash
    git checkout develop;
    cd backend;
    ./gradew installDist;
    docker-compose up -d --build;
    docker-compose ps;

Du solltest hier drei Dienste sehen die "UP" sind.

Schaue [hier](http://localhost:8081/metics/health) nach ob das Backend healty ist.

---
# Checke Deine Umgebung (2/4)

- [X] Bauen des Backends
- [X] Aufrufen der Endpunkte
- [ ] Bauen des Frontend
- [ ] Aufrufen des Projekts

Im geclonten Project. Importiere die Insomanie Endpunkte aus dem Ordner Support in Dein Insomania.

Passe den konfigurierten Endpunkt getToken an, so dass Dein Racf-Account genutzt wird.

Klicke dich mal durch die Endpunkte.


---
# Checke Deine Umgebung (3/4)

- [X] Bauen des Backends
- [X] Aufrufen der Endpunkte
- [X] Bauen des Frontend
- [ ] Aufrufen des Projekts

---
# Checke Deine Umgebung (4/4)

- [X] Bauen des Backends
- [X] Aufrufen der Endpunkte
- [X] Bauen des Frontend
- [X] Aufrufen des Projekts


---

# Spring Boot

Vor Spring Boot, war es nicht unüblich dass Entwickler teils mehrere Tage benötigten um Frontend Technologien z.B. mit Persistence Frameworks und diese mit den entsprechenden Datenbanken zu verbinden.

Boot, hat von verschiedenen anderen Frameworks Ideen aufgegriffen und diese zusammen mit dem vorhanden Spring Ökosystem zu einem Framework zusammengeführt, mit dem Entwickler sehr schnell professionelle Applikationen erstellen können.

* Optionated View auf Anwendungen
* Convention over Configuration


Sehr weit verbreitet. Mindestens Spring ist den allermeisten Entwicklern vertraut

---
# Ein erstes Projekt

Gehe hierzu auf den [Spring Initializer](https://start.spring.io/).
Spring CLI [https://docs.spring.io/spring-boot/docs/current/reference/html/cli.html#cli.using-the-cli.initialize-new-project](Spring CLI)
* Schaue Dich um was, es alles es für Abhängigkeiten gibt.
* Wähle dann folgdes aus:
  * Gradle Projekt
  * Java
  * Version 2.7.3 von Spring Boot
  * Packing JAR
  * Java 11
  * Actuator, Spring Web

Nun generiere und lade das Archiv herunter. Endpacke es, welchsle ins Root-Verzeichnis und führe die Boot-Applikation mit ./gradew bootRun aus.


---
# Was läuft hier eigentlich alles?

[HealthCheck unter http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)
Er lebt!

Welche Beans gibt es eigentlich schon jetzt?

Noch gibt der Actuator diese nicht aus:
[Actuator unter http://localhost:8080/actuator/](http://localhost:8080/actuator/)

Wie geht es?
https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#actuator.endpoints.exposing


# Der erste Endpunkt

@RestController
Eine Klasse hiermit annotiert führt dazu, dass wir in dieser sehr einfach Rest-Endpunkte schreiben können.

@GetMapping("uri")
An einer Methode annotiert, können wir so leicht einzelne Get-Endpunkte schreiben. 

https://spring.io/guides/gs/rest-service/

Schreibe nun einen Rest-Endpunkt, der Hello World zurückgibt!


https://www.baeldung.com/spring-boot-customize-jackson-objectmapper


# Autoconfigration einer Datasource

Füge der `build.gradle` die Module für PostgreSQL und Spring Data Jpa hinzu.

starte die Applikation. Du wirst sehen, dass das System nicht startet.

Autoconfiguration

Du musst noch die application.yml anpassen
---

# Wo geht es weiter?

Themen die wir hier nicht behandelt haben, die aber in der Regel sehr wichtig sind:

 * Monitoring und Logging
 * API Dokumentation
 * Authorisierung
 * Resillince
 * ...

