---
title: Creazione e gestione del contenuto delle app
seo-title: Creazione e gestione del contenuto delle app
description: La gestione dei contenuti delle app richiede un impegno collettivo da parte di sviluppatori, autori di contenuti e amministratori.  Gli autori modificano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app.
seo-description: La gestione dei contenuti delle app richiede un impegno collettivo da parte di sviluppatori, autori di contenuti e amministratori.  Gli autori modificano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app.
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# Creazione e gestione di contenuto dell&#39;app{#creating-and-managing-app-content}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La gestione dei contenuti dell&#39;app richiede un impegno collettivo da parte di [sviluppatori](#developer), [autori](#author) e [amministratori](#administrator). Gli autori modificano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app.

Infine, gli amministratori pubblicano strategicamente il contenuto dell&#39;app aggiornata.

>[!NOTE]
>
>**Prerequisito**:
>
>In [Implementazione e manutenzione](/help/sites-deploying/deploy.md), gli sviluppatori hanno acquisito familiarità con AEM sistema di componenti e modelli.

## Gestisci sezione contenuto pagina {#the-manage-page-content-tile}

>[!CAUTION]
>
>Se non utilizzate un modello di app integrato, per abilitare la pubblicazione OTA del nuovo contenuto dell&#39;app, dovete configurare un gestore di sincronizzazione dei contenuti.
>
>Per ulteriori informazioni, consultate [Mobile con Content Sync](/help/mobile/phonegap-contentsync.md) nella sezione Sviluppatore.

In questo caso, il contenuto può essere creato, modificato ed eliminato in  AEM Mobile nello stesso modo in cui lo si creava in  AEM Sites.

La sezione **Gestisci contenuto pagina** visualizza il numero di pagine di contenuto gestito e l&#39;ultima modifica apportata a un particolare payload. Per approfondire i contenuti per creare, copiare, spostare, eliminare e aggiornare le pagine, fate clic su ciascun record nella sezione.

Una volta aggiornato il contenuto, gli amministratori possono pubblicare un payload di aggiornamento del contenuto Over-the-Air (OTA) per i clienti tramite la sezione **Gestisci pacchetti di contenuti.**

![chlimage_1-161](assets/chlimage_1-161.png)

Selezionate uno dei pacchetti di contenuti elencati per creare o modificare contenuti quali creazione, modifica o rimozione di pagine, modifica della navigazione e dell&#39;ordine delle pagine, creazione o aggiornamento di contenuti quali copia (testo) e contenuti multimediali.

Nota *tutto è contenuto*, vale a dire stili di applicazione, copia (testo), supporti, pagine, navigazione e, il targeting del contenuto può essere modificato e aggiornato OTA, senza un viaggio in un app store.

Per modificare  contenuto AEM Mobile, *AEM autori *dovranno conoscere AEM&#39;interfaccia di modifica del contenuto: [Creazione di pagine in AEM.](/help/sites-authoring/qg-page-authoring.md)

## Sezione Gestisci pacchetti di contenuti {#the-manage-content-packages-tile}

In questo caso, *AEM amministratori* possono aggiornare rapidamente e facilmente le app per offrire esperienze coinvolgenti e contenuti aggiornati in grado di promuovere il coinvolgimento del marchio e soddisfare gli obiettivi aziendali, senza la necessità di inviare nuovamente uno sviluppatore o un app store.

![chlimage_1-162](assets/chlimage_1-162.png)

Dopo che *AEM Authors* ha aggiunto o modificato contenuto tramite la sezione Gestisci contenuto, *AEM amministratori* possono inviare tali modifiche ai clienti con un aggiornamento Pacchetti di contenuti.

L&#39;azione Pacchetto contenuti consente a *AEM Author* di creare e modificare il contenuto delle pagine mentre il team di sviluppo apporta modifiche alla progettazione e all&#39;implementazione di un&#39;applicazione host, inclusi navigazione, stile, logica lato server, modelli e componenti, e quindi invia tali modifiche ai clienti senza dover inviare nuovamente i diversi store per la distribuzione.

**Per pubblicare contenuto nuovo o aggiornato**

Selezionate un pacchetto di contenuti dalla sezione, in questo esempio il pacchetto inglese. Una finestra di dialogo di aggiornamento del contenuto elenca la relativa configurazione *Content Sync*. Se il contenuto dell&#39;app è stato modificato dopo un aggiornamento precedente, lo stato sarà *In sospeso*, come mostrato di seguito.

![chlimage_1-163](assets/chlimage_1-163.png)

Quindi, selezionate l&#39;azione **Stage** in alto a destra per creare il nuovo aggiornamento del contenuto. Aggiungete le informazioni di aggiornamento appropriate e premete Fine.

![chlimage_1-164](assets/chlimage_1-164.png)

Il gestore *Content Sync* crea quindi i pacchetti richiesti formando un delta (un pacchetto di *only* che ha modificato). Una volta completato, questo pacchetto di aggiornamento del contenuto è stato messo in stato di avanzamento come mostrato di seguito.

L&#39;avvio di un aggiornamento al contenuto consente di effettuare diversi aggiornamenti prima di pubblicarli su OTA per dispositivi mobili.

>[!NOTE]
>
>Il contenuto sullo stage può essere verificato utilizzando l&#39;app AEM Verify prima della pubblicazione.
>
>Per ulteriori informazioni sull&#39;app AEM verifica, vedere [Mobile Quickstart per AEM Verify](/help/mobile/phonegap-mobile-quickstart.md).

![chlimage_1-165](assets/chlimage_1-165.png)

Quando siete pronti per inviare nuovo contenuto agli utenti dell&#39;app con Content Sync OTA, selezionate **Pubblica** come mostrato di seguito.

![chlimage_1-166](assets/chlimage_1-166.png)

### Passaggi successivi {#the-next-steps}

Dopo aver appreso la creazione e la gestione del contenuto dell&#39;app nel dashboard dell&#39;applicazione, consulta le risorse seguenti per altri ruoli di authoring:

* [Gestisci sezione app](/help/mobile/phonegap-app-details-tile.md)
* [Modifica dei metadati dell&#39;app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Creazione di una nuova app tramite Creazione guidata app](/help/mobile/phonegap-create-new-app.md)
* [Importare un&#39;app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Sviluppo per  Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per  Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
