---
title: Crea modello dati modulo
seo-title: Crea modello dati modulo
description: Scopri come creare modelli di dati modulo con o senza origini dati configurate.
seo-description: Scopri come creare modelli di dati modulo con o senza origini dati configurate.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
feature: Form Data Model
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---


# Crea modello dati modulo{#create-form-data-model}

![](do-not-localize/data-integeration.png)

L’integrazione dei dati di AEM Forms fornisce un’interfaccia utente intuitiva per creare e utilizzare modelli di dati dei moduli. Un modello di dati modulo si basa su origini dati per lo scambio di dati; tuttavia, è possibile creare un modello dati modulo con o senza un’origine dati. Esistono due approcci per creare un modello dati da a seconda che siano state configurate origini dati:

* **Utilizzo di origini** dati preconfigurate: Se sono state configurate origini dati come descritto in  [Configurazione origini dati](../../forms/using/configure-data-sources.md), è possibile selezionarle durante la creazione di un modello dati del modulo. Porta tutti gli oggetti, le proprietà e i servizi del modello dati dalle origini dati selezionate disponibili per l’uso nel modello dati del modulo.

* **Senza origini** dati: Se non sono state configurate origini dati per il modello dati del modulo, è comunque possibile crearlo senza origini dati. È possibile utilizzare il modello dati del modulo per creare moduli adattivi e comunicazioni interattive e testarli utilizzando dati di esempio. Quando sono disponibili origini dati, è possibile eseguire un binding del modello dati del modulo con origini dati, che si rifletteranno automaticamente nei moduli adattivi e nelle comunicazioni interattive associate.

>[!NOTE]
>
>È necessario essere membri sia dei gruppi **fdm-author** che **forms-user** per poter creare e utilizzare il modello dati del modulo. Contatta il tuo amministratore AEM per diventare membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Assicurarsi di aver configurato le origini dati che si intende utilizzare nel modello dati del modulo come descritto in [Configurare origini dati](../../forms/using/configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, procedere come segue:

1. Nell&#39;istanza AEM autore, passa a **[!UICONTROL Forms > Integrazioni dati]**.
1. Tocca **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo :

   * Specificare un nome per il modello dati del modulo.
   * (**Facoltativo**) Specifica il titolo, la descrizione e i tag per il modello dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate**) Toccare l&#39;icona di spunta accanto al campo **[!UICONTROL Configurazione origine dati]** e selezionare il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che si desidera utilizzare. Limita l’elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, qualsiasi database JDBC e origini dati AEM profilo utente sono elencate per impostazione predefinita. Se non selezioni un nodo di configurazione, vengono elencate le origini dati da tutti i nodi di configurazione.

   Tocca **[!UICONTROL Avanti]**.

1. (**Applicabile solo se le origini dati sono configurate**) La schermata **[!UICONTROL Seleziona origine dati]** elenca le eventuali origini dati disponibili. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Tocca **[!UICONTROL Crea]** e nella finestra di dialogo di conferma, tocca **[!UICONTROL Apri]** per aprire l’editor del modello di dati del modulo.

Esaminiamo i diversi componenti dell’interfaccia utente dell’editor dei modelli di dati per moduli.

![Un modello di dati modulo con tre origini dati: un servizio RESTful, un profilo utente AEM e un RDBMS](assets/fdm-ui.png)

**A.** Origini datiElenca le origini dati in un modello dati del modulo. Espandere un’origine dati per visualizzare gli oggetti e i servizi del modello dati corrispondente.

**B. Aggiorna** definizioni origine datiRecupera le modifiche nelle definizioni delle origini dati da origini dati configurate e le aggiorna nella scheda Origini dati dell&#39;editor del modello dati del modulo.

**C. Area** ModelContent in cui vengono visualizzati gli oggetti modello dati aggiunti.

**D. Area** ServiziContenuto in cui vengono visualizzate operazioni o servizi di origine dati aggiunti.

**E.** ToolbarStrumenti per lavorare con il modello dati del modulo. La barra degli strumenti mostra più opzioni a seconda dell’oggetto selezionato nel modello dati del modulo.

**F. Aggiungi** selezionatiAggiunge gli oggetti e i servizi del modello dati selezionato al modello dati del modulo.

Per ulteriori informazioni sull&#39;editor del modello dati del modulo e su come utilizzarlo per modificare e configurare il modello dati del modulo, vedere [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md).

## Aggiorna origini dati {#update}

Per aggiungere o aggiornare origini dati a un modello dati modulo esistente, procedere come segue.

1. Vai a **[!UICONTROL Forms > Integrazioni dati]**, seleziona il modello di dati del modulo in cui desideri aggiungere o aggiornare origini dati e tocca **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati del modulo, passare alla scheda **[!UICONTROL Aggiorna origine]** .

   Nella scheda Aggiorna origine :

   * Tocca l&#39;icona Sfoglia nel campo **[!UICONTROL Configurazione in base al contesto]** e seleziona un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati che desideri aggiungere. Se non selezioni un nodo, le configurazioni cloud che risiedono solo nel nodo `global` vengono elencate quando tocchi **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, toccare **[!UICONTROL Aggiungi origini]** e selezionare le origini dati da aggiungere al modello dati del modulo. Vengono visualizzate tutte le origini dati configurate in `global` e l&#39;eventuale nodo di configurazione selezionato.

   * Per sostituire un’origine dati esistente con un’altra origine dati dello stesso tipo, tocca l’icona **[!UICONTROL Modifica]** per l’origine dati e seleziona dall’elenco delle origini dati disponibili.
   * Per eliminare un’origine dati esistente, tocca l’icona **[!UICONTROL Elimina]** dell’origine dati. L’icona Elimina è disabilitata se un oggetto modello dati nell’origine dati viene aggiunto nel modello dati del modulo.

   ![proprietà fdm](assets/fdm-properties.png)

1. Tocca **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurarsi di aggiornare i riferimenti di binding, se appropriato, nei moduli adattivi e nelle comunicazioni interattive che utilizzano il modello dati del modulo aggiornato.

## Passaggi successivi {#next-steps}

Ora è disponibile un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati del modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti modello dati, modificare proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, vedere [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md).
