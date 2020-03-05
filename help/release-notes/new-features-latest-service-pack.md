---
title: Novità in Adobe Experience Manager 6.5 Service Pack 4
description: Novità in Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 1d867ee46ca9cd5945c7413d42fc002b90332c3c

---


# Novità in Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Nel 2020, per Adobe Experience Manager (AEM) 6.5, i Service Pack trimestrali contengono nuove funzioni e miglioramenti. I clienti traggono vantaggio da questo nuovo approccio per adottare le innovazioni più rapidamente.

L’ultimo Service Pack 4 di AEM (6.5.4.0) è stato rilasciato il 5 **marzo 2020**. In questo articolo vengono evidenziate le funzioni offerte dall’ultimo Service Pack per rendere il vostro viaggio AEM più ricco.

## AEM Sites {#aem-sites}

### Miglioramenti delle prestazioni in varie aree {#performance-improvements}

* Ridurre il tempo necessario per caricare e inizializzare ContextHub in un sito (contexthub.kernel.js). Consente di caricare più rapidamente la prima pagina durante una visita del sito.

* Nell’Editor pagina, riduci il tempo di aggiornamento della pagina dopo aver trascinato e rilasciato frammenti esperienza nell’area di lavoro della pagina.

* In Panoramica di Live Copy, riducete il tempo necessario per caricare le voci se il sito contiene molte copie in tempo reale (+200).

* Nell’Editor modelli, è possibile migliorare la gestione degli URL incompleti/non validi che potrebbero rallentare l’Editor modelli.

Inoltre, a partire da AEM 6.5 SP4, il sistema di stile è stato migliorato e ora è possibile selezionare gli stili anche all&#39;interno di una finestra di dialogo dei componenti.

## AEM Assets {#aem-assets}

### Integrazione con Brand Portal tramite la console di I/O di Adobe {#assets-integration-bp}

AEM Assets è ora configurato con Brand Portal tramite Adobe I/O, che fornisce un token IMS per l&#39;autorizzazione del tenant del Brand Portal. In precedenza era stato configurato nell’interfaccia classica tramite il gateway OAuth legacy.

Le nuove integrazioni con OAuth legacy non saranno supportate dopo il 6 aprile 2020 e passeranno alla console di I/O di Adobe. Se non modificate l&#39;integrazione, le configurazioni esistenti continueranno a funzionare.

Potete creare una nuova integrazione o aggiornare le impostazioni di integrazione alla console di I/O di Adobe.

### Accessibility enhancements {#accessibility-enhancements}

* Le caselle di controllo con stato misto dispongono ora di un attributo con controllo aria con valore &quot;misto&quot; per esporre lo stato misto agli assistenti vocali.

* I controlli basati su tastiera sono ora supportati oltre ai gesti basati sul percorso per spostarsi intorno alle immagini ingrandite.

* Nelle etichette dei campi sono stati inseriti vincoli di formato data che consentono agli utenti di utilizzare solo la tastiera per immettere manualmente la data.

* L&#39;attributo Alt è stato aggiunto alle icone decorative e rimosso l&#39;attributo role=img, in modo che tali icone e immagini non siano esposte agli utenti dell&#39;assistente vocale.

* È stato aggiunto l&#39;attributo Alt per chiudere le icone e indicare agli utenti dell&#39;assistente vocale quando si spostano con il tasto Tab.

## AEM Forms {#aem-forms}

### Genera output stampabile nei flussi di lavoro AEM Forms {#generate-printable-output}

Se si desidera una soluzione per stampare più copie di un file modello di origine e integrarlo con un file di dati contenente numerosi record, in AEM Forms è disponibile un nuovo passaggio del flusso di lavoro Genera output stampabile. Ad esempio, se si desidera stampare un modulo di origine con un nome diverso ogni volta che viene stampato, è possibile inserire tali nomi nel file di dati e integrarlo con un file modello standard.

Sfruttate questa funzione tramite **Strumenti** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL Crea]** e quindi cercate il passaggio del flusso di lavoro **[!UICONTROL Genera output]** stampabile.

![Genera output stampabile](assets/generate-print-output-demo.gif)

Per ulteriori informazioni su questa funzione, vedere [Flusso di lavoro incentrato sui moduli in OSGi - Riferimento](../forms/using/aem-forms-workflow-step-reference.md)passo.

### Supporto a più colonne per moduli adattivi e comunicazioni interattive in modalità Layout {#multi-column-adaptive-forms}

