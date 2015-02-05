# vacation-osgi
Vacation Integration Sample as an OSGi Bundle

## ServiceMix Deployment

1. Download des Sericemix 5.4.0 von http://servicemix.apache.org/ und das heruntergeladene Zip entpacken

2. Klonen des Git Archivs mittels https://github.com/predic8/vacation-osgi oder Download des Repositories als Zip-Archiv

3. Navigiere in das vacation-osgi Verzeichnis und führe mvn install aus.

4. Nun kannst Du den Servicemix starten, dazu navigierst Du auf der Konsole in das Servicemix/bin Verzeichnis und führst servicemix.bat aus.

5. Sobald Servicemix gestartet ist, müssen die beiden folgenden beiden Features installiert werden, dazu die beiden Eingaben einzeln in die Servicemix Eingabeaufforderung kopieren und asuführen:
  features:install camel-jetty
  features:install camel-xmljson 

6. Jetzt kann aus dem lokalen Maven Repository das vaction-osgi Projekt dirent im Servicemix installiert werden.
  install mvn:de.predic8/vacation-osgi

7. Nun kannst du den Befehl list auf der Servicemix Konsole ausführen und darin sollte das vacation-osgi deployment aufgelistet sein.
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

