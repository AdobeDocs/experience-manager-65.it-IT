---
title: Interfaccia utente di Recommendations per i clienti
description: Elenco di consigli relativi alle interfacce utente classiche e ottimizzate per il tocco.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Interfaccia utente di Recommendations per i clienti{#user-interface-recommendations-for-customers}

Adobe Experience Manager viene fornito con due interfacce: l’interfaccia utente Experience Cloud unificata (nota anche come interfaccia touch) e l’interfaccia classica.

Questo documento ha lo scopo di guidare i clienti nella scelta dell’interfaccia utente da utilizzare a seconda della loro situazione.

Condizioni di interesse:

* **Interfaccia utente (o interfaccia standard)**
Interfaccia utente moderna introdotta in 5.6.0 come anteprima tecnologica ed estesa nelle versioni successive. Si basa sull’esperienza utente unificata per Adobe Experience Cloud, precedentemente nota come interfaccia touch o interfaccia touch.

* **Interfaccia classica**
Interfaccia utente basata sulla tecnologia ExtJS introdotta con CQ 5.1 nel 2008.

* **Amministratore sito**
Funzionalità per gestire la gerarchia del sito (spostare, attivare, gestire riferimenti) e creare nuove pagine.

* **Authoring delle pagine**
Funzionalità per aggiungere/modificare il contenuto di una pagina.

* **Amministratore DAM/Assets**
Funzionalità per gestire le risorse digitali (tra cui immagini, video, documenti, download).

* **ContextHub**
Funzionalità per aggregare informazioni sul visitatore e utilizzarlo per vari scopi. Fornisce un&#39;interfaccia utente per simulare le persone che visitano il sito. A partire da AEM 6.2, ContextHub ha sostituito la tecnologia precedente, Client Context.

## Generale {#general}

Negli ultimi anni Adobe ha aggiornato tutte le soluzioni Adobe Experience Cloud con un’interfaccia utente unificata. Gli utenti delle soluzioni di Experience Cloud godono di un’esperienza coerente con i pattern comuni su come utilizzare e utilizzare le applicazioni. A ogni versione, Adobe ha perfezionato la propria interfaccia utente in base al feedback ricevuto dai clienti che lavorano sulle varie soluzioni.

L’interfaccia utente originale per Adobe Experience Manager (precedentemente nota come CQ5), introdotta nel 2008 e utilizzata dai clienti che eseguono le versioni 5.0-5.6.1, è presente in AEM 6.5. In questo modo i clienti possono eseguire l’aggiornamento alla versione 6.5 e beneficiare di una piattaforma aggiornata con nuove funzionalità, continuando a utilizzare la stessa interfaccia utente.

L’Adobe consiglia ai clienti di pianificare il passaggio alla nuova interfaccia utente nel 2018/19. Questa operazione può essere eseguita durante l’aggiornamento alla versione 6.5 oppure in progetti separati dopo l’aggiornamento, che includerebbero le modifiche necessarie alle finestre di dialogo delle personalizzazioni e dei componenti.

L’interfaccia classica è stata rimossa con AEM 6.4 e Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia classica. L’interfaccia classica rimane completamente supportata anche se è obsoleta.

### Regole e Recommendations {#rules-and-recommendations}

Di seguito è riportato un elenco di consigli di Product Management per Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Il mio progetto...</th>
   <th>Consigli</th>
  </tr>
  <tr>
   <td>Sta iniziando a utilizzare Adobe Experience Manager.</td>
   <td>Utilizza l’interfaccia utente predefinita.</td>
  </tr>
  <tr>
   <td><p>Ha usato l'AEM per un po'.</p> <p>Ha utilizzato l’interfaccia utente del prodotto pronta all’uso e ha sviluppato componenti personalizzati per i siti.<br /> </p> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per amministrazione sito, risorse, .. ecc.<br /> </li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia utente classica. Consulta <a href="#selecting-your-ui">Selezione dell’interfaccia utente</a>.</li>
    </ol> <p>Quindi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato della finestra di dialogo Coral 3. L’Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">Strumenti di modernizzazione AEM</a> per aggiornare i componenti.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creato un sito che utilizza il ClientContext con integrazioni.<br /> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per amministrazione sito, risorse, .. ecc.</li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia utente classica. Consulta <a href="#selecting-your-ui">Selezione dell’interfaccia utente</a>.</li>
    </ol> <p>Quindi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato della finestra di dialogo Coral 3. L’Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">Strumenti di modernizzazione AEM</a> per aggiornare i componenti.</li>
     <li>Configura ContextHub (il sostituto del ClientContext) e aggiorna i modelli di pagina per utilizzare ContextHub. ContextHub dispone di una modalità di compatibilità che consente di caricare archivi di ClientContext personalizzati.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha usato CQ/AEM per molti anni.</p> <p>Ha esteso l’interfaccia utente del prodotto (ad esempio, Amministratore sito) e creato componenti con ampie finestre di dialogo per modifica.</p> </td>
   <td><p>Esegui l’aggiornamento alla versione 6.5 e configura l’interfaccia classica come predefinita per l’authoring delle pagine per tutti gli utenti. Consulta <a href="#selecting-your-ui">Selezione dell’interfaccia utente</a>.</p> <p>Quindi avvia un progetto per applicare la personalizzazione e ottimizzare le finestre di dialogo dei componenti in formato Coral 3. Consulta <a href="#resources-to-help">Risorse per l’Aiuto</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Domande frequenti {#faq}

Consulta l’articolo della Knowledge Base, [Domande frequenti sull’authoring dell’interfaccia touch](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), per dettagli, comprese eventuali informazioni sulla pianificazione obsoleta per l’interfaccia classica.

### Selezione dell’interfaccia utente {#selecting-your-ui}

Consulta [Selezione dell’interfaccia utente](/help/sites-authoring/select-ui.md) per informazioni sulla configurazione del sistema in base alle esigenze.

### Stato interfaccia touch {#touch-enabled-ui-status}

Per informazioni dettagliate sui miglioramenti apportati all’interfaccia utente touch in AEM 6.5, consulta [Novità](/help/release-notes/release-notes.md#what-s-new) nelle Note sulla versione.

Panoramica completa consulta [Stato delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md) pagina

### Risorse per l’Aiuto {#resources-to-help}

Per informazioni di base sulla manipolazione di base:

* [Authoring delle pagine](/help/sites-authoring/page-authoring.md).

Per informazioni dettagliate sullo sviluppo:

* [Architettura dell’interfaccia touch](/help/sites-developing/touch-ui-concepts.md).
* Utilizza il [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) per convertire le finestre di dialogo di modifica dei componenti dall’interfaccia classica all’interfaccia touch.

* [Struttura dell’interfaccia touch](/help/sites-developing/touch-ui-structure.md).

* [Personalizzazione delle console nell’interfaccia touch](/help/sites-developing/customizing-consoles-touch.md) (include il codice di esempio).

* [Personalizzazione dell’authoring delle pagine nell’interfaccia utente touch](/help/sites-developing/customizing-page-authoring-touch.md) (include il codice di esempio).

* [Documentazione dell’interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