È ora possibile definire il numero di colonne per un pannello nei moduli adattivi e nelle comunicazioni interattive.

Per trovare la nuova opzione, passate alla modalità Layout, toccate il pannello da convertire in un formato a più colonne, selezionate la relativa icona padre e toccate l’icona a più colonne, come illustrato nella figura riportata di seguito, per definire il numero di colonne per il pannello.

![Layout a più colonne](assets/multi-column-layout.gif)

Per ulteriori informazioni, vedere [Uso della modalità Layout per ridimensionare i componenti](../forms/using/resize-using-layout-mode.md).

### Personalizzazioni di AEM Inbox {#aem-inbox}

È mai necessario personalizzare le opzioni disponibili nell’intestazione di AEM? È ora possibile con la nuova versione di Service Pack con l&#39;introduzione di un&#39;opzione **[!UICONTROL Admin Control]** .

**Personalizza il testo dell’intestazione**

Gli utenti appartenenti al gruppo amministratori **del** flusso di lavoro possono ora personalizzare il testo dell’intestazione disponibile nella parte superiore con testo personalizzato, in modo da sostituire il testo esistente di **[!UICONTROL Adobe Experience Manager]** .

La nuova opzione **[!UICONTROL Personalizza testo]** intestazione è disponibile nel selettore delle viste (disponibile in alto a destra della barra degli strumenti) > **[!UICONTROL Admin Control]**.

**Personalizza logo**

Come per il testo personalizzato dell’intestazione, gli utenti appartenenti al gruppo **workflow-amministratori** possono personalizzare il logo disponibile nella parte superiore con il logo desiderato.

La nuova opzione **[!UICONTROL Personalizza logo]** è disponibile in Selettore visualizzazione > **[!UICONTROL Controllo]** amministratore.

Per ulteriori informazioni su questa funzione, vedere [Casella in entrata](../sites-authoring/inbox.md).

### Controllo navigazione utente {#user-navigation-control}

Gli utenti appartenenti al gruppo amministratori **del** flusso di lavoro hanno la possibilità di far sì che gli utenti lavorino su AEM in modalità limitata in base al loro ruolo. Gli amministratori possono controllare la visualizzazione delle opzioni di navigazione disponibili nell’intestazione e limitare gli utenti alla modalità di authoring del flusso di lavoro o passare all’Aiuto o ad altri collegamenti della soluzione.

Scopri le nuove opzioni **[!UICONTROL di navigazione]** Nascondi opzioni **[!UICONTROL in Selettore vista > Controllo]** amministratore.

Per ulteriori informazioni su questa funzione, vedere [Casella in entrata](../sites-authoring/inbox.md).

### Supporto di testo RTF nei moduli HTML5 {#rich-text-support}

Nel campo di testo è ora possibile visualizzare un elenco delle opzioni di formattazione nel modulo HTML5 di cui è stato effettuato il rendering. In Forms Designer è necessario definire un formato di campo per il campo di testo in modo da applicare le impostazioni appropriate al campo.

Per utilizzare questa funzione, toccare il campo di testo in visualizzazione **** Struttura in Forms Designer. Nella scheda **[!UICONTROL Campo]** , selezionare Testo **** RTF dall&#39;elenco a discesa Formato **** campo per applicare le impostazioni. Il campo di testo ora visualizza le opzioni di formattazione quando viene eseguito il rendering in un modulo HTML5.

Per ulteriori informazioni, vedere [Progettazione di modelli di modulo per moduli](../forms/using/designing-form-template.md)HTML5.

## Evidenziazioni principali

Oltre alle nuove funzioni, AEM 6.5 Service Pack 4 include le seguenti funzionalità principali:

* Ora è possibile sincronizzare in Scene7 solo le sottostrutture di contenuto selettivo, anziché tutte `content/dam`.

* L&#39;integrazione del modello di dati del modulo con il servizio Web SOAP ora supporta i gruppi di scelta o gli attributi sugli elementi.

* Le strutture di input o output SOAP e i dati complessi ora supportano la sostituzione di gruppi dinamici.

## Funzioni principali nei precedenti Service Pack di AEM 6.5

### Immagini intelligenti per contenuti multimediali dinamici {#smart-imaging}

La tecnologia di imaging intelligente sfrutta le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento. La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Consultate [Smart Imaging](../assets/imaging-faq.md).

### Ricerca visiva per AEM Assets {#visual-search}

