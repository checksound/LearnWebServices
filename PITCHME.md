# I Web Services

---

@snap[north-west text-08]
### I Web Services
“A web service is a software system designed to support interoperable machine-to-machine interaction over a network. It has an interface described in a machine-processable format “ (W3C, Web Services Glossary )
<br><br>
Parliamo quindi di:
@ol[]
1. servizio - offre un servizio specifico, ad esempio: servizio prenotazioni, dati geolocalizzazioni, ...;
1. web - invocabile da web, utilizza i protocolli del web;
1. interfaccia - espone in modo rigoroso in un formato processabile da un client software i servizi che espone;
@olend

@snapend
---
@snap[north-west text-07]
![width=700](assets/img/intro_ws_roles.gif)
<br>
*WSD*: web service descriptor, un formato processabile da un client che descrive l'interfaccia esposta.
@snapend
---
@snap[north-west]
### RPC - Remote Procedure Call
![width=700](assets/img/RPC.PNG)
<br>
I Web Service, 'un altro modo per fare RPC'.
@snapend
---
@snap[west]
Esistono due modalità principali di Web Services:
@ul[]
* SOAP - **S**imple **O**bject **A**ccess **P**rotocol;
* REST - **RE**presentional **S**tate **T**ransfer;
@snapend
---
@snap[north-west]
### SOAP
Vediano tremite un esempio di capire la funzione del WSDL, partendo dall'esempio di un servizio che ritorna i valori delle azioni (Stocks).<br>
<br>
Il WSDL, è un documento in formato XML, descritto come specifica del W3C, che permette di definire in
modo preciso l'interfaccia esposta dai Web Services.
@snapend
---?gist=MassimoCappellano/d15675cbabf291c47705512e02581622&lang=xml&title=Esempio WSDL di un servizio per chiedere i valori di borsa di un'azione:
@snap[text-08]
@[9-27](Types -- a container for data type definitions using some type system (such as XSD).)
@[29-35](Message -- an abstract, typed definition of the data being communicated.)
@[37-42](Operation -- an abstract description of an action supported by the service.)
@snapend
---

@snap[north-west text-07]
### Le altre parti specificate nel WSDL sono:
@ul[](false)
* Port Type -- an abstract set of operations supported by one or more endpoints.
* Binding -- a concrete protocol and data format specification for a particular port type.
* Port -- a single endpoint defined as a combination of a binding and a network address.
* Service -- a collection of related endpoints.
@ulend
<br>
<br>
Tutte queste parti specificano in modo preciso il 'contratto' tra client e il web service. Abbiamo già detto che il WSDL è espresso in linguaggio XML.  
<br>
XML è un linguaggio di markup che permette di descrivere delle strutture dati come nel caso del WSDL, in cui descrive il tipo dei dati dei metodi o anche rappresentare dati veri e propri, come nel caso dei massaggi scambiati tra client e server.  
@snapend

---
@snap[north-west]
### SOAP Message
![](assets/img/SOAPSimpleO1.png)
@snapend

---?gist=MassimoCappellano/4803465f006725a9044a78f0e7a066b7&title=Servizio che chiede i valori di un'azione
### SOAP Request

---?gist=MassimoCappellano/33ae0970f3d193d3c7b1897f72626187&title=Messaggio di ritorno alla richiesta
#### SOAP Response
---
@snap[north-west text-07]

### SOAP Request

Servizio che chiede i valori di un'azione in questa richiesta `MOT`.
```xml
POST /StockQuote HTTP/1.1
Host: www.stockquoteserver.com
Content-Type: text/xml;
charset="utf-8"
Content-Length: nnnn
SOAPAction: "Some-URI"

<SOAP-ENV:Envelope
 xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" 
 SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"> 
   <SOAP-ENV:Body>
    <m:GetLastTradePrice
     xmlns:m="Some-URI">
      <symbol>MOT</symbol>
    </m:GetLastTradePrice>     
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
@snapend
---
@snap[north-west text-07]

### SOAP Response

Messaggio di ritorno alla richiesta del client con in valore dell'azione.

```
HTTP/1.1 200 OK Content-Type: text/xml; charset="utf-8"
Content-Length: nnnn

<SOAP-ENV:Envelope
 xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"
 SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"/>   
 <SOAP-ENV:Body>
  <m:GetLastTradePriceResponse
   xmlns:m="Some-URI">
   <Price>14.5</Price>
  </m:GetLastTradePriceResponse>
 </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
@snapend
---

@snap[west text-06]
Esempio Web Service SOAP:<br>

https://geoservices.tamu.edu/Services/Geocode/WebService/v04_01/Simple/SOAP/
<br>
<br>
**API URL:**<br>
https://geoservices.tamu.edu/Services/Geocode/WebService/GeocoderService_V04_01.asmx
<br>
<br>
**WSDL:**<br>
https://geoservices.tamu.edu/Services/Geocode/WebService/GeocoderService_V04_01.asmx?WSDL

@snapend
---














