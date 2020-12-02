---
title: Interfaccia utente Recommendations per clienti
seo-title: Interfaccia utente Recommendations per clienti
description: Un elenco di raccomandazioni relative alle interfacce utente classiche e ottimizzate per il tocco.
seo-description: Un elenco di raccomandazioni relative alle interfacce utente classiche e ottimizzate per il tocco.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---


# Recommendations interfaccia utente per clienti{#user-interface-recommendations-for-customers}

Adobe Experience Manager viene fornito con due interfacce utente: l’interfaccia utente unificata del Experience Cloud  (detta interfaccia touch) e l’interfaccia classica.

Questo documento è pensato per guidare i clienti nella scelta dell’interfaccia da utilizzare a seconda della loro situazione.

Termini di interesse:

* **Interfaccia utente (o interfaccia standard)Interfaccia utente**
moderna introdotta in 5.6.0 come anteprima tecnologica ed estesa nelle versioni successive. Si basa sull’esperienza utente unificata di Adobe Experience Cloud, precedentemente nota come interfaccia touch o interfaccia touch.

* **Interfaccia classica**
UIUser basata sulla tecnologia ExtJS introdotta con CQ 5.1 nel 2008.

* **Site**
AdminCapabilities per gestire la gerarchia del sito (spostamento, attivazione, riferimenti gestiti) e creare nuove pagine.

* **Page**
AuthoringFunzionalità per aggiungere o modificare il contenuto di una pagina.

* **DAM/Assets**
AdminFunzionalità per la gestione delle risorse digitali (immagini, video, documenti, download).

* ****
ContextHubCapabilities per aggregare le informazioni sul visitatore e utilizzarle per vari scopi. Fornisce un&#39;interfaccia utente per simulare le persone che visitano il sito. A partire da AEM 6.2, ContextHub ha sostituito la tecnologia precedente, ClientContext.

## Generale {#general}

Negli ultimi anni  Adobe ha aggiornato tutte le soluzioni Adobe Experience Cloud con un&#39;interfaccia utente unificata. Gli utenti di tutte le soluzioni  Experience Cloud godono di un&#39;esperienza coerente con pattern comuni su come utilizzare e utilizzare le applicazioni. Con ogni versione,  Adobe ha perfezionato l&#39;interfaccia utente in base al feedback ricevuto dai clienti che lavoravano tra le varie soluzioni.

L’interfaccia utente originale per Adobe Experience Manager (precedentemente nota come CQ5), introdotta nel 2008 e utilizzata dai clienti con versioni 5.0-5.6.1, è presente nella AEM 6.5. Questo garantisce che i clienti possano effettuare l&#39;aggiornamento alla versione 6.5 e beneficiare di una piattaforma aggiornata con nuove funzionalità, continuando a utilizzare la stessa interfaccia utente.

 Adobe consiglia ai clienti di passare alla nuova interfaccia nel 2018/19. Questo può essere fatto durante l’aggiornamento alla versione 6.5 oppure in un progetto separato dopo l’aggiornamento, che includerà le modifiche necessarie alle finestre di dialogo delle personalizzazioni e dei componenti.

L’interfaccia classica era obsoleta con AEM 6.4 e  Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia classica. Nota: l’interfaccia utente classica rimane completamente supportata anche se obsoleta.

### Regole e Recommendations {#rules-and-recommendations}

