---
title: Novità in Adobe Experience Manager 6.5 Service Pack 4
description: Novità in Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: da9d682a0392e5de8e012e254fb82bd15547a542

---


# Novità in Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (AEM) 6.5 offre funzioni e miglioramenti continui tramite i Service Pack trimestrali. Il nuovo approccio è vantaggioso per i nostri clienti che adottano le innovazioni più rapidamente.

L’ultimo Service Pack 4 di AEM (6.5.4.0) è stato rilasciato il 5 **marzo 2020**. In questo articolo vengono evidenziate le funzioni offerte dall’ultimo Service Pack per rendere il vostro viaggio AEM più ricco.

## AEM Sites {#aem-sites}

AEM 6.5.4.0 include miglioramenti a Style System. È ora possibile selezionare gli stili nella finestra di dialogo del componente.

### Miglioramenti delle prestazioni in varie aree {#performance-improvements}

* È stato ridotto il tempo necessario per caricare e inizializzare ContextHub in un sito (`contexthub.kernel.js`). Ne risulta un caricamento più rapido delle pagine durante una visita del sito.

* È stato ridotto il tempo necessario per aggiornare una pagina dopo aver trascinato i frammenti esperienza nell’Editor pagina Siti.

* È stato ridotto il tempo di caricamento delle voci in una pagina Siti con più di 200 copie dal vivo in Panoramica **** Live Copy.

* Gestione migliorata degli URL incompleti o non validi. Tali URL possono rallentare l’Editor modelli.

## AEM Assets {#aem-assets}

### Configurare AEM Assets con Brand Portal {#configure-assets-bp}

Il canale di autorizzazione tra Risorse AEM e Portale marchio viene modificato. Precedentemente, Brand Portal era stato configurato nell’interfaccia classica tramite il gateway OAuth legacy, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l’autorizzazione. AEM Assets è ora configurato con Brand Portal tramite Adobe I/O, che fornisce un token IMS per l&#39;autorizzazione del tenant del Brand Portal.

I passaggi per configurare Risorse AEM con Portale marchio variano a seconda della versione di AEM in uso e se si sta configurando per la prima volta o si stanno aggiornando le configurazioni esistenti. Per informazioni dettagliate, consultate [Configurare AEM Assets con il Portale](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) marchio.


### Accessibility enhancements {#accessibility-enhancements}

Experience Manager Assets include i seguenti miglioramenti a livello di accessibilità:

* I tasti freccia sulla tastiera possono essere utilizzati per spostare e scorrere le aree all&#39;interno delle immagini ingrandite. Per ulteriori informazioni, consultate [Anteprima delle risorse solo](../assets/managing-assets-touch-ui.md#previewing-assets)con i tasti di scelta rapida.

* Le caselle di controllo dello stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non vengono selezionate e vengono evidenziate) nel pannello Filtri sono leggibili dagli assistenti vocali.

* Le limitazioni relative al formato di data e ora sono fornite nelle etichette dei campi data, per consentire agli utenti di immettere la data nel formato corretto utilizzando la tastiera.

   Esempio, `On Time (MM-DD-YYYY HH:mm)`. Qui MM è mese in formato a due cifre, AAAA è anno, GG è giorno in formato a due cifre, HH è ora in formato militare a 24 ore e mm è minuto.

* Il `X` simbolo sul pulsante per rimuovere i tag attualmente selezionati viene ora annunciato dagli assistenti vocali insieme al numero di tag selezionati.

## AEM Forms {#aem-forms}

### Genera output stampabile nei flussi di lavoro AEM Forms {#generate-printable-output}

Il nuovo passaggio del flusso di lavoro Genera output stampabile consente di integrare un file modello sorgente con un file di dati. Questa integrazione consente di stampare o salvare copie diverse del file modello. Ad esempio, è possibile stampare un modulo di origine con un nome diverso ogni volta che viene stampato. Salvare i nomi nel file di dati e integrare il file di dati con un file modello standard. Per ulteriori informazioni su questa funzione, vedere [Flusso di lavoro incentrato sui moduli in OSGi - Riferimento](../forms/using/aem-forms-workflow-step-reference.md)passo.

![Genera output stampabile](assets/generate-print-output-demo.gif)

### Supporto per più colonne per moduli adattivi e comunicazioni interattive in modalità Layout {#multi-column-adaptive-forms}

È ora possibile definire il numero di colonne per un pannello nei moduli adattivi e nelle comunicazioni interattive. Passate alla modalità di layout per utilizzare la nuova opzione a più colonne. Per ulteriori informazioni, vedere [Uso della modalità Layout per ridimensionare i componenti](../forms/using/resize-using-layout-mode.md).


![Layout a più colonne](assets/multi-column-layout.gif)



### Personalizzazioni di AEM Inbox {#aem-inbox}

La nuova opzione Controllo amministratore consente agli amministratori di:

* Personalizzare il testo dell’intestazione e il logo

* Controllare la visualizzazione dei collegamenti di navigazione disponibili nell&#39;intestazione

L’opzione Controllo amministratore è visibile solo ai membri del gruppo Amministratori o Amministratori di workflow. Per ulteriori informazioni su questa funzione, vedere [Casella in entrata](../sites-authoring/inbox.md).

