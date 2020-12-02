---
title: '[!DNL Assets] Esperienza pagina iniziale'
description: Personalizza la pagina principale  [!DNL Experience Manager Assets] per un'esperienza ricca di schermate di benvenuto, con un'istantanea delle attività recenti intorno alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Esperienza pagina iniziale  {#aem-assets-home-page-experience}

Personalizzate la pagina principale [!DNL Adobe Experience Manager Assets] per un&#39;esperienza ricca di schermata di benvenuto, con un&#39;istantanea delle attività recenti intorno alle risorse.

[!DNL Assets] la pagina principale offre un’esperienza sulla schermata di benvenuto ricca e personalizzata, che include un’istantanea delle attività recenti, come le risorse che sono state visualizzate o caricate di recente.

La pagina principale [!DNL Assets] è disabilitata per impostazione predefinita. Per attivarla, effettuare le seguenti operazioni:

1. Aprire [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite il servizio **[!UICONTROL Day CQ DAM Event Recorder]**.
1. Selezionare **[!UICONTROL Abilita questo servizio]** per abilitare la registrazione dell&#39;attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Nell&#39;elenco **[!UICONTROL Tipi di eventi]**, selezionare gli eventi da registrare e salvare le modifiche.

   >[!CAUTION]
   >
   >Abilitando le opzioni di visualizzazione delle risorse, dei progetti visualizzati e delle raccolte, il numero di eventi registrati aumenta notevolmente.

1. Aprite il servizio **[!UICONTROL DAM Asset Home Page Feature Flag]** da Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selezionare l&#39;opzione `isEnabled.name` per abilitare la funzione [!DNL Assets] Home page. Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Aprite la finestra di dialogo **[!UICONTROL Preferenze utente]** e selezionate **[!UICONTROL Abilita pagina iniziale risorse]**. Salva le modifiche.

   ![Abilita pagina principale risorse nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver attivato la pagina principale [!DNL Assets], passare all&#39;interfaccia utente [!DNL Assets] dalla pagina di navigazione o accedervi direttamente dall&#39;URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configura collegamento esperienza nell’interfaccia utente di Risorse](assets/config-experience-link.png)

Fate clic su **[!UICONTROL Fate clic qui per configurare il collegamento esperienza]** per aggiungere il nome utente, l&#39;immagine di sfondo e l&#39;immagine del profilo.

La pagina principale [!DNL Assets] include le seguenti sezioni:

* Sezione Benvenuti
* Sezione Widget

**Sezione Benvenuti**

Se il vostro profilo esiste, nella sezione Benvenuti viene visualizzato un messaggio di benvenuto indirizzato a voi. Inoltre, mostra l&#39;immagine del profilo e un&#39;immagine di benvenuto (se già configurata).

Se il profilo è incompleto, nella sezione Benvenuti vengono visualizzati un messaggio di benvenuto generico e un segnaposto per l&#39;immagine del profilo.

**Sezione Widget**

Questa sezione viene visualizzata sotto la sezione Benvenuti e presenta i widget out-of-the-box nelle seguenti sezioni:

* Attività
* Recente
* Scopri

**Attività**: In questa sezione, il  **[!UICONTROL widget]** Attività personale visualizza le attività recenti svolte dall’utente che ha eseguito l’accesso con risorse (incluse risorse senza rappresentazioni), ad esempio caricamenti di risorse, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni.

**Recente**: Il  **[!UICONTROL widget]** Visualizzato di recente in questa sezione visualizza le entità a cui l&#39;utente ha effettuato l&#39;accesso di recente, comprese cartelle, raccolte e progetti.

**Scopri**: In questa sezione,  **** il widget Newsletter visualizza le risorse e le rappresentazioni recentemente caricate nella  [!DNL Assets] distribuzione.

Per abilitare la rimozione dei dati dell&#39;attività dell&#39;utente, abilita il **[!UICONTROL servizio di rimozione degli eventi DAM]** da Configuration Manager. Dopo aver attivato questo servizio, le attività dell&#39;utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata introduttiva fornisce strumenti di navigazione semplici, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>Se si abilitano i servizi [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL DAM Event Purge], le operazioni di scrittura su JCR e l&#39;indicizzazione delle ricerche aumentano notevolmente il carico sul server [!DNL Experience Manager]. Il carico aggiuntivo sul server [!DNL Experience Manager] può influire sulle prestazioni.

>[!CAUTION]
>
>L&#39;acquisizione, il filtro e l&#39;eliminazione delle attività utente necessarie per la pagina principale [!DNL Assets] comportano un sovraccarico delle prestazioni. Pertanto, gli amministratori devono configurare la pagina principale in modo efficace per gli utenti target.
>
> Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione Pagina iniziale risorsa per impedire l’aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Day CQ DAM Event Recorder] da [!UICONTROL Configuration Manager].
>
>Se utilizzate la funzione,  Adobe consiglia di pianificare la frequenza di eliminazione in base al carico del server.
