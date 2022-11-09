---
title: Interfaccia utente Recommendations per clienti
seo-title: User Interface Recommendations for Customers
description: Un elenco di consigli relativi alle interfacce utente classica e ottimizzata per il tocco.
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 2%

---

# Interfaccia utente Recommendations per clienti{#user-interface-recommendations-for-customers}

Adobe Experience Manager è dotato di due interfacce: l’interfaccia utente di Experience Cloud unificata (interfaccia touch) e l’interfaccia classica.

Questo documento ha lo scopo di guidare i clienti nella scelta dell’interfaccia da utilizzare a seconda della loro situazione.

Termini di interesse:

* **Interfaccia (o interfaccia standard)**
Interfaccia utente moderna introdotta in 5.6.0 come anteprima tecnologica ed estesa nelle versioni successive. Si basa sull’esperienza utente unificata di Adobe Experience Cloud, precedentemente nota come interfaccia touch o interfaccia touch.

* **Interfaccia classica**
Interfaccia utente basata sulla tecnologia ExtJS introdotta con CQ 5.1 nel 2008.

* **Amministratore del sito**
Possibilità di gestire la gerarchia del sito (spostamento, attivazione, gestione dei riferimenti) e creare nuove pagine.

* **Authoring delle pagine**
Possibilità di aggiungere o modificare il contenuto di una pagina.

* **Amministratore DAM/Assets**
Possibilità di gestire le risorse digitali (incluse immagini, video, documenti, download).

* **ContextHub**
Capacità di aggregare informazioni sul visitatore e di utilizzarle per vari scopi. Fornisce un&#39;interfaccia utente per simulare le persone che visitano il sito. A partire AEM 6.2, ContextHub ha sostituito la tecnologia precedente, Client Context.

## Generale {#general}

Negli ultimi anni Adobe ha aggiornato tutte le soluzioni Adobe Experience Cloud con un&#39;interfaccia utente unificata. Gli utenti di tutte le soluzioni di Experience Cloud godono di un&#39;esperienza coerente con pattern comuni su come utilizzare e utilizzare le applicazioni. Ad ogni versione, Adobe ha perfezionato l’interfaccia utente in base ai feedback ricevuti dai clienti che lavorano tra le varie soluzioni.

L’interfaccia utente originale per Adobe Experience Manager (precedentemente nota come CQ5), introdotta nel 2008 e utilizzata dai clienti che eseguono le versioni 5.0-5.6.1, è presente nella AEM 6.5. Questo garantisce ai clienti la possibilità di eseguire l’aggiornamento alla versione 6.5 e di beneficiare di una piattaforma aggiornata con nuove funzionalità, continuando a utilizzare la stessa interfaccia utente.

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
   <td>Sto solo iniziando a usare Adobe Experience Manager.</td>
   <td>Utilizza l’interfaccia utente predefinita.</td>
  </tr>
  <tr>
   <td><p>Ha usato AEM per un po'.</p> <p>Ha utilizzato l’interfaccia utente del prodotto out-of-the-box e sviluppato componenti personalizzati per i siti.<br /> </p> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per l’amministrazione del sito, le risorse .. ecc.<br /> </li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia classica. Vedi <a href="#selecting-your-ui">Selezione dell’interfaccia</a>.</li>
    </ol> <p>Poi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato di dialogo Coral 3. L'Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">Strumenti di modernizzazione AEM</a> per aggiornare i componenti.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creato un sito che utilizza il ClientContext con le integrazioni.<br /> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per l’amministrazione del sito, le risorse .. ecc.</li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia classica. Vedi <a href="#selecting-your-ui">Selezione dell’interfaccia</a>.</li>
    </ol> <p>Poi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato di dialogo Coral 3. L'Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">Strumenti di modernizzazione AEM</a> per aggiornare i componenti.</li>
     <li>Configura ContextHub (la sostituzione del ClientContext) e aggiorna i modelli di pagina per utilizzare ContextHub. ContextHub dispone di una modalità di compatibilità che consente di caricare archivi di ClientContext personalizzati.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha usato CQ/AEM per molti anni.</p> <p>Ha esteso l’interfaccia utente del prodotto (ad esempio Amministratore sito) e generato componenti con finestre di dialogo di modifica estese.</p> </td>
   <td><p>Aggiorna alla versione 6.5 e configura l’interfaccia classica come impostazione predefinita per l’authoring delle pagine per tutti gli utenti. Vedi <a href="#selecting-your-ui">Selezione dell’interfaccia</a>.</p> <p>Quindi avvia un progetto per applicare la personalizzazione e ottimizzare le finestre di dialogo dei componenti in formato Coral 3. Vedi <a href="#resources-to-help">Risorse per assistenza</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Domande frequenti {#faq}

Vedi l&#39;articolo della Knowledge Base, [Domande frequenti sull’authoring dell’interfaccia utente touch](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), per informazioni dettagliate; incluse eventuali informazioni sulla pianificazione obsoleta dell’interfaccia classica.

### Selezione dell’interfaccia {#selecting-your-ui}

Vedi [Selezione dell’interfaccia](/help/sites-authoring/select-ui.md) per informazioni sulla configurazione del sistema, in base alle esigenze.

### Stato interfaccia touch {#touch-enabled-ui-status}

Per informazioni dettagliate sui miglioramenti apportati all’interfaccia utente touch in AEM 6.5, vedi [Novità](/help/release-notes/release-notes.md#what-s-new) nelle note sulla versione.

Una panoramica completa vedi [Stato delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md) page

### Risorse per assistenza {#resources-to-help}

Per informazioni generali sulla gestione di base:

* [Authoring delle pagine](/help/sites-authoring/page-authoring.md).

Per informazioni dettagliate sullo sviluppo:

* [Architettura dell’interfaccia touch](/help/sites-developing/touch-ui-concepts.md).
* Utilizza la [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) per convertire le finestre di dialogo di modifica dei componenti dall’interfaccia classica all’interfaccia touch.

* [Struttura dell’interfaccia touch](/help/sites-developing/touch-ui-structure.md).

* [Personalizzazione delle console nell’interfaccia touch](/help/sites-developing/customizing-consoles-touch.md) (include il codice di esempio).

* [Personalizzazione dell’authoring delle pagine nell’interfaccia touch](/help/sites-developing/customizing-page-authoring-touch.md) (include il codice di esempio).

* [Documentazione dell’interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
