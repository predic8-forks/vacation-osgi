# vacation-osgi
Vacation Integration Sample as an OSGi Bundle

## ServiceMix Deployment

1. Download des <a href="http://example.com/">Sericemix</a> (getestet ab 5.4.0) und entpacken

2. Klonen des Git Archivs
  ```
  git clone https://github.com/predic8/vacation-osgi
  ```
3. Nachladen der Dependencies mit Maven
  ```mvn install ``

4. Nun kannst Du den Servicemix starten
  ```./servicemix```

5. Installieren der beiden Features Jetty und XML-Json
  ```
  features:install camel-jetty
  features:install camel-xmljson 
  ```
6. Installation des Projekts im ServiceMix
  ```install mvn:de.predic8/vacation-osgi```

7. list zeigt
8. Zeigt Servicemix an, dass sich das Deployment in der "GracePeriod" befindet, dann hat die Installation einer der Dependencies nicht funktioniert. Camel-jetty und camel-xmljson müssen beide ebenfalls aufgeführt werden, wenn der Befehlt "list" ausgeführt wird.
9. Wenn der Start erfolgreich war, dann sollte nach ausführen von "camel:context-list" der Camel-Context des Vacation-OSGi Projektes in einer Liste angezeigt werden.


camel:context-info vacation 

camel:route-list 

## Testen des Deployments
Wenn Curl installiert ist, dann kann das beiliegende Sample-File welches sich im Root-Verzeichnis dieses Projektes befindet mit dem folgenden Befehl an die Camel-Route geschickt werden.

curl -X POST -d @data.json http://localhost:8080/vacation

camel:route-info  route4 

Statistiken anschaun

activemq:bstat 
activemq:dstat 

