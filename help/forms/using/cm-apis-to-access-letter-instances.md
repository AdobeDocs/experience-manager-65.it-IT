---
title: API per accedere alle istanze delle lettere
description: Scopri le API e utilizzale per accedere in modo programmatico alle istanze di lettere nell’ambiente AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# API per accedere alle istanze delle lettere {#apis-to-access-letter-instances}

## Panoramica {#overview}

Utilizzando l’interfaccia utente per la creazione della corrispondenza di Gestione corrispondenza, puoi salvare le bozze delle istanze di lettere in corso e sono presenti istanze di lettere inviate.

Gestione della corrispondenza fornisce API che consentono di creare l’interfaccia per l’inserzione in modo che funzioni con le istanze di lettere inviate o le bozze. Le API elencano e aprono le istanze di lettera inviata e bozza di un agente, in modo che l’agente possa continuare a lavorare sulle istanze di lettera bozza o inviata.

## Recupero delle istanze di lettere {#fetching-letter-instances}

Gestione della corrispondenza espone le API per recuperare le istanze di lettere tramite il servizio LetterInstanceService.

| Metodo | Descrizione |
|--- |--- |
| getAllLetterInstances | Recupera le istanze di lettere in base al parametro di query di input. Per recuperare tutte le istanze di lettere, passa il parametro di query come null. |
| getLetterInstance | Recupera l’istanza della lettera specificata in base all’ID dell’istanza della lettera. |
| letterInstanceExists | Controlla se esiste una LetterInstance con il nome specificato. |

>[!NOTE]
>
>LetterInstanceService è un servizio OSGI e la relativa istanza può essere recuperata utilizzando @Reference in Java™
>Classe o sling.getService(LetterInstanceService. Class ) in JSP.

### Utilizzo di getAllLetterInstances {#using-nbsp-getallletterinstances}

L’API seguente trova le istanze di lettere in base all’oggetto query (sia Inviato che Bozza). Se l&#39;oggetto query è null, restituisce tutte le istanze di lettere. Questa API restituisce un elenco di [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) che possono essere utilizzati per estrarre informazioni aggiuntive dell&#39;istanza della lettera.

**Sintassi**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>Il parametro query viene utilizzato per trovare/filtrare l’istanza di Letter. In questo caso, la query supporta solo attributi/proprietà di livello superiore dell’oggetto. Query è costituita da istruzioni e "attributeName" utilizzato nell'oggetto Statement deve essere il nome della proprietà nell'oggetto istanza Letter.<br /> </td>
  </tr>
 </tbody>
</table>

#### Esempio 1: recupera tutte le istanze di lettere di tipo INVIATO {#example-fetch-all-the-letter-instances-of-type-submitted}

Il codice seguente restituisce l&#39;elenco delle istanze di lettere inviate. Per ottenere solo le bozze, modifica il `LetterInstanceType.COMPLETE.name()` a `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### Esempio 2: recupera tutte le istanze di lettere inviate da un utente e il tipo di istanza di lettera è BOZZA {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

Il codice seguente include più istruzioni nella stessa query per ottenere i risultati filtrati in base a criteri diversi, ad esempio l&#39;istanza della lettera inviata (attributo submit by) da un utente e il tipo di letterInstanceType è DRAFT.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### Utilizzo di getLetterInstance {#using-nbsp-getletterinstance}

Recupera l’istanza della lettera identificata dall’ID istanza della lettera specificato. Restituisce &quot;null&quot; se l’ID istanza non corrisponde.

**Sintassi:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Verifica dell&#39;esistenza di LetterInstance {#verifying-if-letterinstance-exist}

Verifica se esiste un’istanza di lettera con il nome specificato

**Sintassi**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parametro** | **Descrizione** |
|---|---|
| letterInstanceName | Nome dell’istanza della lettera che desideri verificare se esiste. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Apertura delle istanze di lettere {#opening-letter-instances}

L&#39;istanza della lettera può essere di tipo Inviata o Bozza. L’apertura di entrambi i tipi di istanza della lettera mostra comportamenti diversi:

* Se è presente un’istanza di Inviata lettera, viene aperto un PDF che rappresenta l’istanza di Lettera. L’istanza della lettera inviata è persistente sul server e contiene anche dataXML e XDP elaborato, che può essere utilizzato per eseguire e personalizzare ulteriormente un caso d’uso, ad esempio la creazione di un PDF/A.
* Se è presente un’istanza Bozza lettera, l’interfaccia utente per la corrispondenza viene ricaricata nello stato precedente esatto, come era al momento della creazione della bozza

### Apertura dell&#39;istanza della bozza di lettera  {#opening-draft-letter-instance-nbsp}

L’interfaccia utente CCR supporta il parametro cmLetterInstanceId, che può essere utilizzato per ricaricare la lettera.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Non è necessario specificare cmLetterId o cmLetterName/State/Version durante il ricaricamento di una corrispondenza, in quanto i dati inviati contengono già tutti i dettagli sulla corrispondenza ricaricata. RandomNo viene utilizzato per evitare problemi di cache del browser; è possibile utilizzare una marca temporale come numero casuale.

### Apertura istanza lettera inviata {#opening-submitted-letter-instance}

Il PDF inviato può essere aperto direttamente utilizzando l’ID istanza della lettera:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