Aggiunta della funzionalità di ricerca di immagini visivamente simili per gli utenti di Assets. Dall’archivio DAM, AEM visualizza le immagini con tag avanzati che risultano simili a quelle selezionate dall’utente. See [Visual search](../assets/search-assets.md).

### Condividere e richiedere l&#39;accesso agli elementi Inbox di un utente {#share-request-access}

È possibile condividere gli elementi Inbox con un altro utente. Quando un altro utente ha accesso agli elementi della Casella in entrata, può richiedere e intervenire sugli elementi condivisi. Allo stesso modo, potete richiedere l’accesso agli elementi della casella in entrata ad altri utenti. Consultate [Condividere e richiedere l’accesso agli elementi in entrata di un utente](../forms/using/configure-shared-queues-osgi.md).

### Configurazione dell&#39;impostazione fuori sede per gli elementi della casella in entrata {#configure-out-of-office}

Se prevedete di uscire dall&#39;ufficio, potete specificare cosa accade agli elementi assegnati a quel periodo.
È possibile specificare una data e un&#39;ora di inizio e una data e un&#39;ora di fine affinché le impostazioni fuori sede siano attive. Potete impostare una persona predefinita alla quale vengono inviati tutti gli elementi. Consultate [Configurare le impostazioni](../forms/using/configure-out-of-office-settings.md)Fuori sede.

### Generazione di più comunicazioni interattive mediante l&#39;API Batch {#generate-multiple-ic}

Potete utilizzare l&#39;API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L&#39;API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti. Consultate [Generare più comunicazioni interattive utilizzando l&#39;API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

### Messaggi di errore di convalida standard per i moduli adattivi {#standard-validation}

I moduli adattivi possono ora integrarsi con i servizi personalizzati per eseguire le convalide dei dati. Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore di convalida restituito dal server è nel formato di messaggio standard, i messaggi di errore vengono visualizzati a livello di campo nel modulo. Se i valori di input non soddisfano i criteri di convalida e il messaggio di errore convalida server non è nel formato di messaggio standard, i moduli adattivi forniscono un meccanismo per trasformare i messaggi di errore di convalida in un formato standard in modo che siano visualizzati a livello di campo nel modulo. Vedere Messaggi di errore di convalida [standard per i moduli](../forms/using/standard-validation-error-messages-adaptive-forms.md)adattivi.

## Versioni principali da AEM 6.5 SP3

Tra il 12 dicembre 2019 e il 5 marzo 2020 Adobe ha rilasciato le seguenti funzionalità che non rientrano nel risultato finale di AEM:

* AEM Cloud Manager 2020.1.0 e 2020.2.0Miglioramenti mensili a Cloud Manager, le ultime due release sono incentrate sul miglioramento dello stato della pipeline e sulla possibilità di scaricare i registri per i vari passaggi. Leggi le note complete sulla versione qui:
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* Aggiornamenti CLI di AEM Cloud ManagerAutomatizzare le attività di Cloud Manager utilizzando lo strumento della riga di comando. Stiamo continuando a estendere l&#39;CLI - join su [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites: Project Archetype 23Il modo migliore per avviare un nuovo progetto AEM. Con Archetype 23 stiamo [unendo il Project Archetype per SPA e i siti regolari in un unico](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23), fornendo inoltre un tema predefinito per dare il via al vostro sviluppo front-end.

* AEM Sites: Sito di riferimento WKNDTutti i [nuovi progetti](https://www.wknd.site/) di riferimento dotati di procedure ottimali per la creazione di siti con AEM. Scopri di più leggendo l&#39;esercitazione [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) WKND completamente aggiornata e acquisisci il codice da [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites: Commerce CIF Componenti di base 0.7.0 e 0.9.0Integrazione di AEM Sites e Magento Commerce. Stiamo [estendendo continuamente i componenti core dedicati e un archetipo di progetto con attenzione su Commerce](https://github.com/adobe/aem-core-cif-components/releases).

* Risorse AEM: Desktop App 2.0.1.1
   [Accesso desktop alle risorse](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens: Feature Pack 202001Digital Signage direttamente da AEM. Scopri gli ultimi miglioramenti apportati al Feature Pack più recente, questa volta [abilitiamo la riproduzione sincrona tra più lettori](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)multimediali.

## Risorse utili

* [Guide utente di AEM 6.5](../user-guide/capabilities.md)

* [Note generali sulla versione per Adobe Experience Manager 6.5](release-notes.md)

* [Note sulla versione di Service Pack per Adobe Experience Manager 6.5](sp-release-notes.md)
