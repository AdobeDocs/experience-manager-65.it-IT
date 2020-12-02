---
title: Suggerimenti sulla codifica
seo-title: Suggerimenti sulla codifica
description: Suggerimenti per la codifica dei AEM
seo-description: Suggerimenti per la codifica dei AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---


# Suggerimenti per la codifica{#coding-tips}

## Usare il più possibile taglibs o HTL {#use-taglibs-or-htl-as-much-as-possible}

L&#39;inclusione di script in JSP rende difficile il debug dei problemi nel codice. Inoltre, includendo gli script in JSP, è difficile separare la logica aziendale dal livello di visualizzazione, che è una violazione del principio di responsabilità singola e del modello di progettazione MVC.

### Codice leggibile in scrittura {#write-readable-code}

Il codice viene scritto una volta, ma letto più volte. Trascorrere un po &#39;di tempo in avanti per pulire il codice che scriviamo pagherà i dividendi lungo la strada come noi e altri sviluppatori hanno bisogno di leggerlo più tardi.

### Scegliere i nomi di rivelazione delle intenzioni {#choose-intention-revealing-names}

Idealmente, un altro programmatore non dovrebbe dover aprire un modulo per capire cosa fa. Allo stesso modo, dovrebbero essere in grado di capire cosa fa un metodo senza leggerlo. Meglio possiamo abbonarci a queste idee, più facile sarà leggere il nostro codice e più velocemente saremo in grado di scrivere e cambiare il nostro codice.

Nella base di codici AEM sono utilizzate le seguenti convenzioni:


* Un&#39;unica implementazione di un&#39;interfaccia è denominata `<Interface>Impl`, ovvero `ReaderImpl`.
* Più implementazioni di un&#39;interfaccia sono denominate `<Variant><Interface>`, ovvero `JcrReader` e `FileSystemReader`.
* Le classi di base astratte sono denominate `Abstract<Interface>` o `Abstract<Variant><Interface>`.
* I pacchetti sono denominati `com.adobe.product.module`.  Ogni manufatto Maven o bundle OSGi deve avere un proprio pacchetto.
* Le implementazioni Java vengono inserite in un pacchetto impl sotto la relativa API.


Tenete presente che queste convenzioni non devono necessariamente essere applicate alle implementazioni dei clienti, ma è importante che le convenzioni siano definite e rispettate in modo che il codice possa essere mantenuto.

Idealmente, i nomi dovrebbero rivelare le loro intenzioni. Un test comune del codice per i nomi che non sono chiari come dovrebbero essere è la presenza di commenti che spiegano a cosa serve la variabile o il metodo:

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
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Non ripetere {#don-t-repeat-yourself}

DRY afferma che lo stesso set di codici non deve mai essere duplicato. Questo vale anche per cose come i letterali stringa. La duplicazione del codice apre la porta a difetti ogni volta che qualcosa deve cambiare e deve essere ricercato ed eliminato.

### Evitare regole CSS nude {#avoid-naked-css-rules}

Le regole CSS devono essere specifiche per l&#39;elemento di destinazione nel contesto dell&#39;applicazione. Ad esempio, una regola CSS applicata a *.content.center* sarebbe troppo ampia e potrebbe potenzialmente avere un impatto su un sacco di contenuto nel sistema, richiedendo ad altri di ignorare questo stile in futuro. *.myapp-* centertextè una regola più specifica in quanto specifica il  ** testo centrato nel contesto dell&#39;applicazione.

### Eliminazione dell&#39;utilizzo di API obsolete {#eliminate-usage-of-deprecated-apis}

Quando un&#39;API è obsoleta, è sempre meglio trovare il nuovo approccio consigliato invece di affidarsi all&#39;API obsoleta. In questo modo, gli aggiornamenti saranno più fluidi in futuro.

### Scrivi codice localizzabile {#write-localizable-code}

Le stringhe che non vengono fornite da un autore devono essere racchiuse in una chiamata al dizionario i18n di AEM tramite *I18n.get()* in JSP/Java e *CQ.I18n.get()* in JavaScript. Questa implementazione restituirà la stringa che gli è stata passata se non viene trovata alcuna implementazione, quindi offre la flessibilità di implementare la localizzazione dopo l&#39;implementazione delle funzionalità nella lingua primaria.

### Escape resource path for security {#escape-resource-paths-for-safety}

Mentre i percorsi nel JCR non devono contenere spazi, la loro presenza non deve causare l&#39;interruzione del codice. Jackrabbit fornisce una classe di utilità Testo con i metodi *escape()* e *escapePath()*. Per i JSP, l&#39;interfaccia Granite espone una funzione *granite:encodeURIPath() EL*.

### Utilizzate l&#39;API XSS e/o l&#39;HTL per proteggere dagli attacchi di script tra siti {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM fornisce un&#39;API XSS per pulire facilmente i parametri e garantire la sicurezza dagli attacchi di script tra siti. Inoltre, HTL ha queste protezioni integrate direttamente nel linguaggio di modellazione. Un foglio di supporto API è disponibile per il download all&#39;indirizzo [Sviluppo - Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementare la registrazione appropriata {#implement-appropriate-logging}

Per il codice Java, AEM supporta slf4j come API standard per la registrazione dei messaggi e dovrebbe essere utilizzato insieme alle configurazioni rese disponibili tramite la console OSGi per garantire la coerenza dell&#39;amministrazione. Slf4j espone cinque diversi livelli di registrazione. Per scegliere quale livello registrare un messaggio, consigliamo di utilizzare le seguenti linee guida:

* ERRORE: Quando un elemento è danneggiato nel codice e l&#39;elaborazione non può continuare. Ciò si verificherà spesso a seguito di un&#39;eccezione imprevista. In genere è utile includere tracce di stack in questi scenari.
* AVVISO: Quando qualcosa non funziona correttamente, ma l&#39;elaborazione può continuare. Spesso questo è il risultato di un&#39;eccezione prevista, ad esempio *PathNotFoundException*.
* INFORMAZIONI: Informazioni utili per il monitoraggio di un sistema. Tieni presente che questa è l&#39;impostazione predefinita e che la maggior parte dei clienti lascerà tale impostazione agli ambienti. Pertanto, non utilizzarla eccessivamente.
* DEBUG: Informazioni di livello inferiore sull&#39;elaborazione. Utile quando si esegue il debug di un problema con il supporto.
* TRACE: Le informazioni di livello più basso, ad esempio i metodi di immissione/uscita. In genere questo viene utilizzato solo dagli sviluppatori.

Nel caso di JavaScript, *console.log* deve essere utilizzato solo durante lo sviluppo e tutte le istruzioni di registro devono essere rimosse prima del rilascio.

### Evitare la programmazione di cult cargo {#avoid-cargo-cult-programming}

Evitate di copiare il codice senza comprendere cosa fa. In caso di dubbi, è sempre meglio chiedere a qualcuno che ha più esperienza con il modulo o l&#39;API su cui non si è chiari.
