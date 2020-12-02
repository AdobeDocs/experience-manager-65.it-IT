---
title: Configurazione delle estensioni Acrobat Reader DC per l'acquisizione dei dati
seo-title: Configurazione delle estensioni Acrobat Reader DC per l'acquisizione dei dati
description: Scoprite come configurare le estensioni Acrobat Reader DC per l'acquisizione dei dati.
seo-description: Scoprite come configurare le estensioni Acrobat Reader DC per l'acquisizione dei dati.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Configurazione delle estensioni Acrobat Reader DC per l&#39;acquisizione dei dati {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Se gli utenti dell&#39;installazione dei moduli AEM utilizzano la funzionalità di acquisizione dei dati di Content Services (obsoleto), è consigliabile creare un ruolo con accesso in sola lettura per tali utenti.

***nota **:  Adobe® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle LiveCycle®. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulle persone. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Vedere [ documento sul ciclo di vita del prodotto del Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Per informazioni sulla configurazione di Content Services (obsoleto), vedere [Amministrazione di Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).*

Per acquisire i dati è necessario assegnare un ruolo utente per accedere a SampleReaderExtensionsCredential. È possibile assegnare il ruolo Amministratore trust standard, ma si consideri che questo ruolo offre agli utenti generali non amministrativi i potenti privilegi di amministratore che controllano le impostazioni PKI Trust e gestiscono le credenziali PKI, compromettendo la sicurezza dell&#39;installazione dei moduli AEM in un ambiente di produzione. È consigliabile che l&#39;amministratore di sistema dei moduli AEM crei un ruolo che conceda l&#39;accesso in sola lettura all&#39;archivio attendibili e assegni questo nuovo ruolo agli utenti non amministratori che utilizzano l&#39;acquisizione dei dati.

## Creazione di un ruolo per gli utenti di acquisizione dati {#create-a-role-for-data-capture-users}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Nuovo ruolo.
1. Immettete il nome del ruolo (ad esempio, Utente acquisizione dati) e la descrizione nei campi appropriati, quindi fate clic su Avanti.
1. Nella schermata Autorizzazioni ruolo, fate clic su Trova autorizzazioni, quindi selezionate Lettura credenziali dall’elenco delle autorizzazioni disponibili.
1. Fare clic su OK, quindi su Fine.

## Assegnazione del ruolo di acquisizione dei dati {#assign-the-data-capture-role}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fate clic su Trova.
1. Fare clic sul ruolo utente di acquisizione dei dati creato.
1. Nella scheda Utenti/gruppi ruolo, fate clic su Trova utenti/gruppi.
1. Nella schermata Trova utenti e gruppi, fate clic su Trova, selezionate gli utenti che richiedono il ruolo utente di acquisizione dei dati, quindi fate clic su OK.
1. Nella schermata Modifica ruolo, fate clic su Salva.

