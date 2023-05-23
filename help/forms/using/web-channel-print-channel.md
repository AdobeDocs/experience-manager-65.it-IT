---
title: Canale di stampa e canale web
seo-title: Print channel and web channel
description: Importazione di modelli di canale di stampa e creazione e abilitazione di modelli di canale web
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Canale di stampa e canale web{#print-channel-and-web-channel}

Le comunicazioni interattive possono essere distribuite attraverso due canali: stampa e web. Il canale di stampa viene utilizzato per creare PDF e comunicazioni cartacee, ad esempio una lettera stampata come promemoria per il pagamento del premio assicurativo, mentre il canale web viene utilizzato per fornire esperienze online, ad esempio l’estratto conto di una carta di credito su un sito web.

Gli autori delle comunicazioni interattive possono riutilizzare risorse quali frammenti di documenti e immagini per creare versioni stampate e web delle comunicazioni interattive.

Uno dei prerequisiti per [Creazione di una comunicazione interattiva](../../forms/using/create-interactive-communication.md) deve avere i modelli per la stampa e/o il canale web disponibili sul server. Mentre gli autori di modelli creano il modello di canale web nello stesso AEM, il modello di canale di stampa XDP viene creato in Adobe Forms Designer e caricato sul server.

## Stampa canale {#printchannel}

Il canale di stampa di una comunicazione interattiva utilizza il modello di modulo XFA, XDP. Un XDP è progettato in Adobe Forms Designer. Per ulteriori informazioni sulla creazione di modelli di canale di stampa, vedere [Progettazione layout](../../forms/using/layout-design-details.md). Per utilizzare un modello di canale di stampa nella comunicazione interattiva, devi caricarlo nel server di AEM Forms.

### Carica modello di canale di stampa comunicazione interattiva {#upload-interactive-communication-print-channel-template}

Per caricare il modello, devi essere membro del gruppo utenti di forms. Per caricare il modello del canale di stampa (XDP) in AEM Forms, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**.

   Individua e seleziona il modello di canale di stampa (XDP) appropriato, quindi tocca **[!UICONTROL Apri]**.

## Canale web {#web-channel}

Gli autori e gli amministratori di modelli possono creare, modificare e abilitare i modelli web. Per consentire ad altri utenti di creare modelli Web, devi assegnare loro i diritti necessari. Per ulteriori informazioni, consulta [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md).

### Authoring di un modello di canale web {#authoring-web-channel-template}

Per creare un modello di canale web, devi prima creare una cartella di modelli. Dopo aver creato un modello Web all&#39;interno di una cartella di modelli, è necessario abilitare il modello per consentire agli utenti dei moduli di creare un canale Web di una comunicazione interattiva basata sul modello.

La procedura seguente illustra come creare un modello di canale web:

1. Crea una cartella di modelli per mantenere i modelli web di comunicazione interattiva, se non ne hai già uno. Per ulteriori informazioni, consulta Cartelle modelli in [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md).

   1. Tocca **[!UICONTROL Strumenti]** ![strumenti](assets/tools.png) > **[!UICONTROL Browser configurazioni]**.
      * Consulta la [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.
   1. Nella pagina Browser configurazioni, tocca **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella, seleziona **[!UICONTROL Modelli modificabili]**, e tocca **[!UICONTROL Crea]**.

      La cartella viene creata ed elencata nella pagina Browser configurazioni.

1. Passa alla cartella dei modelli appropriata e crea un modello web.

   1. Passare alla cartella dei modelli appropriata selezionando **[!UICONTROL Strumenti]** > **[!UICONTROL Modelli]** > **`[Folder]`**.
   1. Tocca **[!UICONTROL Crea]**.
   1. Seleziona **[!UICONTROL Comunicazione interattiva - Canale web]** e tocca **[!UICONTROL Successivo]**.
   1. Inserisci un titolo e una descrizione per il modello, quindi tocca **[!UICONTROL Crea]**.

      Il modello viene creato e viene visualizzata una finestra di dialogo.

   1. Tocca **[!UICONTROL Apri]** per aprire il modello creato nell’editor di modelli.

      Viene visualizzato l&#39;Editor modelli.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Durante la creazione o la modifica di un modello, un autore di modelli può definire diversi aspetti. La creazione o la modifica di un modello è simile all’authoring delle pagine. Per ulteriori informazioni, consulta Modifica di modelli - Autori di modelli in [Creazione di modelli di pagina](/help/sites-authoring/templates.md).

1. Per consentire l’utilizzo di questo modello per la creazione di comunicazioni interattive, abilita il modello.

   1. Tocca **[!UICONTROL Strumenti]** ![strumenti](assets/tools.png) > **[!UICONTROL Modelli]**.
   1. Passa al modello appropriato, selezionalo e tocca **[!UICONTROL Abilita]** e nel messaggio di avviso, tocca **[!UICONTROL Abilita]**.

      Il modello è abilitato e il suo stato viene visualizzato come Abilitato. Ora puoi procedere alla creazione di una comunicazione interattiva in cui puoi utilizzare il modello di canale web appena creato.

### Stampa canale come master per canale web {#print-channel-as-master-for-web-channel}

Durante l’authoring di una comunicazione interattiva, gli autori possono selezionare questa opzione per creare il canale web in sincronia con il canale di stampa. L’utilizzo del canale di stampa come master per il canale web assicura che il contenuto, l’ereditarietà e l’associazione dati del canale web siano derivati dal canale di stampa e che le modifiche apportate nel canale di stampa possano essere riflesse nel canale web. Gli autori delle comunicazioni interattive, tuttavia, possono interrompere l’ereditarietà di componenti specifici nel canale web, in base alle esigenze.

![Stampa canale come principale](assets/create_ic_print_master_new.png) ![Canale web con canale di stampa come principale](assets/create_ic_print_master_web_new.png)
