# vacation-osgi
Vacation Integration Sample as an OSGi Bundle

## ServiceMix Deployment

1. Download <a href="http://example.com/">SericeMix</a> (getestet ab 5.4.0) und entpacken

2. ``` git clone https://github.com/predic8/vacation-osgi ```

3. ``` mvn install ```

4. ``` ./bin/servicemix ```

5. Installieren der beiden Camel-Features Jetty und XML-Json
  ```
  features:install camel-jetty
  features:install camel-xmljson 
  ```
6. Installation des Projekts im ServiceMix
  ```install mvn:de.predic8/vacation-osgi```

7. ```list```
  es sollte nun ```[ 151] [Installed  ] [            ] [       ] [   80] Vacation ESB Sample OSGi (1.0.0.SNAPSHOT) ```erscheinen
  
8. ``` camel:context-list ```

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
