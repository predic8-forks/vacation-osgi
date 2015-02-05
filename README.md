# vacation-osgi
Vacation Integration Sample as an OSGi Bundle

## ServiceMix Deployment

1. Download des <a href="http://example.com/">Sericemix</a> (getestet ab 5.4.0) und entpacken

2. Klonen des Git Archivs
  ```
  git clone https://github.com/predic8/vacation-osgi
  ```
3. Nachladen der Dependencies mit Maven
  ``` mvn install ```

4. Nun kannst Du den Servicemix starten
  ``` ./servicemix ```

5. Installieren der beiden Features Jetty und XML-Json
  ```
  features:install camel-jetty
  features:install camel-xmljson 
  ```
6. Installation des Projekts im ServiceMix
  ```install mvn:de.predic8/vacation-osgi```

7. unter ```list``` sollte nun Vaction-osgi erscheinen.

9. Bei erfolgreichem Start erscheint der Context nun in der Liste
  ``` camel:context-list ```

## Testen des Deployments
Wenn Curl installiert ist, dann kann das beiliegende Sample-File welches sich im Root-Verzeichnis dieses Projektes befindet mit dem folgenden Befehl an die Camel-Route geschickt werden.

curl -X POST -d @data.json http://localhost:8080/vacation


Weitere Informationen können mittels der folgenden Befehle eingesehen werden: 

```
camel:context-info vacation 

camel:route-list 

camel:route-info  route4 

activemq:bstat 
activemq:dstat 
```
