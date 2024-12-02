---
title: '[!DNL Assets] esperienza pagina iniziale'
description: Personalizza la  [!DNL Experience Manager Assets] home page per un'esperienza avanzata con la schermata di benvenuto, inclusa un'istantanea delle attività recenti relative alle risorse.
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

# Esperienza della home page [!DNL Adobe Experience Manager Assets] {#aem-assets-home-page-experience}

Personalizza la home page di [!DNL Adobe Experience Manager Assets] per un&#39;esperienza avanzata con la schermata di benvenuto, inclusa un&#39;istantanea delle attività recenti relative alle risorse.

La pagina Home di [!DNL Assets] offre un&#39;esperienza della schermata di benvenuto ricca e personalizzata, che include un&#39;istantanea delle attività recenti, ad esempio le risorse visualizzate o caricate di recente.

La home page di [!DNL Assets] è disabilitata per impostazione predefinita. Per attivarla, effettuare le seguenti operazioni:

1. Aprire [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri il servizio **[!UICONTROL Day CQ DAM Event Recorder]**.
1. Selezionare **[!UICONTROL Abilita il servizio]** per abilitare la registrazione delle attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dall&#39;elenco **[!UICONTROL Tipi di evento]**, selezionare gli eventi da registrare e salvare le modifiche.

   >[!CAUTION]
   >
   >L’abilitazione delle opzioni Risorsa visualizzata, Progetti visualizzati e Raccolte visualizzate aumenta in modo significativo il numero di eventi registrati.

1. Apri il servizio **[!UICONTROL Flag per funzione Pagina iniziale risorse DAM]** da Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Selezionare l&#39;opzione `isEnabled.name` per abilitare la funzionalità della home page di [!DNL Assets]. Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Apri la finestra di dialogo **[!UICONTROL Preferenze utente]** e seleziona **[!UICONTROL Abilita home page di Assets]**. Salva le modifiche.

   ![Abilitare la home page delle risorse nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver abilitato la home page di [!DNL Assets], passare all&#39;interfaccia utente di [!DNL Assets] dalla pagina Navigazione oppure accedervi direttamente dall&#39;URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurare experience link nell&#39;interfaccia utente di Assets](assets/config-experience-link.png)

Fai clic su **[!UICONTROL Fai clic qui per configurare il collegamento esperienza]** per aggiungere il nome utente, l&#39;immagine di sfondo e l&#39;immagine del profilo.

La home page di [!DNL Assets] include le sezioni seguenti:

* Sezione di benvenuto
* Sezione widget

**Sezione introduttiva**

Se il profilo esiste, nella sezione Benvenuti viene visualizzato un messaggio di benvenuto indirizzato all&#39;utente. Inoltre, mostra l’immagine del profilo e un’immagine di benvenuto (se configurata già).

Se il profilo è incompleto, nella sezione Benvenuti vengono visualizzati un messaggio di benvenuto generico e un segnaposto per l&#39;immagine del profilo.

**Sezione widget**

Questa sezione viene visualizzata sotto la sezione Benvenuti e mostra i widget predefiniti nelle sezioni seguenti:

* Attività
* Recente
* Scopri

**Attività**: in questa sezione, il widget **[!UICONTROL Attività personale]** mostra le attività recenti eseguite dall&#39;utente connesso con risorse (incluse le risorse senza rappresentazioni), ad esempio caricamenti, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni.

**Recenti**: il widget **[!UICONTROL Visualizzato di recente]** in questa sezione visualizza le entità a cui l&#39;utente connesso ha effettuato l&#39;accesso di recente, incluse cartelle, raccolte e progetti.

**Individua**: il widget **[!UICONTROL Nuovo]** in questa sezione visualizza le risorse e le rappresentazioni caricate di recente nella distribuzione [!DNL Assets].

Per abilitare la rimozione dei dati delle attività utente, abilitare il servizio **[!UICONTROL Rimozione eventi DAM]** da Configuration Manager. Dopo aver attivato questo servizio, le attività dell&#39;utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata iniziale fornisce semplici strumenti di navigazione, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>L&#39;abilitazione dei servizi [!UICONTROL Day CQ DAM Event Recorder] e [!UICONTROL DAM Event Purge] aumenta le operazioni di scrittura in JCR e l&#39;indicizzazione della ricerca, aumentando notevolmente il carico sul server [!DNL Experience Manager]. Il carico aggiuntivo sul server [!DNL Experience Manager] può influire sulle prestazioni.

>[!CAUTION]
>
>L&#39;acquisizione, il filtraggio e l&#39;eliminazione delle attività utente necessarie per la home page di [!DNL Assets] determinano un sovraccarico delle prestazioni. Pertanto, gli amministratori devono configurare la pagina Home in modo efficace per gli utenti target.
>
>Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione Pagina iniziale risorse per evitare un aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Day CQ DAM Event Recorder] da [!UICONTROL Configuration Manager].
>
>Se utilizzi la funzione, Adobe consiglia di pianificare la frequenza di eliminazione in base al caricamento del server.
