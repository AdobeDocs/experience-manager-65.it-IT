---
title: '[!DNL Assets] Esperienza della home page'
description: Personalizza la  [!DNL Experience Manager Assets] home page per un’esperienza ricca di schermate di benvenuto, inclusa un’istantanea delle attività recenti relative alle risorse.
contentOwner: AG
feature: Strumenti per sviluppatori, gestione delle risorse
role: Amministratore, Business Practices
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Esperienza home page  {#aem-assets-home-page-experience}

Personalizza la home page di [!DNL Adobe Experience Manager Assets] per un’esperienza ricca di schermate di benvenuto, inclusa un’istantanea delle attività recenti relative alle risorse.

[!DNL Assets] home page offre un’esperienza ricca e personalizzata con schermata di benvenuto, che include un’istantanea delle attività recenti, come le risorse visualizzate o caricate di recente.

La home page [!DNL Assets] è disabilitata per impostazione predefinita. Per abilitarlo, esegui le seguenti operazioni:

1. Apri [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri il servizio **[!UICONTROL Day CQ DAM Event Recorder]** .
1. Seleziona il **[!UICONTROL Abilita questo servizio]** per abilitare la registrazione delle attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dall’elenco **[!UICONTROL Tipi di eventi]**, seleziona gli eventi da registrare e salva le modifiche.

   >[!CAUTION]
   >
   >Attivando le opzioni di visualizzazione Risorsa visualizzata, Progetti visualizzati e Raccolte, si aumenta in modo significativo il numero di eventi registrati.

1. Apri il servizio **[!UICONTROL DAM Asset Home Page Feature Flag]** da Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleziona l’opzione `isEnabled.name` per abilitare la funzione Home page [!DNL Assets] . Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Apri la finestra di dialogo **[!UICONTROL Preferenze utente]** e seleziona **[!UICONTROL Abilita pagina iniziale risorse]**. Salva le modifiche.

   ![Abilita la home page delle risorse nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver abilitato la home page [!DNL Assets], passa all&#39;interfaccia utente [!DNL Assets] dalla pagina Navigazione o accedi direttamente dall&#39;URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurare il collegamento esperienza sull’interfaccia utente Assets](assets/config-experience-link.png)

Fai clic su **[!UICONTROL Fai clic qui per configurare il collegamento esperienza]** per aggiungere nome utente, immagine di sfondo e immagine di profilo.

La home page di [!DNL Assets] include le sezioni seguenti:

* Sezione di benvenuto
* Sezione Widget

**Sezione di benvenuto**

Se il tuo profilo esiste, nella sezione Benvenuto viene visualizzato un messaggio di benvenuto a te indirizzato. Inoltre, mostra l’immagine del tuo profilo e un’immagine di benvenuto (se configurata).

Se il profilo è incompleto, nella sezione Benvenuto vengono visualizzati un messaggio di benvenuto generico e un segnaposto per l’immagine del profilo.

**Sezione Widget**

Questa sezione viene visualizzata sotto la sezione Benvenuto e presenta i widget preconfigurati nelle sezioni seguenti:

* Attività
* Recente
* Scopri

**Attività**: In questa sezione, il  **[!UICONTROL widget]** Attività personale visualizza le attività recenti eseguite dall’utente connesso con risorse (incluse risorse senza rendering), ad esempio caricamenti di risorse, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni.

**Recenti**: Il  **[!UICONTROL widget]** Visualizzato di recente in questa sezione visualizza le entità a cui l’utente ha effettuato l’accesso di recente, incluse cartelle, raccolte e progetti.

**Scopri**: In questa sezione,  **** Newwidget mostra le risorse e i rendering recentemente caricati nella  [!DNL Assets] distribuzione.

Per abilitare l&#39;eliminazione dei dati delle attività utente, abilita il **[!UICONTROL servizio di eliminazione degli eventi DAM]** da Configuration Manager. Dopo aver abilitato questo servizio, le attività dell&#39;utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata introduttiva fornisce semplici strumenti di navigazione, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>L&#39;abilitazione dei servizi [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL DAM Event Purge] aumenta le operazioni di scrittura su JCR e l&#39;indicizzazione della ricerca, il che aumenta notevolmente il carico sul server [!DNL Experience Manager]. Il carico aggiuntivo sul server [!DNL Experience Manager] può influire sulle prestazioni.

>[!CAUTION]
>
>L’acquisizione, il filtraggio e l’eliminazione delle attività utente necessarie per la home page di [!DNL Assets] impongono un sovraccarico alle prestazioni. Pertanto, gli amministratori devono configurare la home page in modo efficace per gli utenti target.
>
>L’Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione Home page della risorsa per evitare un aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Day CQ DAM Event Recorder] da [!UICONTROL Configuration Manager].
>
>Se utilizzi questa funzione, Adobe consiglia di pianificare la frequenza di eliminazione in base al carico del server.
