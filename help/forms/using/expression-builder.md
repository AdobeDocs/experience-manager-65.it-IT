---
title: Funzioni remote in Expression Builder
seo-title: Expression Builder
description: Generatore di espressioni in Gestione Corrispondenza consente di creare espressioni e funzioni remote.
seo-description: Expression Builder in Correspondence Management lets you create expressions and remote functions.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Funzioni remote in Expression Builder{#remote-functions-in-expression-builder}

Utilizzando il Generatore di espressioni, puoi creare espressioni o condizioni che eseguono calcoli sui valori dei dati forniti dal dizionario dati o dagli utenti finali. Gestione della corrispondenza utilizza il risultato della valutazione delle espressioni per selezionare risorse quali testo, immagini, elenchi e condizioni e inserirle nella corrispondenza come necessario.

## Creazione di espressioni e funzioni remote con il generatore di espressioni {#creating-expressions-and-remote-functions-with-expression-builder}

Il Generatore di espressioni utilizza internamente le librerie JSP EL, quindi l’espressione si attiene alla sintassi JSPEL. Per ulteriori informazioni, consulta [Espressioni di esempio](#exampleexpressions).

![Generatore di espressione](assets/expressionbuilder.png)

### Operatori {#operators}

Gli operatori disponibili per l’uso nelle espressioni sono disponibili nella barra superiore del generatore di espressioni.

### Espressioni di esempio {#exampleexpressions}

Di seguito sono riportati alcuni esempi JSP EL comunemente utilizzati che puoi utilizzare nella tua soluzione di gestione della corrispondenza:

* Per aggiungere due numeri: ${numero1 + numero2}
* Per concatenare due stringhe: ${str1} ${str2}
* Per confrontare due numeri: ${age &lt; 18}

Puoi trovare ulteriori informazioni nella sezione [Specifica JSP EL](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). Il gestore di espressioni lato client non supporta determinate variabili e funzioni nella specifica JSP EL, in particolare:

* Indici delle raccolte e chiavi di mappa (utilizzando [] notazione) non sono supportati nei nomi delle variabili per le espressioni valutate sul lato client.
* Di seguito sono riportati i tipi di parametri o i tipi di funzioni restituiti utilizzati nelle espressioni:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
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

Le funzioni remote offrono la possibilità di utilizzare logica personalizzata nelle espressioni. È possibile scrivere una logica personalizzata da utilizzare nell’espressione come metodo in Java e utilizzare la stessa funzione all’interno delle espressioni. Le funzioni remote disponibili sono elencate nella scheda &quot;Funzioni remote&quot; sul lato sinistro di Expression Editor.

![remotefunction](assets/remotefunction.png)

#### Aggiunta di funzioni remote personalizzate {#adding-custom-remote-functions}

Puoi creare un bundle personalizzato per esportare le tue funzioni remote da utilizzare all&#39;interno delle espressioni. Per creare un bundle personalizzato per esportare le proprie funzioni remote, esegui le seguenti attività. Viene illustrato come scrivere una funzione personalizzata che ne capitalizza la stringa di input.

1. Definisci un&#39;interfaccia per il servizio OSGi contenente i metodi che vengono esportati per l&#39;utilizzo da Expression Manager.
1. Dichiara i metodi sull&#39;interfaccia A e annota con l&#39;annotazione @ServiceMethod (com.adobe.exm.expeval.ServiceMethod). Expression Manager ignora eventuali metodi non annotati. L&#39;annotazione ServiceMethod ha i seguenti attributi facoltativi che è possibile specificare anche:

   1. **Abilitato**: Determina se questo metodo è abilitato. Expression Manager ignora i metodi disabilitati.
   1. **familyId**: Specifica la famiglia del metodo (gruppo). Se vuoto, Expression Manager presuppone che il metodo appartenga alla famiglia predefinita. Non esiste un registro delle famiglie (ad eccezione di quello predefinito) da cui vengono scelte le funzioni. Expression Manager crea in modo dinamico il Registro di sistema prendendo un&#39;unione di tutti gli ID familiari specificati da tutte le funzioni esportate dai vari bundle. Assicurati che l’ID qui specificato sia ragionevolmente leggibile, in quanto viene visualizzato anche nell’interfaccia utente per la creazione delle espressioni.
   1. **displayName**: Un nome leggibile dall&#39;utente per la funzione. Questo nome viene utilizzato a scopo di visualizzazione nell’interfaccia utente di authoring. Se vuoto, Expression Manager crea un nome predefinito utilizzando il prefisso e il nome locale della funzione.
   1. **Descrizione**: Descrizione dettagliata della funzione. Questa descrizione viene utilizzata a scopo di visualizzazione nell’interfaccia utente di authoring. Se vuoto, Expression Manager crea una descrizione predefinita utilizzando il prefisso e il nome locale della funzione.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   I parametri dei metodi possono anche essere annotati facoltativamente utilizzando l&#39;annotazione @ServiceMethodParameter (com.adobe.exm.expeval.ServiceMethodParameter). Questa annotazione viene utilizzata solo per specificare nomi e descrizioni leggibili dall’utente dei parametri dei metodi da utilizzare nell’interfaccia utente di authoring. Assicurati che i parametri e i valori restituiti dei metodi di interfaccia appartengano a uno dei seguenti tipi:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
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

La voce exm.service=true indica a Expression manager che il servizio contiene funzioni remote adatte all&#39;uso nelle espressioni. La &lt;service_id> deve essere un identificatore Java valido (alfanumerico,$, _ senza altri caratteri speciali). Questo valore, con il prefisso della parola chiave REMOTE_, forma il prefisso utilizzato all’interno delle espressioni. Ad esempio, è possibile fare riferimento a un&#39;interfaccia con un metodo annotated bar() e l&#39;ID del servizio foo nelle proprietà del servizio all&#39;interno di espressioni utilizzando REMOTE_foo:bar().

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

* **GoodFunctions.jar.zip** è il file jar con bundle contenente una definizione di funzione remota di esempio. Scarica il file GoodFunctions.jar.zip e decomprimilo per ottenere il file jar.
* **GoodFunctions.zip** è il pacchetto di codice sorgente per definire una funzione remota personalizzata e creare un bundle per essa.

GoodFunctions.jar.zip

[Ottieni file](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Ottieni file](assets/goodfunctions.zip)
