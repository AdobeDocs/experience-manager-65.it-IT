---
title: Esperienza della pagina Home di [!DNL Assets]
description: Personalizza la pagina Home di  [!DNL Experience Manager Assets]  per un’esperienza avanzata con la schermata introduttiva, inclusa un’istantanea delle attività recenti relative alle risorse.
contentOwner: AG
feature: Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '562'
ht-degree: 100%

---

# Esperienza della pagina Home di [!DNL Adobe Experience Manager Assets] {#aem-assets-home-page-experience}

Personalizza la pagina Home di [!DNL Adobe Experience Manager Assets] per un’esperienza avanzata con la schermata introduttiva, inclusa un’istantanea delle attività recenti relative alle risorse.

La pagina Home di [!DNL Assets] offre un’esperienza avanzata e personalizzata della schermata introduttiva, che include un’istantanea delle attività recenti, ad esempio le risorse visualizzate o caricate di recente.

La pagina Home di [!DNL Assets] è disabilitata per impostazione predefinita. Per abilitarla, effettua le seguenti operazioni:

1. Apri Gestione configurazione di [!DNL Experience Manager] `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri il servizio **[!UICONTROL Registratore eventi DAM CQ day]**.
1. Seleziona **[!UICONTROL Abilita questo servizio]** per abilitare la registrazione delle attività.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dall’elenco **[!UICONTROL Tipi di evento]**, seleziona gli eventi da registrare e salva le modifiche.

   >[!CAUTION]
   >
   >L’abilitazione delle opzioni Risorsa visualizzata, Progetti visualizzati e Raccolte visualizzate aumenta in modo significativo il numero di eventi registrati.

1. Apri il servizio **[!UICONTROL Flag di funzione pagina Home risorse DAM]** da Gestione configurazione `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleziona l’opzione `isEnabled.name` per abilitare la funzione della pagina Home di [!DNL Assets]. Salva le modifiche.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Apri la finestra di dialogo **[!UICONTROL Preferenze utente]** e seleziona **[!UICONTROL Abilita pagina Home di Assets]**. Salva le modifiche.

   ![Abilitare la pagina Home di Assets nella finestra di dialogo Preferenze utente](assets/Annotation-color.png)

Dopo aver abilitato la pagina Home di [!DNL Assets], passa all’interfaccia utente di [!DNL Assets] dalla pagina Navigazione oppure accedi direttamente dall’URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurare il collegamento alle esperienze nell’interfaccia utente di Assets](assets/config-experience-link.png)

Fai clic su **[!UICONTROL Fai clic qui per configurare il collegamento alle esperienze]** per aggiungere il nome utente, l’immagine di sfondo e l’immagine del profilo.

La pagina Home di [!DNL Assets] include le sezioni seguenti:

* Sezione introduttiva
* Sezione dei widget

**Sezione introduttiva**

Se il tuo profilo esiste, nella sezione introduttiva viene visualizzato un messaggio di benvenuto indirizzato a te. Inoltre, viene mostrata l’immagine del profilo e un’immagine di benvenuto (se già configurata).

Se il tuo profilo è incompleto, nella sezione introduttiva vengono visualizzati un messaggio di benvenuto generico e un segnaposto per l’immagine del tuo profilo.

**Sezione dei widget**

Questa sezione viene visualizzata sotto la sezione introduttiva e mostra i widget disponibili nelle sezioni seguenti:

* Attività
* Recente
* Scopri

**Attività**: in questa sezione, il widget **[!UICONTROL La mia attività]** mostra le attività recenti eseguite dall’utente connesso con le risorse (incluse le risorse senza rappresentazioni), ad esempio caricamenti di risorse, download, creazione di risorse, modifiche, commenti, annotazioni e condivisioni.

**Recenti**: il widget **[!UICONTROL Visualizzato di recente]** in questa sezione visualizza le entità a cui l’utente connesso ha effettuato l’accesso di recente, inclusi cartelle, raccolte e progetti.

**Scopri**: il widget **[!UICONTROL Nuovo]** in questa sezione visualizza le risorse e le rappresentazioni caricate di recente nell’implementazione [!DNL Assets].

Per abilitare la rimozione dei dati delle attività utente, abilita il **[!UICONTROL servizio di eliminazione eventi DAM]** da Gestione configurazione. Dopo aver abilitato questo servizio, le attività dell’utente connesso che superano un numero specificato vengono eliminate dal sistema.

La schermata introduttiva fornisce supporti alla navigazione semplici, ad esempio icone sulla barra degli strumenti per accedere a cartelle, raccolte e cataloghi.

>[!NOTE]
>
>L’abilitazione dei servizi [!UICONTROL Registratore eventi DAM CQ Day] ed [!UICONTROL Eliminazione eventi DAM] aumenta le operazioni di scrittura nel JCR e l’indicizzazione delle ricerche, aumentando notevolmente il carico sul server [!DNL Experience Manager]. Il carico aggiuntivo sul server [!DNL Experience Manager] può influire sulle prestazioni.

>[!CAUTION]
>
>L’acquisizione, il filtraggio e l’eliminazione delle attività utente necessari per la pagina Home di [!DNL Assets] determinano un sovraccarico delle prestazioni. Pertanto, gli amministratori devono configurare la pagina Home in modo efficace per gli utenti di destinazione.
>
>Adobe consiglia agli amministratori e agli utenti che eseguono operazioni in blocco di evitare di utilizzare la funzione pagina Home di Risorse per evitare un aumento delle attività degli utenti. Inoltre, gli amministratori possono escludere le attività di registrazione per utenti specifici configurando [!UICONTROL Registratore eventi DAM CQ day] da [!UICONTROL Gestione configurazione].
>
>Se utilizzi questa funzione, Adobe consiglia di pianificare la frequenza di eliminazione in base al carico del server.
