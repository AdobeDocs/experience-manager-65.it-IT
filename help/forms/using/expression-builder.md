---
title: Funzioni remote in Expression Builder
description: Il Generatore di espressioni in Gestione della corrispondenza consente di creare espressioni e funzioni remote.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Funzioni remote in Expression Builder{#remote-functions-in-expression-builder}

Utilizzando il Generatore di espressioni, puoi creare espressioni o condizioni che eseguono calcoli sui valori dei dati forniti dal dizionario dati o dagli utenti finali. Gestione della corrispondenza utilizza il risultato della valutazione dell’espressione per selezionare risorse quali testo, immagini, elenchi e condizioni e inserirle nella corrispondenza come richiesto.

## Creazione di espressioni e funzioni remote con il generatore di espressioni {#creating-expressions-and-remote-functions-with-expression-builder}

Il Generatore di espressioni utilizza internamente le librerie JSP EL, in modo che l’espressione sia conforme alla sintassi JSPEL. Per ulteriori informazioni, consulta [Espressioni di esempio](#exampleexpressions).

![Generatore di espressioni](assets/expressionbuilder.png)

### Operatori {#operators}

Gli operatori disponibili per l’utilizzo nelle espressioni sono disponibili nella barra superiore del generatore di espressioni.

### Espressioni di esempio {#exampleexpressions}

Di seguito sono riportati alcuni esempi JSP EL comunemente utilizzati che è possibile utilizzare nella soluzione di gestione della corrispondenza:

* Per aggiungere due numeri: ${number1 + number2}
* Per concatenare due stringhe: ${str1} ${str2}
* Per confrontare due numeri: ${age &lt; 18}

Per ulteriori informazioni, consulta [Specifiche JSP EL](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). Il gestore di espressioni lato client non supporta determinate variabili e funzioni nella specifica JSP EL, in particolare:

* Indici di raccolta e chiavi di mappatura (utilizzando [] notation) non sono supportate nei nomi delle variabili per le espressioni valutate sul lato client.
* Di seguito sono riportati i tipi di parametri o i tipi restituiti di funzioni utilizzati nelle espressioni:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Intero
   * java.util.list
   * java.lang.Short
   * Breve
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Doppio
   * java.lang.Long
   * Lungo
   * java.lang.Float
   * Mobile
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### Funzione remota {#remote-function}

Le funzioni remote consentono di utilizzare una logica personalizzata nelle espressioni. È possibile scrivere una logica personalizzata da utilizzare nell’espressione come metodo in Java e la stessa funzione può essere utilizzata all’interno delle espressioni. Le funzioni remote disponibili sono elencate nella scheda &quot;Funzioni remote&quot; sul lato sinistro di Expression Editor.

![remotefunction](assets/remotefunction.png)

#### Aggiunta di funzioni remote personalizzate {#adding-custom-remote-functions}

Puoi creare un bundle personalizzato per esportare le funzioni remote da utilizzare all’interno delle espressioni. Per creare un bundle personalizzato per esportare le funzioni remote, effettuare le seguenti operazioni. Viene illustrato come scrivere una funzione personalizzata che maiuscole la relativa stringa di input.

1. Definisci un’interfaccia per il servizio OSGi contenente i metodi che vengono esportati per l’utilizzo da parte di Gestione espressioni.
1. Dichiara i metodi sull’interfaccia A e aggiungi loro annotazioni con l’annotazione @ServiceMethod (com.adobe.exm.expeval.ServiceMethod). Expression Manager ignora eventuali metodi non annotati. È inoltre possibile specificare i seguenti attributi facoltativi per l&#39;annotazione ServiceMethod:

   1. **Abilitato**: determina se questo metodo è abilitato. Expression Manager ignora i metodi disabilitati.
   1. **familyId**: specifica la famiglia (gruppo) del metodo. Se vuoto, Gestione espressioni presuppone che il metodo appartenga alla famiglia predefinita. Non esiste un registro di famiglie (ad eccezione di quello predefinito) da cui vengono scelte le funzioni. Expression Manager crea in modo dinamico il Registro di sistema creando un’unione di tutti gli ID di famiglia specificati da tutte le funzioni esportate dai vari bundle. Assicurati che l’ID qui specificato sia ragionevolmente leggibile, poiché viene visualizzato anche nell’interfaccia utente di creazione delle espressioni.
   1. **displayName**: nome leggibile della funzione. Questo nome viene utilizzato a scopo di visualizzazione nell’interfaccia utente di authoring. Se vuoto, Expression Manager crea un nome predefinito utilizzando il prefisso e il nome locale della funzione.
   1. **Descrizione**: descrizione dettagliata della funzione. Questa descrizione viene utilizzata a scopo di visualizzazione nell’interfaccia utente di authoring. Se vuoto, Expression Manager crea una descrizione predefinita utilizzando il prefisso e il nome locale della funzione.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   I parametri dei metodi possono anche essere facoltativamente annotati utilizzando l’annotazione @ServiceMethodParameter (com.adobe.exm.expeval.ServiceMethodParameter). Questa annotazione viene utilizzata solo per specificare nomi leggibili dall’utente e descrizioni dei parametri dei metodi da utilizzare nell’interfaccia utente di creazione. Assicurati che i parametri e i valori restituiti dei metodi di interfaccia appartengano a uno dei seguenti tipi:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Intero
   * java.lang.Short
   * Breve
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Doppio
   * java.lang.Long
   * Lungo
   * java.lang.Float
   * Mobile
   * java.util.Calendar
   * java.util.Date
   * java.util.List

1. Definisci l’implementazione dell’interfaccia, configurala come servizio OSGI e definisci le seguenti proprietà del servizio:

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

La voce exm.service=true indica a Gestione espressioni che il servizio contiene funzioni remote idonee per l&#39;utilizzo nelle espressioni. Il &lt;service_id> il valore deve essere un identificatore Java valido (alfanumerico,$, _ senza altri caratteri speciali). Questo valore, preceduto dalla parola chiave REMOTE_, forma il prefisso utilizzato all&#39;interno delle espressioni. Ad esempio, è possibile fare riferimento a un&#39;interfaccia con una barra dei metodi con annotazioni e l&#39;ID del servizio nelle proprietà del servizio all&#39;interno delle espressioni utilizzando REMOTE_foo:bar().

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

Di seguito sono riportati alcuni archivi di esempio da utilizzare:

* **GoodFunctions.jar.zip** è il file jar con un bundle contenente un esempio di definizione di funzione remota. Scarica il file GoodFunctions.jar.zip e decomprimi per ottenere il file jar.
* **GoodFunctions.zip** è il pacchetto di codice sorgente per la definizione di una funzione remota personalizzata e la creazione di un bundle per essa.

GoodFunctions.jar.zip

[Ottieni file](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Ottieni file](assets/goodfunctions.zip)
