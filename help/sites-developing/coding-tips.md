---
title: Suggerimenti sulla codifica
seo-title: Coding Tips
description: Suggerimenti per la codifica dei AEM
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Suggerimenti sulla codifica{#coding-tips}

## Utilizza taglibs o HTL il più possibile {#use-taglibs-or-htl-as-much-as-possible}

L&#39;inclusione degli script in JSP rende difficile il debug dei problemi nel codice. Inoltre, includendo gli script in JSP, è difficile separare la logica di business dal livello di visualizzazione, che è una violazione del principio di responsabilità singola e del modello di progettazione MVC.

### Scrivi codice leggibile {#write-readable-code}

Il codice viene scritto una volta, ma letto molte volte. Trascorrere un po&#39; di tempo in anticipo per pulire il codice che scriviamo pagherà dividendi lungo la strada come noi e altri sviluppatori hanno bisogno di leggerlo più tardi.

### Scegliere i nomi che rivelano le intenzioni {#choose-intention-revealing-names}

Idealmente, un altro programmatore non dovrebbe dover aprire un modulo per capire cosa fa. Allo stesso modo, dovrebbero essere in grado di dire cosa fa un metodo senza leggerlo. Meglio possiamo abbonarci a queste idee, più facile sarà leggere il nostro codice e più velocemente saremo in grado di scrivere e cambiare il nostro codice.

Nella base di codice AEM vengono utilizzate le seguenti convenzioni:


* Viene denominata una singola implementazione di un’interfaccia `<Interface>Impl`, vale a dire `ReaderImpl`.
* Sono denominate più implementazioni di un&#39;interfaccia `<Variant><Interface>`, vale a dire `JcrReader` e `FileSystemReader`.
* Le classi base astratte sono denominate `Abstract<Interface>` o `Abstract<Variant><Interface>`.
* I pacchetti sono denominati `com.adobe.product.module`.  Ogni artefatto Maven o bundle OSGi deve avere un proprio pacchetto.
* Le implementazioni Java vengono inserite in un pacchetto impl sotto la loro API.


Tieni presente che queste convenzioni non devono necessariamente essere applicate alle implementazioni dei clienti, ma è importante che le convenzioni siano definite e rispettate in modo che il codice possa rimanere gestibile.

Idealmente, i nomi dovrebbero rivelare le loro intenzioni. Un test comune del codice per quando i nomi non sono chiari come dovrebbero essere è la presenza di commenti che spiegano a cosa serve la variabile o il metodo:

<table>
 <tbody>
  <tr>
   <td><p><strong>Non chiaro</strong></p> </td>
   <td><p><strong>Cancella</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tempo trascorso in giorni</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//Ottenere immagini con tag<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Non ripeterti  {#don-t-repeat-yourself}

DRY afferma che lo stesso set di codice non deve mai essere duplicato. Questo vale anche per cose come le stringhe letterali. La duplicazione del codice apre la strada ai difetti ogni volta che qualcosa deve cambiare e deve essere ricercato ed eliminato.

### Evitare regole CSS nude {#avoid-naked-css-rules}

Le regole CSS devono essere specifiche per l’elemento di destinazione nel contesto dell’applicazione. Ad esempio, una regola CSS applicata a *.content .center* sarebbe eccessivamente ampio e potrebbe potenzialmente influenzare molti contenuti nel sistema, richiedendo ad altri di ignorare questo stile in futuro. *.myapp-centertext* sarebbe una regola più specifica mentre specifica centrato *text* nel contesto dell&#39;applicazione.

### Eliminazione dell’utilizzo di API obsolete {#eliminate-usage-of-deprecated-apis}

Quando un’API è obsoleta, è sempre meglio trovare il nuovo approccio consigliato invece di basarsi sull’API obsoleta. In questo modo gli aggiornamenti saranno più semplici in futuro.

### Scrivi codice localizzabile {#write-localizable-code}

Le stringhe che non vengono fornite da un autore devono essere racchiuse in una chiamata al dizionario i18n di AEM tramite *I18n.get()* in JSP/Java e *CQ.I18n.get()* in JavaScript. Questa implementazione restituirà la stringa che gli è stata passata se non viene trovata alcuna implementazione, quindi offre la flessibilità di implementare la localizzazione dopo l&#39;implementazione delle funzionalità nella lingua primaria.

### Esci dai percorsi delle risorse per la sicurezza {#escape-resource-paths-for-safety}

Anche se i percorsi nel JCR non devono contenere spazi, la loro presenza non deve causare l&#39;interruzione del codice. Jackrabbit fornisce una classe di utilità di testo con *escape()* e *escapePath()* metodi. Per i JSP, l’interfaccia Granite espone un *granite:encodeURIPath() EL* funzione .

### Utilizza l’API XSS e/o HTL per proteggere dagli attacchi di script tra siti diversi {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM fornisce un’API XSS per pulire facilmente i parametri e garantire la sicurezza dagli attacchi di script tra siti diversi. Inoltre, HTL dispone di queste protezioni integrate direttamente nel linguaggio dei modelli. È disponibile un foglio di supporto API da scaricare all’indirizzo [Sviluppo - Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementare la registrazione appropriata {#implement-appropriate-logging}

Per il codice Java, AEM supporta slf4j come API standard per la registrazione dei messaggi e deve essere utilizzato insieme alle configurazioni rese disponibili tramite la console OSGi per motivi di coerenza nell’amministrazione. Slf4j espone cinque diversi livelli di registrazione. È consigliabile utilizzare le seguenti linee guida quando si sceglie a quale livello registrare un messaggio:

* ERRORE: Quando qualcosa è rotto nel codice e l&#39;elaborazione non può continuare. Questo si verificherà spesso a seguito di un&#39;eccezione imprevista. In genere è utile includere tracce di stack in questi scenari.
* AVVERTENZA: Quando qualcosa non funziona correttamente, ma l&#39;elaborazione può continuare. Questo sarà spesso il risultato di un&#39;eccezione che ci aspettavamo, come *PathNotFoundException*.
* INFORMAZIONI: Informazioni utili per il monitoraggio di un sistema. Tieni presente che questa è l’impostazione predefinita e che la maggior parte dei clienti lo lascerà in posizione nei propri ambienti. Pertanto, non utilizzarlo eccessivamente.
* DEBUG: Informazioni di livello inferiore sull’elaborazione. Utile quando si esegue il debug di un problema con il supporto.
* TRACE: Informazioni di livello più basso, ad esempio metodi di immissione/uscita. In genere questo viene utilizzato solo dagli sviluppatori.

Nel caso di JavaScript, *console.log* deve essere utilizzato solo durante lo sviluppo e tutte le istruzioni di registro devono essere rimosse prima del rilascio.

### Evitare la programmazione di cult cargo {#avoid-cargo-cult-programming}

Evita di copiare il codice senza capire cosa fa. In caso di dubbi, è sempre meglio chiedere a qualcuno che ha più esperienza con il modulo o l’API su cui non sei chiaro.
