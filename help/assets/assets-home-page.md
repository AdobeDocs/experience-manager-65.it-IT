---
title: "[!DNL Assets] Esperienza con la pagina iniziale"
description: Personalizzare [!DNL Experience Manager Assets] Pagina Home per un’esperienza ricca di schermate di benvenuto, inclusa un’istantanea delle attività recenti relative alle risorse.
contentOwner: AG
feature: Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets] Esperienza pagina iniziale {#aem-assets-home-page-experience}

Personalizzare [!DNL Adobe Experience Manager Assets] home page per un’esperienza avanzata con la schermata di benvenuto, inclusa un’istantanea delle attività recenti relative alle risorse.

[!DNL Assets] la pagina principale offre un’esperienza della schermata di benvenuto ricca e personalizzata, che include un’istantanea delle attività recenti, ad esempio le risorse visualizzate o caricate di recente.

Il [!DNL Assets] la home page è disabilitata per impostazione predefinita. Per attivarla, effettuare le seguenti operazioni:

1. Apri [!DNL Experience Manager] Gestione configurazione `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Day CQ DAM Event Recorder]** servizio.
1. Seleziona la **[!UICONTROL Abilita questo servizio]** per abilitare la registrazione delle attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dalla sezione **[!UICONTROL Tipi di evento]** selezionare gli eventi da registrare e salvare le modifiche.

   >[!CAUTION]
   >
   >L’abilitazione delle opzioni Risorsa visualizzata, Progetti visualizzati e Raccolte visualizzate aumenta in modo significativo il numero di eventi registrati.

1. Apri **[!UICONTROL Flag per funzione Home page risorse DAM]** servizio da Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleziona la `isEnabled.name` per abilitare [!DNL Assets] Funzione della pagina iniziale. Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Apri **[!UICONTROL Preferenze utente]** e seleziona **[!UICONTROL Abilita pagina iniziale risorse]**. Salva le modifiche.

   ![Abilitare la pagina iniziale delle risorse nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver abilitato [!DNL Assets] Home page, passa alla [!DNL Assets] interfaccia utente dalla pagina Navigazione o accedervi direttamente dall&#39;URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurare il collegamento esperienza nell’interfaccia utente di Assets](assets/config-experience-link.png)

Fai clic su **[!UICONTROL Fai clic qui per configurare il collegamento esperienza]** per aggiungere il nome utente, l&#39;immagine di sfondo e l&#39;immagine del profilo.

Il [!DNL Assets] La home page include le sezioni seguenti:

* Sezione di benvenuto
* Sezione widget

**Sezione di benvenuto**

Se il profilo esiste, nella sezione Benvenuti viene visualizzato un messaggio di benvenuto indirizzato all&#39;utente. Inoltre, mostra l’immagine del profilo e un’immagine di benvenuto (se configurata già).

Se il profilo è incompleto, nella sezione Benvenuti vengono visualizzati un messaggio di benvenuto generico e un segnaposto per l&#39;immagine del profilo.

**Sezione widget**

Questa sezione viene visualizzata sotto la sezione Benvenuti e mostra i widget predefiniti nelle sezioni seguenti:

* Attività
* Recente
* Scopri

**Attività**: sotto questa sezione, il **[!UICONTROL La mia attività]** il widget mostra le attività recenti eseguite dall’utente connesso con risorse (incluse le risorse senza rendering), ad esempio caricamenti, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni di risorse.

**Recente**: Il **[!UICONTROL Visualizzato di recente]** in questa sezione vengono visualizzate le entità a cui l&#39;utente connesso ha effettuato l&#39;accesso di recente, incluse cartelle, raccolte e progetti.

**Scoprire**: Il **[!UICONTROL Nuovo]** Il widget sotto questa sezione mostra le risorse e le rappresentazioni caricate di recente nel [!DNL Assets] distribuzione.

Per abilitare la rimozione dei dati delle attività utente, abilita **[!UICONTROL Servizio di eliminazione eventi DAM]** da Configuration Manager. Dopo aver attivato questo servizio, le attività dell&#39;utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata iniziale fornisce semplici strumenti di navigazione, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>Abilitazione di [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL Eliminazione eventi DAM] servizi aumenta le operazioni di scrittura in JCR e l’indicizzazione della ricerca, il che aumenta in modo significativo il carico sul [!DNL Experience Manager] server. Il carico aggiuntivo sul [!DNL Experience Manager] il server può influire sulle prestazioni.

>[!CAUTION]
>
>Acquisizione, filtraggio ed eliminazione delle attività utente necessarie per [!DNL Assets] La pagina Home di impone un sovraccarico sulle prestazioni. Pertanto, gli amministratori devono configurare la pagina Home in modo efficace per gli utenti target.
>
>L’Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione Pagina iniziale risorse per impedire un aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Day CQ DAM Event Recorder] da [!UICONTROL Gestione configurazione].
>
>Se utilizzi la funzione, Adobe consiglia di pianificare la frequenza di eliminazione in base al caricamento del server.