Di seguito è riportato un elenco di raccomandazioni di Product Management per Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Il mio progetto...</th>
   <th>Consigli</th>
  </tr>
  <tr>
   <td>Sto iniziando a usare Adobe Experience Manager.</td>
   <td>Utilizzare l'interfaccia utente predefinita.</td>
  </tr>
  <tr>
   <td><p>Ha usato AEM per un po'.</p> <p>Ha utilizzato l'interfaccia utente del prodotto e sviluppato componenti personalizzati per i siti.<br /> </p> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Usa l’interfaccia utente predefinita per l’amministrazione del sito, le risorse, ... etc.<br /> </li>
     <li>Configura l’azione "Modifica pagina" per aprire l’editor classico delle pagine dell’interfaccia utente. Vedere <a href="#selecting-your-ui">Selezione dell'interfaccia utente</a>.</li>
    </ol> <p>Quindi, in una seconda fase:</p>
    <ol>
     <li>Aggiornate le finestre di dialogo dei componenti per utilizzare il formato di dialogo Coral 3.  Adobe consiglia di utilizzare <a href="/help/sites-developing/dialog-conversion.md">Dialog Conversion Tool</a> per aggiornare i componenti.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creato un sito che utilizza il ClientContext con integrazioni.<br /> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Usa l’interfaccia utente predefinita per l’amministrazione del sito, le risorse, ... etc.</li>
     <li>Configura l’azione "Modifica pagina" per aprire l’editor classico delle pagine dell’interfaccia utente. Vedere <a href="#selecting-your-ui">Selezione dell'interfaccia utente</a>.</li>
    </ol> <p>Quindi, in una seconda fase:</p>
    <ol>
     <li>Aggiornate le finestre di dialogo dei componenti per utilizzare il formato di dialogo Coral 3.  Adobe consiglia di utilizzare <a href="/help/sites-developing/dialog-conversion.md">Dialog Conversion Tool</a> per aggiornare i componenti.</li>
     <li>Configurate ContextHub (la sostituzione del ClientContext) e aggiornate i modelli di pagina per utilizzare ContextHub. ContextHub dispone di una modalità di compatibilità che consente il caricamento di store di ClientContext personalizzati.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha utilizzato CQ/AEM per molti anni.</p> <p>Ha esteso l'interfaccia utente del prodotto (ad esempio Amministratore sito) e integrato componenti con ampie finestre di dialogo per la modifica.</p> </td>
   <td><p>Aggiornamento alla versione 6.5 e configurazione dell’interfaccia classica come impostazione predefinita per l’authoring delle pagine per tutti gli utenti. Vedere <a href="#selecting-your-ui">Selezione dell'interfaccia utente</a>.</p> <p>Quindi avviate un progetto per applicare la personalizzazione e ottimizzare le finestre di dialogo dei componenti in formato Coral 3. Vedere <a href="#resources-to-help">Risorse per la Guida</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Domande frequenti {#faq}

Per informazioni, consultate l&#39;articolo della Knowledge Base, [Domande frequenti sull&#39;authoring con l&#39;interfaccia utente touch](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html); incluse eventuali informazioni sulla pianificazione obsoleta dell’interfaccia classica.

### Selezione dell&#39;interfaccia {#selecting-your-ui}

Per informazioni sulla configurazione del sistema, vedere [Selezione dell&#39;interfaccia utente](/help/sites-authoring/select-ui.md).

### Stato interfaccia utente touch {#touch-enabled-ui-status}

Per informazioni dettagliate sui miglioramenti apportati all&#39;interfaccia touch nella AEM 6.5, consultate [Novità](/help/release-notes/release-notes.md#what-s-new) nelle note sulla versione.

Panoramica completa: vedere la pagina [Stato delle funzioni dell&#39;interfaccia utente touch](/help/release-notes/touch-ui-features-status.md)

### Risorse per la Guida {#resources-to-help}

Per informazioni di base sulla gestione di base:

* [Authoring delle pagine](/help/sites-authoring/page-authoring.md).

Per informazioni dettagliate sullo sviluppo:

* [Architettura](/help/sites-developing/touch-ui-concepts.md) dell’interfaccia touch.
* Utilizzate lo [strumento di conversione finestra di dialogo](/help/sites-developing/dialog-conversion.md) per convertire le finestre di dialogo di modifica dei componenti dall’interfaccia classica all’interfaccia touch.

* [Struttura dell’interfaccia](/help/sites-developing/touch-ui-structure.md) touch.

* [Personalizzazione delle console nell’interfaccia](/help/sites-developing/customizing-consoles-touch.md)  touch (include un esempio di codice).

* [Personalizzazione dell’authoring delle pagine nell’interfaccia](/help/sites-developing/customizing-page-authoring-touch.md)  touch (include un esempio di codice).

* [AEM sessione Gem sulla personalizzazione](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html) touch.
* [Documentazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) sull’interfaccia utente Granite.

