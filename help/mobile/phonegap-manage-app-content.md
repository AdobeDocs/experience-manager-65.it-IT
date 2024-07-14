---
title: Creazione e gestione del contenuto delle app
description: La gestione dei contenuti delle app richiede uno sforzo collettivo da parte di sviluppatori, autori di contenuti e amministratori. Gli autori manipolano le pagine, basate su modelli e componenti generati dagli sviluppatori di app.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---

# Creazione e gestione del contenuto delle app{#creating-and-managing-app-content}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

La gestione del contenuto dell&#39;app richiede uno sforzo collettivo da parte di [sviluppatori](#developer), [autori](#author) e [amministratori](#administrator). Gli autori manipolano le pagine, basate su modelli e componenti generati dagli sviluppatori di app.

Infine, gli amministratori pubblicano in modo strategico il contenuto aggiornato dell’app.

>[!NOTE]
>
>**Prerequisito**:
>
>In [Distribuzione e manutenzione](/help/sites-deploying/deploy.md), gli sviluppatori hanno acquisito familiarità con i componenti e i modelli di sistema in Adobe Experience Manager (AEM).

## Sezione Gestione contenuto pagina {#the-manage-page-content-tile}

>[!CAUTION]
>
>Se non utilizzi un modello di app predefinito, per abilitare la pubblicazione del nuovo contenuto dell’app OTA devi configurare un gestore di sincronizzazione contenuti.
>
>Per ulteriori dettagli, consulta [Mobile con sincronizzazione contenuti](/help/mobile/phonegap-contentsync.md) nella sezione per sviluppatori.

Qui, il contenuto può essere creato, modificato ed eliminato in AEM Mobile nello stesso modo in cui si creerebbe all’interno di AEM Sites.

Il riquadro **Gestione contenuto pagina** visualizza il numero di pagine di contenuto gestito e l&#39;ultima modifica per un determinato payload. È possibile eseguire il drill-in del contenuto per creare, copiare, spostare, eliminare e aggiornare le pagine facendo clic su ogni record nella sezione.

Una volta aggiornato il contenuto, gli amministratori possono pubblicare ai clienti un payload di aggiornamento del contenuto Over-the-Air (OTA) tramite la sezione **Gestisci pacchetti di contenuti.**

![chlimage_1-161](assets/chlimage_1-161.png)

Seleziona uno dei pacchetti di contenuti elencati per creare o modificare contenuti quali la creazione, la modifica o la rimozione di pagine, la modifica della navigazione e dell’ordine delle pagine, la creazione o l’aggiornamento di contenuti quali copia (testo) e file multimediali.

Nota *tutto è contenuto*, il che significa che gli stili dell&#39;applicazione, la copia (testo), i file multimediali, le pagine, la navigazione e il targeting del contenuto possono essere modificati e aggiornati OTA, senza un viaggio in un app store.

Per modificare il contenuto di AEM Mobile, *Gli autori AEM *avranno bisogno di una solida conoscenza dell&#39;interfaccia di modifica dei contenuti AEM: [Authoring delle pagine in AEM.](/help/sites-authoring/qg-page-authoring.md)

## Sezione Gestione pacchetti di contenuti {#the-manage-content-packages-tile}

In questo caso, *gli amministratori dell&#39;AEM* possono aggiornare in modo rapido e semplice le app per fornire esperienze coinvolgenti e contenuti aggiornati, per promuovere il brand engagement e raggiungere gli obiettivi aziendali senza dover ricorrere a un nuovo invio da parte di sviluppatori o app store.

![chlimage_1-162](assets/chlimage_1-162.png)

Una volta che *gli autori dell&#39;AEM* hanno aggiunto o modificato il contenuto tramite il riquadro Gestisci contenuto, *gli amministratori dell&#39;AEM* possono inviare tali modifiche ai clienti con un aggiornamento dei pacchetti di contenuti.

L&#39;azione Pacchetto di contenuti consente all&#39;autore *AEM* di creare e modificare il contenuto della pagina mentre il team di sviluppo apporta modifiche alla progettazione e all&#39;implementazione di un&#39;applicazione host, inclusi navigazione, stile, logica lato server, modelli e componenti, quindi di inviare tali modifiche ai clienti OTA senza dover risottomettere i vari store per la distribuzione.

**Per pubblicare contenuti nuovi o aggiornati**

Seleziona un pacchetto di contenuti dalla sezione, in questo esempio il pacchetto inglese. In una finestra di dialogo di aggiornamento del contenuto è elencata la configurazione *Sincronizzazione contenuto* pertinente. Se il contenuto dell&#39;app è stato modificato dopo un aggiornamento precedente, verrà visualizzato lo stato *In sospeso*, come illustrato di seguito.

![chlimage_1-163](assets/chlimage_1-163.png)

Quindi, seleziona l&#39;azione **Stage** in alto a destra per creare l&#39;aggiornamento del contenuto. Aggiungi le informazioni di aggiornamento appropriate e premi Fine.

![chlimage_1-164](assets/chlimage_1-164.png)

Il gestore *Content Sync* crea quindi i pacchetti richiesti formando un delta (un pacchetto di *only* che cosa è cambiato). Una volta completato, questo pacchetto di contenuti per l’aggiornamento è stato aggiunto all’area intermedia come mostrato di seguito.

La gestione temporanea di un aggiornamento del contenuto consente di effettuare diversi aggiornamenti prima di pubblicarli su dispositivi mobili OTA.

>[!NOTE]
>
>Il contenuto in staging può essere verificato utilizzando l&#39;app Verifica AEM prima della pubblicazione.
>
>Per ulteriori dettagli sull&#39;app di verifica AEM, vedere [Mobile Quickstart per la verifica AEM](/help/mobile/phonegap-mobile-quickstart.md).

![chlimage_1-165](assets/chlimage_1-165.png)

Quando sei pronto a distribuire nuovi contenuti agli utenti dell&#39;app con Content Sync OTA, seleziona **Publish** come mostrato di seguito.

![chlimage_1-166](assets/chlimage_1-166.png)

### Passaggi successivi {#the-next-steps}

Dopo aver appreso le informazioni su Creazione e gestione del contenuto delle app nel dashboard dell’applicazione, consulta le risorse seguenti per altri ruoli di authoring:

* [Sezione Gestione app](/help/mobile/phonegap-app-details-tile.md)
* [Modifica dei metadati dell’app](/help/mobile/phonegap-editmetadata.md)
* [Definizioni delle app](/help/mobile/phonegap-app-definitions.md)
* [Creazione di una nuova app mediante la Creazione guidata app](/help/mobile/phonegap-create-new-app.md)
* [Importa un&#39;app ibrida esistente](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di uno sviluppatore, consulta le risorse seguenti:

* [Sviluppo per Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
