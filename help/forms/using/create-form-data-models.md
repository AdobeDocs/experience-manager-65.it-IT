---
title: Crea modello dati modulo
seo-title: Create form data model
description: Scopri come creare modelli di dati per moduli con o senza origini dati configurate.
seo-description: Learn how to create form data models with or without configured data sources.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
feature: Form Data Model
exl-id: 7f5978c3-6c9f-4ce4-b0fb-660ac1d49244
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# Crea modello dati modulo{#create-form-data-model}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models.html) |
| AEM 6.5 | Questo articolo |


![immagine protagonista](do-not-localize/data-integration.png)

L’integrazione dei dati in AEM Forms fornisce un’interfaccia utente intuitiva per la creazione e l’utilizzo dei modelli di dati dei moduli. Un modello dati modulo si basa su origini dati per lo scambio di dati. È tuttavia possibile creare un modello dati modulo con o senza un&#39;origine dati. Esistono due approcci per creare un modello dati da a seconda che siano state configurate o meno le origini dati:

* **Utilizzo di origini dati preconfigurate**: se hai configurato le origini dati come descritto in [Configurare le origini dati](../../forms/using/configure-data-sources.md), è possibile selezionarli durante la creazione di un modello di dati del modulo. Raccoglie tutti gli oggetti, le proprietà e i servizi del modello dati dalle origini dati selezionate disponibili per l’utilizzo nel modello dati del modulo.

* **Senza origini dati**: se non hai configurato le origini dati per il modello dati del modulo, puoi comunque crearlo senza origini dati. Puoi utilizzare il modello dati del modulo per creare moduli adattivi e per la comunicazione interattiva e testarli utilizzando dati di esempio. Quando le origini dati sono disponibili, è possibile associare il modello dati del modulo a origini dati che si rifletteranno automaticamente nei moduli adattivi associati e nelle comunicazioni interattive.

>[!NOTE]
>
>Devi essere membro di entrambi **fdm-author** e **forms-user** gruppi per creare e utilizzare il modello dati del modulo. Contatta il tuo amministratore AEM per diventare membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Verifica di aver configurato le origini dati che intendi utilizzare nel modello dati del modulo come descritto in [Configurare le origini dati](../../forms/using/configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, eseguire le operazioni seguenti:

1. Nell’istanza di authoring dell’AEM, passa a **[!UICONTROL Forms > Integrazioni dati]**.
1. Tocca **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo:

   * Specifica un nome per il modello dati del modulo.
   * (**Facoltativo**) Specifica titolo, descrizione e tag per il modello di dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate** a) Toccare l&#39;icona di spunta accanto al **[!UICONTROL Configurazione origine dati]** e seleziona il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che desideri utilizzare. Limita l’elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, per impostazione predefinita vengono elencati tutti i database JDBC e le origini dati del profilo utente AEM. Se non si seleziona un nodo di configurazione, vengono elencate le origini dati di tutti i nodi di configurazione.

   Tocca **[!UICONTROL Successivo]**.

1. (**Applicabile solo se le origini dati sono configurate**) La **[!UICONTROL Seleziona origine dati]** nella schermata sono elencate le origini dati disponibili, se presenti. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Tocca **[!UICONTROL Crea]** e nella finestra di dialogo di conferma tocca **[!UICONTROL Apri]** per aprire l&#39;editor modello dati modulo.

Esaminiamo i diversi componenti dell’interfaccia utente dell’editor dei modelli di dati dei moduli.

![Un modello di dati modulo con tre origini dati: un servizio RESTful, un profilo utente AEM e un RDBMS](assets/fdm-ui.png)

**A. Origini dati** Elenca le origini dati in un modello dati modulo. Espandere un&#39;origine dati per visualizzare i relativi servizi e oggetti modello dati.

**B. Aggiornare le definizioni delle origini dati** Recupera eventuali modifiche nelle definizioni dell’origine dati dalle origini dati configurate e le aggiorna nella scheda Origini dati dell’editor modelli dati del modulo.

**C. Modello** Area contenuto in cui vengono visualizzati gli oggetti modello dati aggiunti.

**D. Servizi** Area del contenuto in cui vengono visualizzati operazioni o servizi dell&#39;origine dati aggiunti.

**E. Barra degli strumenti** Strumenti per utilizzare il modello dati del modulo. La barra degli strumenti mostra più opzioni a seconda dell’oggetto selezionato nel modello dati del modulo.

**F. Aggiungi selezionati** Aggiunge al modello dati del modulo gli oggetti e i servizi modello dati selezionati.

Per ulteriori informazioni sull’editor del modello dati modulo e su come utilizzarlo per modificare e configurare il modello dati modulo, consulta [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md).

## Aggiornare le origini dati {#update}

Per aggiungere o aggiornare origini dati a un modello dati modulo esistente, eseguire le operazioni seguenti.

1. Vai a **[!UICONTROL Forms > Integrazioni dati]**, seleziona il modello di dati del modulo in cui desideri aggiungere o aggiornare le origini dati e tocca **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati del modulo, vai al **[!UICONTROL Aggiorna origine]** scheda.

   Nella scheda Aggiorna origine:

   * Tocca l’icona Sfoglia in **[!UICONTROL Configurazione in base al contesto]** e selezionare un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati che si desidera aggiungere. Se non selezioni un nodo, le configurazioni cloud che risiedono solo nel `global` Il nodo viene elencato quando tocchi **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, tocca **[!UICONTROL Aggiungi origini]** e seleziona le origini dati da aggiungere al modello dati del modulo. Tutte le origini dati configurate in `global` e viene visualizzato il nodo di configurazione selezionato, se presente.

   * Per sostituire un’origine dati esistente con un’altra origine dati dello stesso tipo, tocca il **[!UICONTROL Modifica]** per l&#39;origine dati e selezionarla dall&#39;elenco delle origini dati disponibili.
   * Per eliminare un’origine dati esistente, tocca il **[!UICONTROL Elimina]** per l&#39;origine dati. L’icona Elimina è disabilitata se nel modello dati del modulo viene aggiunto un oggetto modello dati nell’origine dati.

   ![fdm-properties](assets/fdm-properties.png)

1. Tocca **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurati di aggiornare i riferimenti di associazione, a seconda delle necessità, nei moduli adattivi e nelle comunicazioni interattive che utilizzano il modello dati del modulo aggiornato.

## Passaggi successivi {#next-steps}

Ora disponi di un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati del modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti del modello dati, modificare proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, consulta [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md).
