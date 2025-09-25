---
title: Configurazione delle estensioni di Acrobat Reader DC per l’acquisizione dei dati
description: Scopri come configurare le estensioni di Acrobat Reader DC per l’acquisizione dei dati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '327'
ht-degree: 100%

---

# Configurazione delle estensioni di Acrobat Reader DC per l’acquisizione dei dati {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Se gli utenti dell’installazione di AEM Forms utilizzano la funzionalità di acquisizione dati di Content Services (obsoleto), è consigliabile creare un ruolo con accesso in sola lettura per tali utenti.

***Nota **: Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Consulta il [documento sul ciclo di vita del prodotto Adobe](https://helpx.adobe.com/it/support/programs/eol-matrix.html).*

Per l’acquisizione dei dati è necessario assegnare un ruolo utente per accedere a SampleReaderExtensionsCredential. Puoi assegnare il ruolo standard di Amministratore attendibile. Tuttavia, tieni presente che questo ruolo conferisce agli utenti generali e non amministratori, privilegi di amministratore che controllano le impostazioni di attendibilità PKI e gestiscono le credenziali PKI, il che potrebbe compromettere la sicurezza dell’installazione di AEM Forms in un ambiente di produzione. È consigliabile che l’amministratore di sistema di AEM Forms crei un ruolo che consenta solo l’accesso in sola lettura all’archivio fonti attendibili e assegni questo nuovo ruolo agli utenti non amministratori che utilizzano l’acquisizione dei dati.

## Creare un ruolo per gli utenti di acquisizione dati {#create-a-role-for-data-capture-users}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione ruolo, quindi fai clic su Nuovo ruolo.
1. Immetti il nome del ruolo (ad esempio, Utente di acquisizione dati) e la descrizione nei campi appropriati, quindi fai clic su Avanti.
1. Nella schermata Autorizzazioni ruolo, fai clic su Trova autorizzazioni, quindi seleziona Lettura credenziali dall’elenco delle autorizzazioni disponibili.
1. Fai clic su OK, quindi su Termina.

## Assegnare il ruolo di acquisizione dati {#assign-the-data-capture-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione ruolo, quindi fai clic su Trova.
1. Fai clic sul ruolo utente di acquisizione dati creato.
1. Nella scheda Utenti/gruppi ruolo fai clic su Trova utenti/gruppi.
1. Nella schermata Trova utenti e gruppi, fai clic su Trova, seleziona gli utenti che richiedono il ruolo utente di acquisizione dati, quindi fai clic su OK.
1. Nella schermata Modifica ruolo, fai clic su Salva.
