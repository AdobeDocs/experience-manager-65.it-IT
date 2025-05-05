---
title: Crea modello dati modulo
description: Scopri come creare modelli di dati per moduli con o senza origini dati configurate.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
exl-id: 7f5978c3-6c9f-4ce4-b0fb-660ac1d49244
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---

# Crea modello dati modulo{#create-form-data-model}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models.html?lang=it) |
| AEM 6.5 | Questo articolo |


![immagine protagonista](do-not-localize/data-integration.png)

L’integrazione dei dati in AEM Forms fornisce un’interfaccia utente intuitiva per la creazione e l’utilizzo dei modelli di dati dei moduli. Un modello dati modulo si basa su origini dati per lo scambio di dati. È tuttavia possibile creare un modello dati modulo con o senza un&#39;origine dati. Esistono due approcci per creare un modello dati da a seconda che siano state configurate o meno le origini dati:

* **Utilizzo di origini dati preconfigurate**: se le origini dati sono state configurate come descritto in [Configurazione di origini dati](../../forms/using/configure-data-sources.md), è possibile selezionarle durante la creazione di un modello dati del modulo. Raccoglie tutti gli oggetti, le proprietà e i servizi del modello dati dalle origini dati selezionate disponibili per l’utilizzo nel modello dati del modulo.

* **Senza origini dati**: se non sono state configurate origini dati per il modello dati del modulo, è comunque possibile crearlo senza origini dati. Puoi utilizzare il modello dati del modulo per creare moduli adattivi e per la comunicazione interattiva e testarli utilizzando dati di esempio. Quando le origini dati sono disponibili, è possibile associare il modello dati del modulo a origini dati che si rifletteranno automaticamente nei moduli adattivi associati e nelle comunicazioni interattive.

>[!NOTE]
>
>Per poter creare e utilizzare il modello di dati del modulo, è necessario essere membri sia del gruppo **fdm-author** che del gruppo **forms-user**. Contatta il tuo amministratore AEM per diventare membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Verificare di aver configurato le origini dati che si intende utilizzare nel modello dati del modulo come descritto in [Configurare le origini dati](../../forms/using/configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, eseguire le operazioni seguenti:

1. Nell&#39;istanza di authoring dell&#39;AEM, passa a **[!UICONTROL Forms > Integrazioni dati]**.
1. Selezionare **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo:

   * Specifica un nome per il modello dati del modulo.
   * (**Facoltativo**) Specificare titolo, descrizione e tag per il modello dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate**) Selezionare l&#39;icona di spunta accanto al campo **[!UICONTROL Configurazione Source dati]** e selezionare il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che si desidera utilizzare. Limita l’elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, per impostazione predefinita vengono elencati tutti i database JDBC e le origini dati del profilo utente AEM. Se non si seleziona un nodo di configurazione, vengono elencate le origini dati di tutti i nodi di configurazione.

   Seleziona **[!UICONTROL Avanti]**.

1. (**Applicabile solo se le origini dati sono configurate**) Nella schermata **[!UICONTROL Seleziona origine dati]** sono elencate le origini dati disponibili, se presenti. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Seleziona **[!UICONTROL Crea]** e nella finestra di dialogo di conferma seleziona **[!UICONTROL Apri]** per aprire l&#39;editor del modello dati del modulo.

Esaminiamo i diversi componenti dell’interfaccia utente dell’editor dei modelli di dati dei moduli.

![Un modello di dati modulo con tre origini dati: un servizio RESTful, un profilo utente AEM e un RDBMS](assets/fdm-ui.png)

**A. Origini dati** Elenca le origini dati in un modello dati modulo. Espandere un&#39;origine dati per visualizzare i relativi servizi e oggetti modello dati.

**B. Aggiorna definizioni Data Source** Recupera eventuali modifiche nelle definizioni dell&#39;origine dati dalle origini dati configurate e le aggiorna nella scheda Origini dati dell&#39;editor modelli dati del modulo.

**C. Area contenuto modello** in cui vengono visualizzati gli oggetti modello dati aggiunti.

**G. Servizi** Area contenuto in cui vengono visualizzati operazioni o servizi dell&#39;origine dati aggiunti.

**E. Barra degli strumenti** Strumenti per l&#39;utilizzo del modello dati del modulo. La barra degli strumenti mostra più opzioni a seconda dell’oggetto selezionato nel modello dati del modulo.

**F. Aggiungi selezionati** Aggiunge gli oggetti e i servizi del modello dati selezionati al modello dati del modulo.

Per ulteriori informazioni sull&#39;editor del modello dati modulo e su come utilizzarlo per modificare e configurare il modello dati modulo, vedere [Utilizzare il modello dati modulo](../../forms/using/work-with-form-data-model.md).

## Aggiornare le origini dati {#update}

Per aggiungere o aggiornare origini dati a un modello dati modulo esistente, eseguire le operazioni seguenti.

1. Vai a **[!UICONTROL Forms > Integrazioni dati]**, seleziona il modello dati del modulo in cui desideri aggiungere o aggiornare le origini dati e seleziona **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati del modulo, vai alla scheda **[!UICONTROL Aggiorna Source]**.

   Nella scheda Aggiorna Source:

   * Selezionare l&#39;icona Sfoglia nel campo **[!UICONTROL Configurazione in base al contesto]** e selezionare un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati che si desidera aggiungere. Se non si seleziona un nodo, le configurazioni cloud che risiedono solo nel nodo `global` vengono elencate quando si seleziona **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, selezionare **[!UICONTROL Aggiungi origini]** e selezionare le origini dati da aggiungere al modello dati del modulo. Vengono visualizzate tutte le origini dati configurate in `global` e l&#39;eventuale nodo di configurazione selezionato.

   * Per sostituire un&#39;origine dati esistente con un&#39;altra origine dati dello stesso tipo, selezionare l&#39;icona **[!UICONTROL Modifica]** per l&#39;origine dati e selezionarla dall&#39;elenco delle origini dati disponibili.
   * Per eliminare un&#39;origine dati esistente, selezionare l&#39;icona **[!UICONTROL Elimina]** per l&#39;origine dati. L’icona Elimina è disabilitata se nel modello dati del modulo viene aggiunto un oggetto modello dati nell’origine dati.

   ![fdm-properties](assets/fdm-properties.png)

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurati di aggiornare i riferimenti di associazione, a seconda delle necessità, nei moduli adattivi e nelle comunicazioni interattive che utilizzano il modello dati del modulo aggiornato.

## Passaggi successivi {#next-steps}

Ora disponi di un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati del modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti del modello dati, modificare proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, vedere [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md).
