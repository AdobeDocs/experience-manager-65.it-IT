---
title: Utilizzo di un modulo adattivo in HTML Workspace
seo-title: Utilizzo di un modulo adattivo in HTML Workspace
description: Utilizzo di un modulo adattivo in HTML Workspace
seo-description: Utilizzo di un modulo adattivo in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# Utilizzo di un modulo adattivo in HTML Workspace{#using-an-adaptive-form-in-html-workspace}

 AEM Forms su JEE consente di utilizzare un modulo adattivo in HTML Workspace.

Poiché è possibile selezionare un file XDP durante la progettazione del processo, è stata aggiunta la possibilità di spostarsi da un modulo adattivo esistente AEM repository. Questa funzione consente al progettista di processi di configurare un modulo adattivo sia nel punto di partenza che in attività.

## Esperienza di progettazione del processo {#process-design-experience}

Per abilitare l&#39;uso dei moduli adattivi nella progettazione del processo, effettuare le seguenti operazioni:

* In Assegna attività e Punto iniziale, è possibile individuare una risorsa modulo adattiva nell&#39;archivio CRX quando si assegna una risorsa modulo a un&#39;attività.
* Nel foglio delle proprietà Assegna workbench task/Start Point è possibile nascondere la barra degli strumenti di livello principale/globale di un modulo adattivo.
* È possibile utilizzare i nuovi profili di azione per eseguire le azioni di rendering e invio nei moduli adattivi.

### Esportazione e importazione di applicazioni di LiveCycle {#livecycle-application-export-and-import}

Poiché i moduli adattivi si trovano nell&#39;archivio AEM, l&#39;esportazione dell&#39;applicazione di LiveCycle contiene solo i riferimenti per i moduli adattivi utilizzati. Pertanto, l&#39;esportazione e l&#39;importazione dell&#39;applicazione di LiveCycle è un processo in due fasi. L&#39;applicazione di LiveCycle include le definizioni dei processi e così via. Un pacchetto separato contenente moduli adattivi viene esportato come file ZIP da AEM. Durante l&#39;importazione, l&#39;applicazione di LiveCycle viene importata tramite Workbench e i moduli adattivi vengono importati tramite AEM.

## Esperienza utente del modulo adattivo in HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace offre alcuni controlli specifici per i moduli adattivi, oltre ai controlli disponibili per i moduli per dispositivi mobili. Un utente può aggiungere allegati, salvare, firmare, inviare e spostarsi all&#39;interno dei moduli adattivi in HTML Workspace quando l&#39;utente apre un&#39;attività o un punto iniziale. Di seguito sono riportate le specifiche:

1. Per allegare i file utilizzate gli allegati attività, come nel caso di Mobile Forms. Qualsiasi pulsante del tipo di file allegato del modulo adattivo è nascosto.

1. Per salvare un modulo adattivo, fare clic su **Salva**, come nel caso di Mobile Forms. Qualsiasi pulsante Salva tipo di modulo adattivo è nascosto.

1. Per inviare un modulo adattivo, utilizzare il pulsante **Invia** o le azioni di route disponibili, come nel caso di Mobile Forms. Qualsiasi pulsante di tipo Invia del modulo adattivo è nascosto.

1. **Visibilità** della barra degli strumenti globale per moduli adattivi: Se Process Designer nasconde la barra degli strumenti globale/di livello principale, la barra degli strumenti e i pulsanti non vengono visualizzati sui moduli adattivi.

1. **Controlli di navigazione area di lavoro per Forms** adattivo: I pulsanti Successivo/Precedente sono disponibili insieme ai pulsanti Salva, Invia e Inoltra azione per un modulo adattivo in HTML Workspace. Fare clic sui pulsanti Successivo/Precedente per spostarsi nei pannelli dei moduli adattivi in HTML Workspace. I pulsanti Successivo/Precedente forniscono una navigazione approfondita, simile ai controlli di navigazione nella vista Mobile dei moduli adattivi.

1. **Servizi eSign e componente di riepilogo del modulo** adattivo: Il componente Riepilogo non è operativo in HTML Workspace. In altre parole, se un modulo adattivo dispone di un componente Riepilogo, non è visibile nell’area di lavoro. Anziché inviare automaticamente nel componente Esign, l’utente dell’area di lavoro fa clic sull’azione Invia o su un’azione di route in HTML Workspace. Dopo che un documento è stato firmato, è visibile come documento firmato a schermo piatto. Fare clic su **Invia** o su un&#39;azione di route per chiudere/completare l&#39;attività o il punto iniziale.\
   Il documento firmato viene raccolto dal server dei servizi eSign e il file XML dei dati viene inoltrato al passaggio successivo della procedura.

## Passaggi per l&#39;utilizzo di moduli adattivi nella progettazione del processo {#steps-to-use-adaptive-forms-in-process-design}

1. Aprire  Adobe Experience Manager Forms Workbench.

1. Passate a **File > Nuovo > Applicazione** oppure utilizzate l&#39;applicazione esistente per creare un&#39;applicazione.

   ![Creare una nuova applicazione](assets/create_new_appl.png)

   Creare una nuova applicazione

1. Create un processo o utilizzate un processo esistente nell&#39;applicazione.

   ![Crea nuovo processo](assets/create_new_process.png)

   Crea nuovo processo

1. Crea un punto iniziale o Assegna attività e fai doppio clic su di esso.
1. Nella sezione **[!UICONTROL Presentation &amp; Data]** (Presentazione e dati), selezionate **[!UICONTROL use a CRX asset]** e fate clic sulle ellissi prima della risorsa.

   ![Utilizzare una risorsa CRX](assets/use_crx_asset.png)

   Utilizzare una risorsa CRX

1. Selezionate il modulo adattivo creato tramite l’interfaccia utente di Gestione risorse e fate clic su **[!UICONTROL OK]**.

   ![Selezione di un modulo adattivo](assets/selecting_form.png)

   Selezione di un modulo adattivo

   >[!NOTE]
   >
   >Per informazioni dettagliate sulla creazione di un modulo adattivo, vedere [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Per informazioni dettagliate sulla creazione di un processo, vedere [Creazione e gestione di processi](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).

