---
title: API per accedere alle istanze di lettere
seo-title: API per accedere alle istanze di lettere
description: Scopri come utilizzare le API per accedere alle istanze di lettere.
seo-description: Scopri come utilizzare le API per accedere alle istanze di lettere.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# API per accedere alle istanze di lettere {#apis-to-access-letter-instances}

## Panoramica {#overview}

Utilizzando l’interfaccia utente Crea corrispondenza di Gestione corrispondenza è possibile salvare le bozze delle istanze di lettere in corso e sono presenti istanze di lettere inviate.

Gestione corrispondenza fornisce API che consentono di creare l’interfaccia per l’inserimento nell’elenco in modo da utilizzare le istanze di lettere o le bozze inviate. Le API elencano e aprono le istanze di lettera inviate e bozza di un agente, in modo che l&#39;agente possa continuare a lavorare sulle istanze di lettera bozza o inviate.

## Recupero delle istanze di lettere {#fetching-letter-instances}

Gestione corrispondenza espone le API per recuperare le istanze di lettere tramite il servizio LetterInstanceService.

| Metodo | Descrizione |
|--- |--- |
| getAllLetterInstances | Recupera le istanze di lettere in base al parametro della query di input. Per recuperare tutte le istanze di lettere, passa il parametro di query come null. |
| getLetterInstance | Recupera l&#39;istanza di lettera specificata in base all&#39;ID dell&#39;istanza di lettera. |
| letterInstanceExists | Controlla se esiste una LetterInstance in base al nome specificato. |

>[!NOTE]
>
>LetterInstanceService è un servizio OSGI e la sua istanza può essere recuperata utilizzando @Reference in Java
>Classe o sling.getService(LetterInstanceService). Classe ) in JSP.

### Utilizzo di getAllLetterInstances {#using-nbsp-getallletterinstances}

L’API seguente trova le istanze della lettera in base all’oggetto query (Inviato e Bozza). Se l&#39;oggetto query è nullo, restituisce tutte le istanze della lettera. Questa API restituisce l&#39;elenco degli oggetti [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), che possono essere utilizzati per estrarre informazioni aggiuntive sull&#39;istanza della lettera

**Sintassi**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>Il parametro query viene utilizzato per trovare/filtrare l’istanza Letter. La query qui supporta solo gli attributi/proprietà di primo livello dell’oggetto. La query è costituita da istruzioni e il "attributeName" utilizzato nell'oggetto Statement deve essere il nome della proprietà nell'oggetto di istanza Letter.<br /> </td>
  </tr>
 </tbody>
</table>

#### Esempio 1: Recupera tutte le istanze di lettera di tipo INVIATO {#example-fetch-all-the-letter-instances-of-type-submitted}

Il codice seguente restituisce l&#39;elenco delle istanze di lettere inviate. Per ottenere solo le bozze, cambia il valore `LetterInstanceType.COMPLETE.name()` in `LetterInstanceType.DRAFT.name().`

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

#### Esempio 2: il recupero di tutte le istanze di lettera inviate da un utente e da un tipo di istanza di lettera è DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

Il codice seguente contiene più istruzioni nella stessa query per ottenere i risultati filtrati in base a criteri diversi, come l&#39;istanza di lettera inviata (attributo inviato da) da un utente e il tipo di letterInstanceType è DRAFT.

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

Recupera l’istanza della lettera identificata dall’ID istanza lettera specificato. Restituisce &quot;null se l&#39;ID istanza non corrisponde.

**Sintassi:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Verifica dell&#39;esistenza di LetterInstance {#verifying-if-letterinstance-exist}

Controlla se esiste un&#39;istanza di Lettera in base al nome specificato

**Sintassi**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parametro** | **Descrizione** |
|---|---|
| letterInstanceName | Nome dell&#39;istanza di lettera che si desidera controllare se esiste. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Apertura delle istanze di lettere {#opening-letter-instances}

L&#39;istanza della lettera può essere di tipo Inviato o Bozza. L’apertura di entrambi i tipi di istanza della lettera mostra diversi comportamenti:

* Nel caso di istanza di lettera inviata, viene aperto un PDF che rappresenta l’istanza di lettera. L&#39;istanza Lettera inviata persistita sul server contiene anche i datiXML e XDP elaborati, che possono essere utilizzati per eseguire e personalizzare ulteriormente un caso d&#39;uso come la creazione di un PDF/A.
* Nel caso di un&#39;istanza di bozza di lettera, l&#39;interfaccia utente per la creazione della corrispondenza viene ricaricata allo stato precedente esatto come nel momento in cui è stata creata la bozza

### Apertura istanza bozza  {#opening-draft-letter-instance-nbsp}

L’interfaccia utente CCR supporta il parametro cmLetterInstanceId , che può essere utilizzato per ricaricare le lettere.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Non è necessario specificare il cmLetterId o cmLetterName/State/Version al momento del ricaricamento di una corrispondenza, in quanto i dati inviati contengono già tutti i dettagli sulla corrispondenza che viene ricaricata. RandomNo viene utilizzato per evitare problemi di cache del browser, è possibile utilizzare la marca temporale come numero casuale.

### Apertura istanza lettera inviata {#opening-submitted-letter-instance}

Il PDF inviato può essere aperto direttamente utilizzando l’ID di istanza della lettera:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
