---
title: Funzioni remote in Generatore di espressioni
seo-title: Generatore di espressione
description: Generatore di espressioni in Gestione corrispondenza consente di creare espressioni e funzioni remote.
seo-description: Generatore di espressioni in Gestione corrispondenza consente di creare espressioni e funzioni remote.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---


# Funzioni remote in Generatore di espressioni{#remote-functions-in-expression-builder}

Utilizzando il Generatore di espressioni, è possibile creare espressioni o condizioni che eseguono calcoli sui valori dei dati forniti dal Dizionario dati o dagli utenti finali. Gestione corrispondenza utilizza il risultato della valutazione delle espressioni per selezionare risorse quali testo, immagini, elenchi e condizioni e inserirle nella corrispondenza come necessario.

## Creazione di espressioni e funzioni remote con il generatore di espressioni {#creating-expressions-and-remote-functions-with-expression-builder}

Il Generatore di espressioni utilizza internamente le librerie JSP EL, pertanto l&#39;espressione è conforme alla sintassi JSPEL. Per ulteriori informazioni, vedere [Espressioni](#exampleexpressions)di esempio.

![Generatore di espressione](assets/expressionbuilder.png)

### Operatori {#operators}

Gli operatori disponibili per l&#39;uso nelle espressioni sono disponibili nella barra superiore del generatore di espressioni.

### Espressioni di esempio {#exampleexpressions}

Di seguito sono riportati alcuni esempi JSP EL comunemente utilizzati per la soluzione di gestione della corrispondenza:

* Per aggiungere due numeri: ${number1 + number2}
* Per concatenare due stringhe: ${str1} ${str2}
* Per confrontare due numeri: ${age &lt; 18}

Per ulteriori informazioni, consulta la specifica [EL](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)JSP. Il gestore di espressioni lato client non supporta determinate variabili e funzioni nella specifica JSP EL, in particolare:

* Gli indici delle raccolte e le chiavi di mappa (utilizzando la [] notazione) non sono supportati nei nomi delle variabili per le espressioni valutate sul lato client.
* Di seguito sono riportati i tipi di parametro o i tipi di restituzione delle funzioni utilizzate nelle espressioni:

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

Le funzioni remote consentono di utilizzare la logica personalizzata nelle espressioni. È possibile scrivere logica personalizzata da utilizzare come metodo in Java e all&#39;interno di espressioni è possibile utilizzare la stessa funzione. Le funzioni remote disponibili sono elencate nella scheda &quot;Funzioni remote&quot; sul lato sinistro dell&#39;Editor espressioni.

![remotefunction](assets/remotefunction.png)

#### Aggiunta di funzioni remote personalizzate {#adding-custom-remote-functions}

È possibile creare un bundle personalizzato per esportare le proprie funzioni remote da utilizzare all&#39;interno di espressioni. Per creare un bundle personalizzato per esportare le proprie funzioni remote, eseguire le operazioni seguenti. Viene illustrato come scrivere una funzione personalizzata in grado di capitalizzare la stringa di input.

1. Definire un&#39;interfaccia per il servizio OSGi contenente i metodi che vengono esportati per l&#39;utilizzo da Expression Manager.
1. Dichiarare i metodi sull&#39;interfaccia A e annotarli con l&#39;annotazione @ServiceMethod (com.adobe.exm.expeval.ServiceMethod). Expression Manager ignora eventuali metodi non annotati. L&#39;annotazione ServiceMethod ha i seguenti attributi facoltativi che è possibile specificare anche:

   1. **Abilitato**: Determina se questo metodo è abilitato. Expression Manager ignora i metodi disattivati.
   1. **familyId**: Specifica la famiglia del metodo (gruppo). Se vuoto, Expression Manager presuppone che il metodo appartenga alla famiglia predefinita. Non esiste un registro delle famiglie (ad eccezione di quello predefinito) da cui vengono scelte le funzioni. Expression Manager crea dinamicamente il Registro di sistema, unendo tutti gli ID familiari specificati da tutte le funzioni esportate dai vari bundle. Assicurarsi che l’ID qui specificato sia ragionevolmente leggibile, in quanto viene visualizzato anche nell’interfaccia utente di authoring delle espressioni.
   1. **displayName**: Un nome leggibile dall&#39;utente per la funzione. Questo nome viene utilizzato per la visualizzazione nell’interfaccia utente di authoring. Se vuoto, Expression Manager crea un nome predefinito utilizzando il prefisso della funzione e il nome locale.
   1. **Descrizione**: Una descrizione dettagliata della funzione. Questa descrizione viene utilizzata per la visualizzazione nell’interfaccia utente di authoring. Se vuoto, Expression Manager crea una descrizione predefinita utilizzando il prefisso della funzione e il nome locale.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   I parametri dei metodi possono anche essere annotati facoltativamente utilizzando l&#39;annotazione @ServiceMethodParameter (com.adobe.exm.expeval.ServiceMethodParameter). Questa annotazione viene utilizzata solo per specificare nomi leggibili e descrizioni dei parametri dei metodi da utilizzare nell’interfaccia utente di authoring. Assicurarsi che i parametri e i valori restituiti dei metodi di interfaccia appartengano a uno dei seguenti tipi:

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


1. Definite l&#39;implementazione dell&#39;interfaccia, configuratela come servizio OSGI e definite le seguenti proprietà del servizio:

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

La voce exm.service=true indica a Expression Manager che il servizio contiene funzioni remote utilizzabili nelle espressioni. Il valore &lt;service_id> deve essere un identificatore Java valido (alfanumerico,$, _ senza altri caratteri speciali). Questo valore, con il prefisso della parola chiave REMOTE_, forma il prefisso utilizzato all&#39;interno delle espressioni. Ad esempio, un&#39;interfaccia con un metodo annotato bar() e l&#39;ID del servizio foo nelle proprietà del servizio, può essere utilizzata come riferimento all&#39;interno di espressioni utilizzando REMOTE_foo:bar().

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

Di seguito sono riportati alcuni esempi di archivi da utilizzare:

* **GoodFunctions.jar.zip** è il file jar con bundle contenente una definizione di funzione remota di esempio. Scaricate il file GoodFunctions.jar.zip e decomprimetelo per ottenere il file jar.
* **GoodFunctions.zip** è il pacchetto di codice sorgente per la definizione di una funzione remota personalizzata e la creazione di un bundle per essa.

GoodFunctions.jar.zip

[Ottieni file](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Ottieni file](assets/goodfunctions.zip)
