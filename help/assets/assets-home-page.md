---
title: Esperienza della home page di AEM Assets
description: Personalizza la home page di Risorse AEM per un’esperienza sulla schermata di benvenuto completa, con un’istantanea delle attività recenti relative alle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Esperienza della home page di AEM Assets {#aem-assets-home-page-experience}

Personalizza la home page di Risorse Adobe Experience Manager (AEM) per un’esperienza di benvenuto completa, con un’istantanea delle attività recenti relative alle risorse.

La home page di Risorse AEM offre una schermata di benvenuto ricca e personalizzata, che include un&#39;istantanea delle attività recenti, come le risorse che sono state visualizzate o caricate di recente.

La home page delle risorse è disabilitata per impostazione predefinita. Per attivarla, effettuare le seguenti operazioni:

1. Aprite AEM Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite il servizio **[!UICONTROL Day CQ DAM Event Recorder]** .
1. Selezionate **[!UICONTROL Abilita questo servizio]** per abilitare la registrazione dell&#39;attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dall’elenco Tipi **** evento, selezionate gli eventi da registrare e salvate le modifiche.

   >[!CAUTION]
   >
   >Abilitando le opzioni di visualizzazione delle risorse, dei progetti visualizzati e delle raccolte, il numero di eventi registrati aumenta notevolmente.

1. Aprite il servizio Flag **[!UICONTROL di funzionalità della home page della risorsa]** DAM da Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selezionate l’ `isEnabled.name` opzione per attivare la funzione Pagina iniziale risorse. Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Aprite la finestra di dialogo Preferenze **** utente e selezionate **[!UICONTROL Abilita pagina]** iniziale risorse. Salva le modifiche.

   ![Abilita pagina principale risorse nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver attivato la home page delle risorse, passa all’interfaccia utente delle risorse dalla pagina di navigazione o accedi direttamente dall’URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configura collegamento esperienza nell’interfaccia utente di Risorse](assets/config-experience-link.png)

Toccate o fate clic su **[!UICONTROL Fate clic qui per configurare il collegamento]** dell&#39;esperienza per aggiungere il vostro nome utente, l&#39;immagine di sfondo e l&#39;immagine del profilo.

La home page delle risorse include le seguenti sezioni:

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

**Attività**: In questa sezione, il widget **[!UICONTROL Attività]** personale visualizza le attività recenti svolte dall’utente che ha eseguito l’accesso con risorse (incluse le risorse senza rappresentazioni), ad esempio caricamenti di risorse, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni.

**Recente**: Il widget **[!UICONTROL Visualizzato]** di recente in questa sezione visualizza le entità a cui l&#39;utente ha effettuato l&#39;accesso di recente, comprese cartelle, raccolte e progetti.

**Scopri**: Il **[!UICONTROL nuovo]** widget in questa sezione presenta le risorse e le rappresentazioni caricate di recente nell’istanza di AEM Assets.

Per abilitare la rimozione dei dati dell&#39;attività utente, abilita il servizio **[!UICONTROL di rimozione eventi]** DAM da Configuration Manager. Dopo aver attivato questo servizio, le attività dell&#39;utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata introduttiva fornisce strumenti di navigazione semplici, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>Se si abilitano i servizi [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL DAM Event Purge] , le operazioni di scrittura su JCR e l&#39;indicizzazione delle ricerche aumentano notevolmente il carico sul server AEM. Il carico aggiuntivo sul server AEM può influire sulle prestazioni.

>[!CAUTION]
>
>L’acquisizione, il filtro e l’eliminazione delle attività utente richieste per la home page delle risorse comportano un sovraccarico delle prestazioni. Pertanto, gli amministratori devono configurare la pagina principale in modo efficace per gli utenti target.
>
>Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione Pagina iniziale risorsa per impedire l’aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Day CQ DAM Event Recorder] da [!UICONTROL Configuration Manager].
>
>Se utilizzate questa funzione, Adobe consiglia di pianificare la frequenza di eliminazione in base al carico del server.
