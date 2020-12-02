---
title: Installazione del feature pack 18912 per la migrazione di massa delle risorse
description: Il Feature Pack 18912 consente di caricare le risorse in blocco tramite FTP, oppure di migrare le risorse da Dynamic Media Classic a Dynamic Media su AEM. Questo pacchetto di funzioni opzionale è disponibile  supporto del Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Installazione del feature pack 18912 per la migrazione di massa delle risorse{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del feature pack 18912 è *opzionale*.

Il Feature Pack 18912 consente di trasferire le risorse direttamente in contenuti multimediali dinamici - in modalità Scene7 su AEM tramite FTP, oppure di migrare le risorse da Dynamic Media Classic a Dynamic Media - in modalità Scene7 su AEM. Il pacchetto di funzioni è disponibile da [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Anche se è possibile utilizzare il pacchetto di funzioni per migrare in massa le risorse in modo autonomo da Dynamic Media Classic a Dynamic Media - Scene 7 in modalità AEM o per migrare in massa le risorse tramite la funzione FTP in Dynamic Media Classic,  Adobe *not* consiglia questo metodo a causa della complessità in questione.
>
>Di conseguenza, i pacchetti di funzionalità di migrazione, come questo, sono supportati *solo* come parte di un progetto di migrazione se eseguiti tramite [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Prima di installare il pacchetto di funzioni, è necessario creare un utente del servizio e fornire tali informazioni al supporto  Adobe.

Vedere anche [Configurazione di contenuti multimediali dinamici - modalità Scene7](/help/assets/config-dms7.md).

**Per installare feature pack 18912 per la migrazione di massa delle risorse**

1. Nell&#39;istanza AEM, passare a **[!UICONTROL Strumenti > Protezione > Utenti]** e selezionare **[!UICONTROL Crea utente]**. L&#39;utente del servizio deve avere *autorizzazioni di lettura/scrittura* su `/content/dam.`
1. Nei campi **[!UICONTROL ID]** e **[!UICONTROL Password]**, immettere un nome utente e una password; ad esempio, **Utente FTP**. Questo nome viene visualizzato nella timeline come utente che ha creato la risorsa. Quando una risorsa viene caricata dall’FTP, viene considerata creata quando viene caricata sul server FTP e viene spinta in AEM.
1. Contatta l&#39;Assistenza clienti [ Adobe Enterprise per  Experience Manager](https://helpx.adobe.com/it/contact/enterprise-support.ec.html) per richiedere l&#39;accesso al feature pack 18912 da scaricare. Quando contattate il supporto, potreste aver bisogno delle seguenti informazioni:

   * Indirizzo IP del server per l’istanza Author, incluso il numero di porta (per impostazione predefinita, il numero di porta è 4502.)
   * AEM nome utente e password utente del servizio dal passaggio precedente.

1.  Adobe Assistenza clienti Enterprise per AEM fornisce le credenziali FTP e l&#39;accesso al feature pack 18912.
1. Dopo aver ricevuto il pacchetto 18912, installatelo.

   Per ulteriori informazioni sull&#39;utilizzo di distribuzione software e pacchetti in AEM, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md).
