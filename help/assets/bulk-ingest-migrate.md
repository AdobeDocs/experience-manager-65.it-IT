---
title: Installazione del feature pack 18912 per la migrazione di massa delle risorse
description: Il Feature Pack 18912 consente di caricare le risorse in blocco tramite FTP o di migrare le risorse da Dynamic Media Classic a Dynamic Media su AEM. Questo pacchetto di funzioni opzionale è disponibile dal supporto Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Installazione del feature pack 18912 per la migrazione di massa delle risorse{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del feature pack 18912 è *opzionale*.

Il Feature Pack 18912 consente di trasferire risorse in massa direttamente in contenuti multimediali dinamici - modalità Scene7 su AEM tramite FTP, oppure di trasferire risorse da Dynamic Media Classic a Dynamic Media - modalità Scene7 su AEM. Il pacchetto di funzioni è disponibile presso [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Sebbene sia possibile utilizzare il pacchetto di funzioni per migrare in massa le risorse in modo autonomo da Dynamic Media Classic a Dynamic Media - Scene7 in AEM o per migrare in massa le risorse tramite la funzione FTP in Dynamic Media Classic, Adobe *non* consiglia questo metodo a causa della complessità in questione.
>
>I pacchetti di funzionalità di migrazione, come questo, sono supportati *solo* come parte di un progetto di migrazione se eseguiti tramite [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Prima di installare il pacchetto di funzioni, è necessario creare un utente del servizio e fornire tali informazioni al supporto Adobe.

Consultate anche [Configurazione di contenuti multimediali dinamici - modalità](/help/assets/config-dms7.md)Scene7.

**Per installare feature pack 18912 per la migrazione di massa delle risorse**

1. Nell’istanza di AEM, andate a **[!UICONTROL Strumenti > Protezione > Utenti]** e selezionate **[!UICONTROL Crea utente]**. L&#39;utente del servizio deve disporre delle autorizzazioni di *lettura/scrittura* per `/content/dam.`
1. Nei campi **[!UICONTROL ID]** e **[!UICONTROL Password]** , immettete un nome utente e una password; ad esempio, Utente **** FTP. Questo nome viene visualizzato nella timeline come utente che ha creato la risorsa. Quando una risorsa viene caricata dall’FTP, viene considerata creata quando viene caricata sul server FTP e inviata ad AEM.
1. Contatta il supporto [Adobe Enterprise per Experience Manager](https://helpx.adobe.com/contact/enterprise-support.ec.html) per richiedere l’accesso al feature pack 18912 da scaricare. Quando contattate il supporto, potreste aver bisogno delle seguenti informazioni:

   * Indirizzo IP del server per l’istanza Author, incluso il numero di porta (per impostazione predefinita, il numero di porta è 4502.)
   * Nome utente e password del servizio AEM dal passaggio precedente.

1. Il supporto Adobe Enterprise per AEM fornisce le credenziali FTP e l&#39;accesso al feature pack 18912.
1. Dopo aver ricevuto il pacchetto 18912, installatelo.

   Consultate [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md) per ulteriori informazioni sull&#39;utilizzo di Package Share e dei pacchetti in AEM.

