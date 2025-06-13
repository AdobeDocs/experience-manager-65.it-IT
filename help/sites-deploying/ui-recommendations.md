---
title: Raccomandazioni in merito all’interfaccia utente per clienti
description: Elenco di consigli relativi alle interfacce utente classiche e ottimizzate per il tocco.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Raccomandazioni in merito all’interfaccia utente per clienti{#user-interface-recommendations-for-customers}

Adobe Experience Manager viene fornito con due interfacce: l’interfaccia utente unificata di Experience Cloud (nota anche come interfaccia touch) e l’interfaccia classica.

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

Negli ultimi anni Adobe ha aggiornato tutte le soluzioni Adobe Experience Cloud con un’interfaccia utente unificata. Gli utenti delle soluzioni Experience Cloud godono di un’esperienza coerente con i pattern comuni su come utilizzare e utilizzare le applicazioni. A ogni rilascio, Adobe ha perfezionato la propria interfaccia utente in base al feedback ricevuto dai clienti che lavorano sulle varie soluzioni.

L’interfaccia utente originale per Adobe Experience Manager (precedentemente nota come CQ5), introdotta nel 2008 e utilizzata dai clienti che eseguono le versioni da 5.0 a 5.6.1, è presente in AEM 6.5. In questo modo i clienti possono eseguire l’aggiornamento alla versione 6.5 e beneficiare di una piattaforma aggiornata con nuove funzionalità, continuando a utilizzare la stessa interfaccia utente.

Adobe consiglia ai clienti di pianificare il passaggio alla nuova interfaccia utente nel 2018/19. Questa operazione può essere eseguita durante l’aggiornamento alla versione 6.5 oppure in progetti separati dopo l’aggiornamento, che includerebbero le modifiche necessarie alle finestre di dialogo delle personalizzazioni e dei componenti.

L’interfaccia classica è stata rimossa con AEM 6.4 e Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia classica. L’interfaccia classica rimane completamente supportata anche se è obsoleta.

### Regole e raccomandazioni {#rules-and-recommendations}

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
   <td><p>Usa AEM da un po’.</p> <p>Ha utilizzato l'interfaccia utente predefinita del prodotto e sviluppato componenti personalizzati per i siti.<br /> </p> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per amministrazione sito, risorse, .. ecc.<br /> </li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia utente classica. Vedi <a href="#selecting-your-ui">Selezione della tua interfaccia utente</a>.</li>
    </ol> <p>Quindi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato della finestra di dialogo Coral 3. Per aggiornare i componenti, Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">Strumenti di modernizzazione AEM</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creato un sito che utilizza ClientContext con integrazioni.<br /> </td>
   <td>
    <ol>
     <li>Aggiornamento a 6.5</li>
     <li>Utilizza l’interfaccia utente predefinita per amministrazione sito, risorse, .. ecc.</li>
     <li>Configura l’azione "Modifica pagina" per aprire l’Editor pagina dell’interfaccia utente classica. Vedi <a href="#selecting-your-ui">Selezione della tua interfaccia utente</a>.</li>
    </ol> <p>Quindi, in una seconda fase:</p>
    <ol>
     <li>Aggiorna le finestre di dialogo dei componenti per utilizzare il formato della finestra di dialogo Coral 3. Per aggiornare i componenti, Adobe consiglia di utilizzare <a href="/help/sites-developing/modernization-tools.md">Strumenti di modernizzazione AEM</a>.</li>
     <li>Configura ContextHub (che sostituisce ClientContext) e aggiorna i modelli di pagina per utilizzare ContextHub. ContextHub dispone di una modalità di compatibilità che consente di caricare archivi ClientContext personalizzati.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Utilizza CQ/AEM da molti anni.</p> <p>Ha esteso l’interfaccia utente del prodotto (ad esempio, Amministratore sito) e creato componenti con ampie finestre di dialogo per modifica.</p> </td>
   <td><p>Esegui l’aggiornamento alla versione 6.5 e configura l’interfaccia classica come predefinita per l’authoring delle pagine per tutti gli utenti. Vedi <a href="#selecting-your-ui">Selezione della tua interfaccia utente</a>.</p> <p>Quindi avvia un progetto per applicare la personalizzazione e ottimizzare le finestre di dialogo dei componenti in formato Coral 3. Consulta <a href="#resources-to-help">Risorse per la Guida</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Selezione dell’interfaccia utente {#selecting-your-ui}

Consulta [Selezione dell&#39;interfaccia utente](/help/sites-authoring/select-ui.md) per informazioni sulla configurazione del sistema in base alle esigenze.

### Stato interfaccia touch {#touch-enabled-ui-status}

Per informazioni dettagliate sui miglioramenti apportati all&#39;interfaccia utente touch in AEM 6.5, vedi [Novità](/help/release-notes/release-notes.md#what-s-new) nelle note sulla versione.

Panoramica completa: visita la pagina [Stato delle funzioni dell&#39;interfaccia utente touch](/help/release-notes/touch-ui-features-status.md)

### Risorse per l’Aiuto {#resources-to-help}

Per informazioni di base sulla manipolazione di base:

* [Authoring delle pagine](/help/sites-authoring/page-authoring.md).

Per informazioni dettagliate sullo sviluppo:

* [Architettura interfaccia utente touch](/help/sites-developing/touch-ui-concepts.md).
* Utilizza [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) per convertire le finestre di dialogo di modifica dei componenti dall&#39;interfaccia classica all&#39;interfaccia touch.

* [Struttura dell&#39;interfaccia utente touch](/help/sites-developing/touch-ui-structure.md).

* [Personalizzazione delle console nell&#39;interfaccia utente touch](/help/sites-developing/customizing-consoles-touch.md) (include il codice di esempio).

* [Personalizzazione dell&#39;authoring delle pagine nell&#39;interfaccia utente touch](/help/sites-developing/customizing-page-authoring-touch.md) (include codice di esempio).

* [Documentazione interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
