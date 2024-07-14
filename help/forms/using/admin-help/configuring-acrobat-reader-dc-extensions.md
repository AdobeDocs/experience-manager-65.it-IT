---
title: Configurazione delle estensioni Acrobat Reader DC per l’acquisizione dei dati
description: Scopri come configurare le estensioni Acrobat Reader DC per l’acquisizione dei dati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Configurazione delle estensioni Acrobat Reader DC per l’acquisizione dei dati {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Se gli utenti dell’installazione dei moduli AEM utilizzano la funzionalità di acquisizione dati di Content Services (obsoleto), è consigliabile creare un ruolo con accesso in sola lettura per tali utenti.

***Nota **: Adobe ® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con il LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 12/31/2014. Consulta [Adobe documento sul ciclo di vita del prodotto](https://helpx.adobe.com/it/support/programs/eol-matrix.html).*

Per l&#39;acquisizione dei dati è necessario assegnare un ruolo utente per accedere a SampleReaderExtensionsCredential. È possibile assegnare il ruolo standard Amministratore trust. Tuttavia, si consideri che questo ruolo conferisce agli utenti generali e non amministratori privilegi di amministratore che controllano le impostazioni di attendibilità PKI e gestiscono le credenziali PKI, il che potrebbe compromettere la sicurezza dell&#39;installazione dei moduli AEM in un ambiente di produzione. Si consiglia all&#39;amministratore di sistema dei moduli AEM di creare un ruolo che consenta solo l&#39;accesso in sola lettura all&#39;archivio fonti attendibili e assegnare questo nuovo ruolo agli utenti non amministratori che utilizzano l&#39;acquisizione dei dati.

## Creare un ruolo per gli utenti di acquisizione dati {#create-a-role-for-data-capture-users}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nuovo ruolo.
1. Immettere il nome del ruolo (ad esempio, Utente di acquisizione dati) e la descrizione nei campi appropriati, quindi fare clic su Avanti.
1. Nella schermata Autorizzazioni ruolo, fai clic su Trova autorizzazioni, quindi seleziona Lettura credenziali dall’elenco delle autorizzazioni disponibili.
1. Fare clic su OK, quindi su Fine.

## Assegnare il ruolo di acquisizione dati {#assign-the-data-capture-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Trova.
1. Fai clic sul ruolo utente di acquisizione dati creato.
1. Nella scheda Utenti/gruppi ruolo fare clic su Trova utenti/gruppi.
1. Nella schermata Trova utenti e gruppi fare clic su Trova, selezionare gli utenti che richiedono il ruolo utente di acquisizione dati, quindi fare clic su OK.
1. Nella schermata Modifica ruolo, fai clic su Salva.
