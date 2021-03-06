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
![width=400](assets/img/SOAPSimpleO1.png)
<br>
Le parti di cui è composto un messaggio SOAP stabilito dallo standard.
@snapend

---?gist=MassimoCappellano/4803465f006725a9044a78f0e7a066b7&title=Servizio che chiede i valori di un'azione
### SOAP Request

---?gist=MassimoCappellano/33ae0970f3d193d3c7b1897f72626187&title=Messaggio di ritorno alla richiesta
### SOAP Response
---

### SOAP Tutorial


[LEARN WEB SERVICES|Free, public SOAP web services example](http://www.learnwebservices.com/)

---
### Cos'è REST?

**REST** (REpresentational State Transfer) definendolo come uno stile architetturale per la progettazione e la creazione di servizi Web, in altre parole REST rappresenta un insieme di regole che definiscono come scambiare risorse in un sistema distribuito

---
@snap[north-west text-06]
### Demistifichiamo REST

La sigla REST, **RE**presentional **S**tate **T**ransfer, sembra alquanto criptica.  
Esso semplicemente vuol dire che il server ha una risorsa e il client può chiedere una rappresentazione (descrizione) dello 'stato' della risorsa. 
<br>
Per esempio, se la risorsa è il post di un blog dentro un database, allora il suo 'respresentional state' potrebbe essere la lista dei valori del record del database.  

![width=750](assets/img/REST_sequence_diagram.PNG)

@snapend
---
@snap[north-west text-06]
Questo significa che il client non si cura dell'implementazione interna della risorsa sul server. Il server potrebbe conservare il post del blog in un database Oracle, un file di testo, o potrebbe essere
generato da una chimata di procedura; questo non interessa al client. Tutto ciò di interessa è la 
rappresentazione che riceve dal server.  
<br>
Il formato **JSON** (Javascript Object Notation) è spesso utilizzato per rappresentare la risorse in REST. E' una semplice notazione coppia nome-valore. Per esempio, la rappresentazione del post del blog nello Step 4, precedente, potrebbe essere in formato JSON:

```javascript
{ 
    "title": "7 Things You Didn't Know about Star Wars", 
    "content": "George Lucas accidentally revealed that..." 
}
```
Quando il client riceve la rappresentazione può, per esempio, cambiare il titolo, e inviare la rappresentazione modificata al server. Il server allora modificherà la sua risorsa interna con i dati della rappresentazione modificata; per esempio modificare il record del database con il nuovo titolo.  
<br>
Quindi "**RE**presentional **S**tate **T**ransfer" semplicemente significa che stiamo trasferendo queste stati di rappresentazione tra il client e il server.

@snapend
---
@snap[north-west text-06]
### Regole per servizi REST (detti RESTFul)
@ul[](false)
- **Client-server**: la comunicazione tra le applicazioni segue il paradigma c/s. Questo disaccoppiamento garantisce che, purché sia stata concordata un'interfaccia, lo sviluppo di client e server può essere eseguito in modo indipendente; 
- **Stateless**: Nessuno stato client è memorizzato sul server. Tutte le informazioni necessarie per eseguire le operazioni sono contenute nelle richieste;
- **Cacheable**: I servizi Web RESTful devono fornire funzionalità di memorizzazione nella cache. I server possono indicare come e per quanto tempo memorizzare nella cache le risposte. I client possono utilizzare le risposte memorizzate nella cache invece di contattare il server. Poiché REST in genere utilizza HTTP, eredita tutte le proprietà di memorizzazione nella cache offerte da HTTP; 
- **Interfaccia uniforme**: le risorse che il server espone devono essere identificate da URI; 
- **Sistema a strati**: Data l’architettura c/s, i client non sono consapevoli del server specifico con cui interagiscono. Questa proprietà consente l'introduzione di server intermedi che possono, ad esempio, gestire la sicurezza o offrire funzionalità di bilanciamento del carico; 
- **Codice su richiesta (opzionale)**: Anche se fa parte dell'architettura REST, questo principio è facoltativo. I server possono estendere le funzionalità dei client trasferendo codice eseguibile;
@ulend
@snapend
---
@snap[north-west text-06]
### Interfaccia uniforme
Ciò che veramente caratterizza REST rispetto ad altri stili archetitturali è l'interfaccia uniforme.  
<br>
Caratteristiche principali delle appicazioni REST:
@ul[](false)
- Le api sono progettate in base a risorse, che possono essere costituite da qualsiasi tipologia di oggetto, servizio o dati accessibile dal client; 
- Una risorsa ha un identificatore, costituito da un URI che identifica in modo univoco la risorsa; 
- I client interagiscono con un servizio scambiando rappresentazioni delle risorse. Molte API usano JSON come formato di scambio; 
- Le API usano un'interfaccia uniforme che consente di separare le implementazioni del client e del servizio. Per le API basate su HTTP, l'interfaccia uniforme include l'uso di verbi HTTP standard per l'esecuzione di operazioni sulle risorse. Le operazioni più comuni sono GET, POST, PUT, PATCH e DELETE;
@ulend

@snapend
---
### REST Tutorial

[Go Rest | Online REST API for Testing and Prototyping](https://gorest.co.in/)


---

### Lezione

https://checksound.gitbook.io/tecnologie5/web-services




