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
 vacation       Started        17.500 seconds 
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
```
camel:route-list 

 Context        Route           Status   
 -------        -----           ------   
 vacation       VacationRoute   Started  
````
```
camel:route-info  VacationRoute

Camel Route VacationRoute
	Camel Context: vacation

Properties
	parent = 575397c8
	id = VacationRoute
	group = de.predic8.vacation.Routes

Statistics
	Inflight Exchanges: 0
	Exchanges Total: 0
	Exchanges Completed: 0
	Exchanges Failed: 0
	Min Processing Time: 0 ms
	Max Processing Time: 0 ms
	Mean Processing Time: 0 ms
	Total Processing Time: 0 ms
	Last Processing Time: 0 ms
	Delta Processing Time: 0 ms
	Load Avg: , , 
	Reset Statistics Date: 2015-02-05 18:15:16
	First Exchange Date:
	Last Exchange Completed Date:

Definition
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<route group="de.predic8.vacation.Routes" trace="true" customId="true" id="VacationRoute" xmlns="http://camel.apache.org/schema/spring">
    <from uri="jetty:http://localhost:8080/vacation/"/>
    <unmarshal ref="xmljson" id="unmarshal2"/>
    <setHeader headerName="city" id="setHeader8">
        <xpath>//city/text()</xpath>
    </setHeader>
    <setHeader headerName="name" id="setHeader9">
        <xpath>//name/text()</xpath>
    </setHeader>
    <log message="${header.name} wants to go to ${header.city}" id="log2"/>
    <setHeader headerName="CamelHttpPath" id="setHeader10">
        <simple>data/2.5/find?q=${header.city}&amp;units=metric&amp;mode=xml</simple>
    </setHeader>
    <setHeader headerName="CamelHttpMethod" id="setHeader11">
        <expressionDefinition>GET</expressionDefinition>
    </setHeader>
    <to uri="jetty:http://api.openweathermap.org/?bridgeEndpoint=true" id="to5"/>
    <convertBodyTo type="org.w3c.dom.Document" id="convertBodyTo2"/>
    <setHeader headerName="count" id="setHeader12">
        <xpath>//count/text()</xpath>
    </setHeader>
    <setHeader headerName="temp" id="setHeader13">
        <xpath>//temperature/@max</xpath>
    </setHeader>
    <to uri="xslt:weather2booking.xsl" id="to6"/>
    <choice id="choice2">
        <when id="when3">
            <expressionDefinition>header{count} == 0</expressionDefinition>
            <setHeader headerName="CamelHttpResponseCode" id="setHeader14">
                <expressionDefinition>400</expressionDefinition>
            </setHeader>
            <setBody id="setBody4">
                <simple>{ "message" : "city not found" }</simple>
            </setBody>
        </when>
        <when id="when4">
            <simple>${header.temp} &gt; 20</simple>
            <to pattern="InOnly" uri="activemq:beach" id="to7"/>
            <setBody id="setBody5">
                <simple>{ "message" : "Enjoy the sun!" }</simple>
            </setBody>
        </when>
        <otherwise id="otherwise2">
            <to pattern="InOnly" uri="activemq:ski" id="to8"/>
            <setBody id="setBody6">
                <simple>{ "message" : "You go skiing!" }</simple>
            </setBody>
        </otherwise>
    </choice>
</route>
````
```
activemq:bstat 

```
```
activemq:dstat 
```
