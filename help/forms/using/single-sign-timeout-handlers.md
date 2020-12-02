---
title: Gestori Single Sign On e timeout
seo-title: Gestori Single Sign On e timeout
description: Procedura per impostare il valore di timeout sessione per 'area di lavoro AEM Forms.
seo-description: Procedura per impostare il valore di timeout sessione per 'area di lavoro AEM Forms.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Gestori Single Sign On e timeout {#single-sign-on-and-timeout-handlers}

&#39;area di lavoro AEM Forms è abilitata l&#39;autenticazione a SSO. Se un utente ha eseguito l&#39;accesso a un&#39;applicazione AEM Forms  come l&#39;interfaccia utente di Forms Manager o PDF Generator e accede &#39;area di lavoro AEM Forms nella stessa sessione del browser, l&#39;utente ha eseguito l&#39;accesso &#39;area di lavoro di AEM Forms e viceversa.

## Gestione del timeout del server nell&#39;area di lavoro  AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Il timeout sessione per un utente può essere configurato nella console di amministrazione.

Per impostare il timeout, accedere a `https://'[server]:[port]'/adminui`, andare a **Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati** e configurare le impostazioni desiderate.

In  il timeout dell&#39;area di lavoro AEM Forms viene gestito come:

* La durata della sessione per un utente è disponibile in risposta alla chiamata `initialize` che inizializza la sessione utente.
* Una finestra di dialogo a comparsa notifica all’utente che la sessione sta per scadere, 15 secondi prima della scadenza della sessione.

In questa finestra di dialogo a comparsa:

* Fate clic su OK per terminare la sessione utente.
* Fate clic su Annulla per inizializzare nuovamente la sessione utente.

>[!NOTE]
>
>Se non viene eseguita alcuna azione, l&#39;utente viene automaticamente disconnesso &#39;area di lavoro di AEM Forms tre secondi prima della scadenza della sessione.
