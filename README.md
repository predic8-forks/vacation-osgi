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

7. ``` list ```
  es sollte nun 
  ``` [ 151] [Installed  ] [            ] [       ] [   80] Vacation ESB Sample OSGi (1.0.0.SNAPSHOT) ```
  erscheinen
  
8. ``` camel:context-list ``` zeigt nun
  ``` 
   Context        Status         Uptime              
 -------        ------         ------              
 weathermap     Started        2 hours 26 minutes  
  ```

## Testen des Deployments
Wenn Curl installiert ist, dann kann das beiliegende Sample-File welches sich im Root-Verzeichnis dieses Projektes befindet mit dem folgenden Befehl an die Camel-Route geschickt werden.

``` curl -X POST -d @data.json http://localhost:8080/vacation ```


Weitere Informationen können mittels der folgenden Befehle eingesehen werden: 

```
camel:context-info vacation

Camel Context vacation
	Name: vacation
	ManagementName: vacation-osgi
	Version: 2.13.2
	Status: Started
	Uptime: 24.091 seconds

Statistics
	Exchanges Total: 0
	Exchanges Completed: 0
	Exchanges Failed: 0
	Min Processing Time: 0ms
	Max Processing Time: 0ms
	Mean Processing Time: 0ms
	Total Processing Time: 0ms
	Last Processing Time: 0ms
	Delta Processing Time: 0ms
	Load Avg: , , 
	Reset Statistics Date: 2015-02-05 18:15:16
	First Exchange Date:
	Last Exchange Completed Date:
	Number of running routes: 1
	Number of not running routes: 0

Miscellaneous
	Auto Startup: true
	Starting Routes: false
	Suspended: false
	Shutdown timeout: 300 sec.
	Allow UseOriginalMessage: true
	Message History: true
	Tracing: false

Properties

Advanced
	ClassResolver: org.apache.camel.core.osgi.OsgiClassResolver@7bfe8258
	PackageScanClassResolver: org.apache.camel.core.osgi.OsgiPackageScanClassResolver@65d7d60c
	ApplicationContextClassLoader: BundleDelegatingClassLoader(vacation-osgi [151])

Components
	activemq
	jetty
	xslt
	properties

Dataformats
	xmljson

Routes
	VacationRoute
```

camel:route-list 

camel:route-info  vacationRoute 

activemq:bstat 
activemq:dstat 
```
