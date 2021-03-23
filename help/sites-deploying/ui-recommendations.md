---
title: Interfaccia utente Recommendations per clienti
seo-title: Interfaccia utente Recommendations per clienti
description: Un elenco di consigli relativi alle interfacce utente classica e ottimizzata per il tocco.
seo-description: Un elenco di consigli relativi alle interfacce utente classica e ottimizzata per il tocco.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---


# Interfaccia utente Recommendations per clienti{#user-interface-recommendations-for-customers}

Adobe Experience Manager è dotato di due interfacce: l’interfaccia utente di Experience Cloud unificata (interfaccia touch) e l’interfaccia classica.

Questo documento ha lo scopo di guidare i clienti nella scelta dell’interfaccia da utilizzare a seconda della loro situazione.

Termini di interesse:

* **Interfaccia utente (o interfaccia standard)**
Interfaccia utente moderna introdotta in 5.6.0 come anteprima di tecnologia ed estesa nelle versioni successive. Si basa sull’esperienza utente unificata di Adobe Experience Cloud, precedentemente nota come interfaccia touch o interfaccia touch.

* **Interfaccia classica**
UIUser basata sulla tecnologia ExtJS introdotta con CQ 5.1 nel 2008.

* **Site**
AdminCapabilities per gestire la gerarchia del sito (spostare, attivare, gestire i riferimenti) e creare nuove pagine.

* **Funzionalità di**
authoring delle pagine per aggiungere/modificare il contenuto di una pagina.

* **Funzionalità**
amministratore DAM/Assets per gestire le risorse digitali (immagini, video, documenti, download).

* ****
ContextHubCapabilities per aggregare informazioni sul visitatore e utilizzarlo per vari scopi. Fornisce un&#39;interfaccia utente per simulare le persone che visitano il sito. A partire AEM 6.2, ContextHub ha sostituito la tecnologia precedente, Client Context.

## Generale {#general}

Negli ultimi anni Adobe ha aggiornato tutte le soluzioni Adobe Experience Cloud con un&#39;interfaccia utente unificata. Gli utenti di tutte le soluzioni di Experience Cloud godono di un&#39;esperienza coerente con pattern comuni su come utilizzare e utilizzare le applicazioni. Ad ogni versione, Adobe ha perfezionato l’interfaccia utente in base ai feedback ricevuti dai clienti che lavorano tra le varie soluzioni.

L’interfaccia utente originale per Adobe Experience Manager (precedentemente nota come CQ5), introdotta nel 2008 e utilizzata dai clienti che eseguono le versioni 5.0-5.6.1, è presente nella AEM 6.5. Questo garantisce ai clienti la possibilità di eseguire l’aggiornamento alla versione 6.5 e di usufruire di una piattaforma aggiornata con nuove funzionalità, continuando a utilizzare la stessa interfaccia utente.

Adobe consiglia ai clienti di pianificare il passaggio alla nuova interfaccia utente nel 2018/19. Questo può essere fatto durante l&#39;aggiornamento alla versione 6.5 oppure in progetti separati dopo l&#39;aggiornamento, che includerebbero le necessarie modifiche alle personalizzazioni e alle finestre di dialogo dei componenti.

L’interfaccia classica è stata dichiarata obsoleta con AEM 6.4 e Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia classica. Nota: l’interfaccia utente classica rimane completamente supportata anche se obsoleta.

### Regole e Recommendations {#rules-and-recommendations}

Di seguito è riportato un elenco di consigli da Product Management per Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Il mio progetto..</th>
   <th>Consigli</th>
  </tr>
  <tr>
   <td>Sta iniziando a usare Adobe Experience Manager.</td>
   <td>Utilizza l’interfaccia utente predefinita.</td>
  </tr>
  <tr>
   <td><p>Ha usato AEM per un po'.</p> <p>Ha utilizzato l'interfaccia utente del prodotto pronta all'uso e sviluppato componenti personalizzati per i siti.<br /> </p> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per l’amministrazione del sito, le risorse .. etc.<br /> </li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia classica. Consulta <a href="#selecting-your-ui">Selezione dell'interfaccia utente</a>.</li>
    </ol> <p>Poi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato di dialogo Coral 3. Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">AEM Strumenti di modernizzazione</a> per aggiornare i componenti.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creato un sito che utilizza il ClientContext con le integrazioni.<br /> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per l’amministrazione del sito, le risorse .. etc.</li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia classica. Consulta <a href="#selecting-your-ui">Selezione dell'interfaccia utente</a>.</li>
    </ol> <p>Poi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato di dialogo Coral 3. Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">AEM Strumenti di modernizzazione</a> per aggiornare i componenti.</li>
     <li>Configura ContextHub (la sostituzione del ClientContext) e aggiorna i modelli di pagina per utilizzare ContextHub. ContextHub dispone di una modalità di compatibilità che consente di caricare archivi di ClientContext personalizzati.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha usato CQ/AEM per molti anni.</p> <p>Ha esteso l’interfaccia utente del prodotto (ad esempio Amministratore sito) e generato componenti con finestre di dialogo di modifica estese.</p> </td>
   <td><p>Aggiorna alla versione 6.5 e configura l’interfaccia classica come impostazione predefinita per l’authoring delle pagine per tutti gli utenti. Consulta <a href="#selecting-your-ui">Selezione dell'interfaccia utente</a>.</p> <p>Quindi avvia un progetto per applicare la personalizzazione e ottimizzare le finestre di dialogo dei componenti in formato Coral 3. Vedere <a href="#resources-to-help">Risorse per la Guida</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Domande frequenti {#faq}

Per ulteriori informazioni, consulta l’articolo della Knowledge Base [Domande frequenti sull’authoring dell’interfaccia utente touch](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html); incluse eventuali informazioni sulla pianificazione obsoleta dell’interfaccia classica.

### Selezione dell&#39;interfaccia utente {#selecting-your-ui}

Per informazioni sulla configurazione del sistema, consulta [Selezione dell&#39;interfaccia utente](/help/sites-authoring/select-ui.md) .

### Stato interfaccia touch {#touch-enabled-ui-status}

Per informazioni dettagliate sui miglioramenti apportati all’interfaccia utente touch nella AEM 6.5, consulta [Novità](/help/release-notes/release-notes.md#what-s-new) nelle note sulla versione.

Panoramica completa della pagina [Stato delle funzioni dell&#39;interfaccia touch](/help/release-notes/touch-ui-features-status.md)

### Risorse per la Guida {#resources-to-help}

Per informazioni generali sulla gestione di base:

* [Authoring delle pagine](/help/sites-authoring/page-authoring.md).

Per informazioni dettagliate sullo sviluppo:

* [Architettura dell’interfaccia touch](/help/sites-developing/touch-ui-concepts.md).
* Utilizza gli [AEM Strumenti di modernizzazione](/help/sites-developing/modernization-tools.md) per convertire le finestre di dialogo Modifica componente dall’interfaccia classica all’interfaccia touch.

* [Struttura dell’interfaccia touch](/help/sites-developing/touch-ui-structure.md).

* [Personalizzazione delle console nell’interfaccia touch](/help/sites-developing/customizing-consoles-touch.md)  (con codice di esempio).

* [Personalizzazione dell’authoring delle pagine nell’interfaccia touch](/help/sites-developing/customizing-page-authoring-touch.md)  (con codice di esempio).

* [AEM sessione Gem sulla personalizzazione](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html) touch.
* [Documentazione dell’interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

