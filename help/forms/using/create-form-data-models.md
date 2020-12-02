---
title: Crea modello dati modulo
seo-title: Crea modello dati modulo
description: Scoprite come creare modelli di dati dei moduli con o senza origini dati configurate.
seo-description: Scoprite come creare modelli di dati dei moduli con o senza origini dati configurate.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Crea modello dati modulo{#create-form-data-model}

![](do-not-localize/data-integeration.png)

&#39;integrazione dei dati AEM Forms fornisce un&#39;interfaccia utente intuitiva per creare e utilizzare modelli di dati del modulo. Un modello dati modulo si basa su origini dati per lo scambio di dati; tuttavia, è possibile creare un modello dati del modulo con o senza un&#39;origine dati. Esistono due approcci per creare un modello dati da un modulo a seconda che siano state configurate origini dati:

* **Utilizzo di origini** dati preconfigurate: Se sono state configurate le origini dati come descritto in  [Configurare le origini](../../forms/using/configure-data-sources.md) dati, è possibile selezionarle durante la creazione di un modello dati del modulo. Contiene tutti gli oggetti del modello dati, le proprietà e i servizi delle origini dati selezionate disponibili per l&#39;uso nel modello dati del modulo.

* **Senza origini** dati: Se non sono state configurate origini dati per il modello dati del modulo, è comunque possibile crearle senza origini dati. È possibile utilizzare il modello dati del modulo per creare moduli adattivi e comunicazioni interattive e testarli utilizzando dati di esempio. Quando sono disponibili le origini dati, è possibile eseguire un binding del modello dati del modulo con le origini dati, che si rifletteranno automaticamente nei moduli adattivi e nelle comunicazioni interattive associati.

>[!NOTE]
>
>È necessario essere membri dei gruppi **fdm-author** e **forms-user** per poter creare e utilizzare il modello dati del modulo. Contattate il vostro amministratore AEM per diventare membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Assicurarsi di aver configurato le origini dati che si desidera utilizzare nel modello dati del modulo come descritto in [Configura origini dati](../../forms/using/configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, effettuare le seguenti operazioni:

1. NellAEMistanza di creazione, passare a **[!UICONTROL Forms > Integrazioni dati]**.
1. Toccare **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo:

   * Specificare un nome per il modello dati del modulo.
   * (**Facoltativo**) Specificare titolo, descrizione e tag per il modello dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate**) Toccare l&#39;icona di spunta accanto al campo **[!UICONTROL Configurazione origine dati]** e selezionare il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che si desidera utilizzare. Limita l&#39;elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, qualsiasi database JDBC e AEM origini dati profilo utente sono elencate per impostazione predefinita. Se non si seleziona un nodo di configurazione, vengono elencate le origini dati provenienti da tutti i nodi di configurazione.

   Toccare **[!UICONTROL Next]**.

1. (**Applicabile solo se le origini dati sono configurate**) La schermata **[!UICONTROL Seleziona origine dati]** elenca le eventuali origini dati disponibili. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Toccare **[!UICONTROL Crea]** e nella finestra di dialogo di conferma, toccare **[!UICONTROL Apri]** per aprire l&#39;editor del modello dati del modulo.

Esaminiamo i diversi componenti dell&#39;interfaccia utente dell&#39;editor modelli dati del modulo.

![Un modello dati modulo con tre origini dati: un servizio RESTful, AEM profilo utente e un RDBMS](assets/fdm-ui.png)

**A. Origini** datiElenca le origini dati in un modello dati del modulo. Espandere un&#39;origine dati per visualizzare gli oggetti e i servizi del modello dati.

**B. Aggiorna** definizioni origine dati: rileva tutte le modifiche nelle definizioni delle origini dati da origini dati configurate e le aggiorna nella scheda Origini dati dell&#39;editor del modello dati del modulo.

**C. Area** ModelContent in cui vengono visualizzati gli oggetti modello dati aggiunti.

**D. Area** ServiziContenuto in cui vengono visualizzate le operazioni o i servizi di origine dati aggiunti.

**E.** Barra degli strumentiStrumenti per l&#39;utilizzo del modello dati del modulo. La barra degli strumenti presenta più opzioni a seconda dell&#39;oggetto selezionato nel modello dati del modulo.

**F. Aggiungi** selezionatoAggiunge oggetti e servizi del modello dati selezionati al modello dati del modulo.

Per ulteriori informazioni sull&#39;editor del modello dati del modulo e su come utilizzarlo per modificare e configurare il modello dati del modulo, vedere [Uso del modello dati del modulo](../../forms/using/work-with-form-data-model.md).

## Aggiorna origini dati {#update}

Per aggiungere o aggiornare le origini dati a un modello dati del modulo esistente, effettuare le operazioni seguenti.

1. Passare a **[!UICONTROL Forms > Integrazioni dati]**, selezionare il modello dati del modulo in cui si desidera aggiungere o aggiornare le origini dati, quindi toccare **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati del modulo, passare alla scheda **[!UICONTROL Aggiorna origine]**.

   Nella scheda Aggiorna origine:

   * Toccate l&#39;icona Sfoglia nel campo **[!UICONTROL Configurazione in base al contesto]** e selezionate un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati da aggiungere. Se non si seleziona un nodo, le configurazioni cloud residenti solo nel nodo `global` vengono elencate quando si tocca **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, toccare **[!UICONTROL Aggiungi origini]** e selezionare le origini dati da aggiungere al modello dati del modulo. Vengono visualizzate tutte le origini dati configurate in `global` e l&#39;eventuale nodo di configurazione selezionato.

   * Per sostituire un&#39;origine dati esistente con un&#39;altra origine dati dello stesso tipo, toccare l&#39;icona **[!UICONTROL Edit]** per l&#39;origine dati e selezionare dall&#39;elenco delle origini dati disponibili.
   * Per eliminare un&#39;origine dati esistente, toccate l&#39;icona **[!UICONTROL Elimina]** per l&#39;origine dati. L&#39;icona Elimina è disattivata se un oggetto del modello dati nell&#39;origine dati viene aggiunto nel modello dati del modulo.

   ![fdm-properties](assets/fdm-properties.png)

1. Toccate **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurarsi di aggiornare i riferimenti di binding, come appropriato, nei moduli adattivi e nelle comunicazioni interattive che utilizzano il modello dati del modulo aggiornato.

## Passaggi successivi {#next-steps}

È ora disponibile un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati del modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti del modello dati, modificare proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, vedere [Uso del modello dati del modulo](../../forms/using/work-with-form-data-model.md).
