---
title: Authoring di applicazioni mobili
description: La dashboard di AEM Mobile consente di creare, generare e distribuire l’app mobile, nonché di creare, eliminare e modificare i metadati dell’applicazione. Per ulteriori informazioni, segui questa pagina.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Authoring di applicazioni mobili{#authoring-mobile-applications}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

La dashboard di AEM Mobile consente di creare, generare e distribuire l’app mobile, nonché di creare, eliminare e modificare i metadati dell’applicazione. Una volta che l’applicazione è attiva, puoi analizzarla includendo le metriche sul ciclo di vita e sull’utilizzo, per migliorare la conversione dei clienti e la fedeltà al marchio.

Per creare la tua applicazione AEM Mobile, consulta [Creazione di applicazioni mobili](/help/mobile/building-app-mobile-phonegap.md) pagina.

Per configurare l’ambiente e iniziare, consulta [Amministrazione dell’AEM per utilizzare l’AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## Catalogo delle app AEM Mobile {#the-aem-mobile-apps-catalog}

Il [Catalogo app AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) mostra tutte le app mobili gestite in AEM.

Considera questo catalogo come la &quot;pagina di destinazione&quot; per AEM Mobile, in cui gli amministratori possono avviare una nuova applicazione AEM Mobile creando in base a un modello o caricando un’app esistente già avviata da uno sviluppatore mobile.

Per accedere alla pagina di destinazione del catalogo delle app, segui la procedura riportata di seguito:

1. Sfoglia per **Navigazione** e quindi scegliere **Dispositivi mobili**.

1. Scegli **App** per aprire il catalogo delle app.

![Catalogo app AEM Mobile](assets/chlimage_1-135.png)

## Dashboard dell’app AEM Mobile {#the-aem-mobile-app-dashboard}

Selezionando un’app AEM Mobile dal catalogo viene visualizzata la relativa dashboard. Qui puoi gestire l’applicazione, visualizzare le statistiche, generare, distribuire e gestire il contenuto dell’app mobile.

Per visualizzare o modificare i dettagli, espandi in ogni tessera nel dashboard di AEM Mobile facendo clic su &quot;...&quot; in basso a destra.

![Centro comandi applicazioni AEM Mobile](assets/chlimage_1-136.png)

### Sezione Gestione app {#the-manage-app-tile}

Il riquadro Gestione app mostra l’icona dell’applicazione, il nome, la descrizione, le piattaforme supportate, nonché l’URL e le informazioni sulla versione da chiamare a casa per gli aggiornamenti. È possibile espandere questo riquadro per modificare e gestire la configurazione dell&#39;applicazione PhoneGap (config.xml) e preparare l&#39;applicazione per l&#39;invio ai vari archivi dell&#39;applicazione per la distribuzione.

Clic [qui](/help/mobile/phonegap-app-details-tile.md) per i dettagli.

![chlimage_1-137](assets/chlimage_1-137.png)

### Sezione Gestione contenuto pagina {#the-manage-page-content-tile}

I contenuti possono essere creati, aggiornati ed eliminati in AEM Mobile nello stesso modo in cui lo si fa in AEM Sites. Il **Gestisci sezione contenuto pagina** visualizza il numero di pagine del contenuto gestito e dell’ultima modifica. È possibile eseguire il drill-in del contenuto per creare, copiare, spostare, eliminare e aggiornare le pagine facendo clic su ogni record nella sezione. Una volta aggiornato il contenuto, puoi inviare un aggiornamento del contenuto ai clienti tramite **Sezione Gestire i pacchetti di contenuti.**

![Sezione contenuto](assets/chlimage_1-138.png)

### Sezione Gestione pacchetti di contenuti {#the-manage-content-packages-tile}

Dopo aver aggiunto o modificato il contenuto tramite il riquadro Gestisci contenuto pagina, puoi inviare tali modifiche ai clienti con un aggiornamento sulla versione del contenuto.

Il pacchetto di contenuti consente all’autore dell’app AEM di gestire il contenuto della pagina nell’AEM e di far sì che il team di sviluppo apporti modifiche all’applicazione PhoneGap Shell (ovvero al framework o all’infrastruttura dell’app) e quindi inviarle rapidamente ai clienti senza dover reclutare uno sviluppatore per inviarle nuovamente ai vari store per la distribuzione.

Pacchetto di contenuti crea un file ZIP, considerato un pacchetto di rilascio dei contenuti, per ogni aggiornamento. Questi pacchetti contengono risorse HTML e pagine HTML generate durante il rendering dell’app ed è sufficientemente intelligente da includere solo i file che sono stati modificati dopo l’ultimo aggiornamento.

Il riquadro Gestione pacchetto contenuti **Tipo** Nella colonna viene visualizzato &quot;App&quot; per indicare il contenuto della shell dell’applicazione, ad esempio il framework o l’infrastruttura dell’app gestita da uno sviluppatore oppure &quot;Content&quot; (Contenuto), che rappresenta il contenuto della pagina gestito dall’autore del contenuto.

Il contenuto può essere rappresentato come lingua o come parte particolare dell’app, dove l’app utilizza più pacchetti di rilascio dei contenuti. La scelta del modo in cui riunire i contenuti è flessibile e completamente adatta alla modalità di gestione dei contenuti per l’applicazione.

Il **Modificato** indica quando le pagine sono state modificate più di recente.

Il **In staging** mostra quando è stato creato l’ultimo aggiornamento del contenuto. Per creare un aggiornamento del contenuto e posizionare nell’area intermedia le modifiche, apri qualsiasi record nella sezione e crea un aggiornamento.

Il **Pubblicato** Questa colonna mostra quando è stato pubblicato l’ultimo aggiornamento del contenuto, che è stato reso disponibile per l’utilizzo da parte dei clienti. Per pubblicare il contenuto, devi prima inserire nell’area intermedia il contenuto e quindi pubblicare l’aggiornamento espandendo questa sezione e pubblicando dalla console dei dettagli della versione di contenuto.

![Sezione rilascio contenuto](assets/chlimage_1-139.png) ![Pacchetto ContentSync per la shell dell’app](do-not-localize/chlimage_1-5.png)

Questa icona rappresenta un pacchetto di rilascio dei contenuti per la shell dell’app

![L’icona del pacchetto Rilascio contenuto è indicata da due simboli di pacchetto quadrati che si sovrappongono.](do-not-localize/chlimage_1-6.png)

Queste icone rappresentano un pacchetto di rilascio dei contenuti per l’app

### Sezione PhoneGap Build {#the-phonegap-build-tile}

Il **PhoneGap Build** si connette con `https://build.phonegap.com` per generare e ospitare build remote. Una volta creata, la build viene resa disponibile come download o direttamente sul dispositivo tramite un codice QR.

In alternativa, è possibile scaricare l&#39;origine del dispositivo per la generazione locale tramite PhoneGap CLI (`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`).

![PhoneGap Build](assets/chlimage_1-140.png)

### Sezione metriche {#the-metrics-tile}

>[!CAUTION]
>
>Il riquadro Metriche viene visualizzato solo dopo aver configurato il servizio cloud.
>
>Consulta [Configurare il Cloud Service Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md) per i dettagli.

AEM Mobile si integra con Adobe Analytics tramite [SDK di Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS)

Centro di controllo **Sezione metriche** visualizza l’analisi di riepilogo estratta da AMS per la tua applicazione. Per approfondire il dashboard di Analytics, fai clic su &quot;...&quot; in basso a destra.

![Sezione metriche](assets/chlimage_1-141.png)

### Sezione Gestione contenuto entità {#the-manage-entity-content-tile}

Il riquadro Gestisci contenuto entità consente di aggiungere e gestire le definizioni di app. Le definizioni delle app sono un modo per identificare quali spazi (e altre configurazioni) sono appropriati per l’app. In questo modo è possibile aggiungere un nuovo spazio, senza dover ricompilare l’app. La definizione dell’app viene aggiornata e include le informazioni per eventuali nuovi spazi.

Clic [qui](/help/mobile/phonegap-app-definitions.md) per creare e gestire le definizioni delle app.

Per espandere il dashboard di gestione del contenuto delle entità, fai clic su &quot;...&quot; in basso a destra.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di uno sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
