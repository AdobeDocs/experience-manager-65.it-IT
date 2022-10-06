---
title: "[!DNL Assets] Home Page experience"
description: Personalizza le [!DNL Experience Manager Assets] Pagina principale per un’esperienza ricca di schermate di benvenuto, che include un’istantanea delle attività recenti relative alle risorse.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] Esperienza home page {#aem-assets-home-page-experience}

Personalizza le [!DNL Adobe Experience Manager Assets] pagina principale per un’esperienza ricca di schermate di benvenuto, che include un’istantanea delle attività recenti relative alle risorse.

[!DNL Assets] home page offre un’esperienza ricca e personalizzata con schermata di benvenuto, che include un’istantanea delle attività recenti, come le risorse visualizzate o caricate di recente.

La [!DNL Assets] la home page è disabilitata per impostazione predefinita. Per abilitarlo, esegui le seguenti operazioni:

1. Apri [!DNL Experience Manager] Gestione configurazione `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Day CQ DAM Event Recorder]** servizio.
1. Seleziona la **[!UICONTROL Abilita questo servizio]** per abilitare la registrazione dell’attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Da **[!UICONTROL Tipi di eventi]** seleziona gli eventi da registrare e salva le modifiche.

   >[!CAUTION]
   >
   >Attivando le opzioni di visualizzazione Risorsa visualizzata, Progetti visualizzati e Raccolte, si aumenta in modo significativo il numero di eventi registrati.

1. Apri **[!UICONTROL Flag di funzione della pagina iniziale della risorsa DAM]** servizio da Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleziona la `isEnabled.name` per abilitare [!DNL Assets] Funzionalità della home page. Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Apri **[!UICONTROL Preferenze utente]** e seleziona **[!UICONTROL Abilita pagina iniziale risorse]**. Salva le modifiche.

   ![Abilita la home page delle risorse nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver abilitato la [!DNL Assets] Home page, passare alla [!DNL Assets] Interfaccia utente dalla pagina Navigazione o accesso diretto dall’URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurare il collegamento esperienza sull’interfaccia utente Assets](assets/config-experience-link.png)

Fai clic sul pulsante **[!UICONTROL Fai clic qui per configurare il collegamento esperienza]** per aggiungere nome utente, immagine di sfondo e immagine di profilo.

La [!DNL Assets] La home page include le sezioni seguenti:

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

**Attività**: In questa sezione, il **[!UICONTROL Attività personale]** widget visualizza le attività recenti eseguite dall’utente connesso con risorse (incluse risorse senza rendering), ad esempio caricamenti di risorse, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni.

**Recente**: La **[!UICONTROL Visualizzato di recente]** in questa sezione vengono visualizzate le entità a cui l&#39;utente ha effettuato l&#39;accesso, incluse cartelle, raccolte e progetti.

**Scopri**: La **[!UICONTROL Nuovo]** in questa sezione vengono visualizzate le risorse e i rendering caricati di recente in [!DNL Assets] distribuzione.

Per abilitare l’eliminazione dei dati dell’attività utente, abilita **[!UICONTROL Servizio di eliminazione degli eventi DAM]** da Configuration Manager. Dopo aver abilitato questo servizio, le attività dell&#39;utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata introduttiva fornisce semplici strumenti di navigazione, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>Abilitazione della [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL Eliminazione degli eventi DAM] i servizi aumentano le operazioni di scrittura su JCR e l&#39;indicizzazione della ricerca, che aumenta in modo significativo il carico sul [!DNL Experience Manager] server. Il carico aggiuntivo sul [!DNL Experience Manager] il server può influire sulle sue prestazioni.

>[!CAUTION]
>
>Acquisizione, filtraggio ed eliminazione delle attività utente necessarie per [!DNL Assets] home page imporre un sovraccarico sulle prestazioni. Pertanto, gli amministratori devono configurare la home page in modo efficace per gli utenti target.
>
>L’Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione Home page della risorsa per evitare un aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Day CQ DAM Event Recorder] da [!UICONTROL Gestione configurazione].
>
>Se utilizzi questa funzione, Adobe consiglia di pianificare la frequenza di eliminazione in base al carico del server.