### Supporto di testo RTF nei moduli HTML5 {#rich-text-support}

È ora possibile convertire un campo di testo in un modulo XFA in un campo di testo RTF se viene eseguito il rendering in un modulo HTML5. Di conseguenza, il campo di testo visualizza un elenco di altre opzioni di formattazione in un modulo HTML5. Per ulteriori informazioni, vedere [Progettazione di modelli di modulo per moduli](../forms/using/designing-form-template.md)HTML5.

### Accessibility enhancements {#forms-accessibility-enhancements-6540}

Experience Manager Forms include i seguenti miglioramenti a livello di accessibilità:

* Gli utenti possono spostare lo stato attivo sulla scheda senza problemi per il tema di riferimento Ultramarine-Accessible di un modulo adattivo.

* Gli assistenti vocali annunciano le caselle di controllo, i collegamenti, il selettore data e i campi di immissione data correttamente in un modulo adattivo.

* Ogni pagina di un modulo adattivo ora include un titolo e un’etichetta con il punto di riferimento principale.

## Funzioni principali nei precedenti Service Pack di AEM 6.5

### Immagini intelligenti per contenuti multimediali dinamici (6.5.3.0) {#smart-imaging}

Le immagini intelligenti utilizzano le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento. La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Consultate [Smart Imaging](../assets/imaging-faq.md).

### Ricerca visiva di Risorse AEM (6.5.2.0) {#visual-search}

Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. Dall’archivio DAM, AEM visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. See [Visual search](../assets/search-assets.md).

### Condivisione e richiesta dell&#39;accesso agli elementi Inbox di un utente (6.5.3.0) {#share-request-access}

È possibile condividere gli elementi Inbox con un altro utente. Quando un altro utente accede agli elementi della Casella in entrata, può richiedere e intervenire sugli elementi condivisi. Allo stesso modo, potete richiedere l’accesso agli elementi della casella in entrata ad altri utenti. Consultate [Condividere e richiedere l’accesso agli elementi in entrata di un utente](../forms/using/configure-shared-queues-osgi.md).

### Configurare l&#39;impostazione out-of-office per gli elementi in entrata (6.5.3.0) {#configure-out-of-office}

Se prevedete di uscire dall&#39;ufficio, potete specificare cosa accade agli elementi assegnati a quel periodo.
È possibile specificare una data e un&#39;ora di inizio e una data e un&#39;ora di fine affinché le impostazioni fuori sede siano attive. Potete impostare una persona predefinita a cui vengono inviati tutti gli elementi. Consultate [Configurare le impostazioni](../forms/using/configure-out-of-office-settings.md)Fuori sede.

### Generazione di più comunicazioni interattive mediante l&#39;API Batch (6.5.3.0) {#generate-multiple-ic}

Potete utilizzare l&#39;API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L&#39;API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti. Consultate [Generare più comunicazioni interattive utilizzando l&#39;API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

## Versioni principali da AEM 6.5 SP3

Tra il 12 dicembre 2019 e il 5 marzo 2020, Adobe ha rilasciato le seguenti funzionalità che non rientrano nel risultato finale di AEM:

* AEM Cloud Manager 2020.1.0 e 2020.2.0

   Gli aggiornamenti delle versioni migliorano lo stato della pipeline e la possibilità di scaricare i registri per vari passaggi. Per ulteriori informazioni, vedere:

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)


* Aggiornamenti CLI di AEM Cloud Manager

   Gli aggiornamenti della release includono l&#39;automazione delle attività di Cloud Manager tramite lo strumento della riga di comando. Consulta [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites: Archetype progetto 23

   Il modo migliore per avviare un nuovo progetto AEM. Archetype 23 unisce l&#39;Archetype di [Progetto per SPA e i siti regolari in un unico](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) e fornisce un tema predefinito per avviare lo sviluppo front-end.

* AEM Sites: Sito di riferimento WKND

   [Nuovo progetto](https://www.wknd.site/) di riferimento con best practice per la creazione di siti con AEM. Per saperne di più, leggi l&#39;esercitazione [WKND aggiornata](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html). Puoi prendere l&#39;ultimo codice da [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites: Commerce CIF Componenti di base 0.7.0 e 0.9.0

   Integra AEM Sites con Magento Commerce. Consulta [Estensione dei componenti core dedicati e del tipo di archivio dei progetti con focus su Commerce](https://github.com/adobe/aem-core-cif-components/releases).

* Risorse AEM: Desktop App 2.0.1.1

   Per ulteriori informazioni, consultate [Ottenere l’accesso desktop alle risorse](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html).

* AEM Screens: Feature Pack 202001

   Digital Signage direttamente da AEM. Installate i miglioramenti con l&#39;ultimo Feature Pack per [abilitare la riproduzione sincrona tra più lettori](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)multimediali.

## Risorse utili

* [Guide utente di AEM 6.5](../user-guide/home.md)

* [Note generali sulla versione per Adobe Experience Manager 6.5](release-notes.md)

* [Note sulla versione di Service Pack per Adobe Experience Manager 6.5](sp-release-notes.md)
