---
title: Installa feature pack 18912 per la migrazione di massa delle risorse
description: Il Feature Pack 18912 consente di caricare in massa le risorse tramite FTP o di migrare le risorse da Dynamic Media Classic a Dynamic Media su Adobe Experience Manager. Questo pacchetto di funzioni opzionale è disponibile dal supporto Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Gestione risorse
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Installa feature pack 18912 per la migrazione di massa delle risorse{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del feature pack 18912 è *opzionale*.

Il Feature Pack 18912 consente di caricare in massa le risorse direttamente in Dynamic Media - Modalità Scene7 su Adobe Experience Manager tramite FTP. Consente inoltre di migrare le risorse da Dynamic Media Classic alla modalità Dynamic Media - Scene7 all’Experience Manager. Il pacchetto di funzioni è disponibile da [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>È possibile utilizzare il pacchetto di funzioni per eseguire la migrazione in massa delle risorse da solo da Dynamic Media Classic a Dynamic Media - Scene7 in modalità ad Experience Manager. Puoi anche eseguire la migrazione in massa delle risorse utilizzando la funzione FTP in Dynamic Media Classic. Tuttavia, Adobe consiglia *not* di utilizzare uno di questi metodi a causa della complessità in questione.
>
>Di conseguenza, questo pacchetto di funzioni di migrazione è *supportato solo* come parte di un progetto di migrazione quando viene eseguito tramite [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Prima di installare il feature pack, crea un utente del servizio e fornisci tali informazioni al supporto di Adobe.

Vedere anche [Configurazione Dynamic Media - Modalità Scene7](/help/assets/config-dms7.md).

**Per installare il feature pack 18912 per la migrazione di massa delle risorse:**

1. Nell&#39;istanza di Experience Manager, passa a **[!UICONTROL Tool]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]** e seleziona **[!UICONTROL Crea utente]**. L&#39;utente del servizio deve disporre delle autorizzazioni di *lettura/scrittura* per `/content/dam.`
1. Nei campi **[!UICONTROL ID]** e **[!UICONTROL Password]** , immetti un nome utente e una password; ad esempio, **FTP User**. Questo nome viene visualizzato nella timeline come utente che ha creato la risorsa. Quando una risorsa viene caricata da FTP, viene considerata una creazione quando viene caricata sul server FTP e inviata ad Experience Manager.
1. Contatta [Adobe Enterprise Customer Care per Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) per richiedere l&#39;accesso al feature pack 18912 per il download. Quando si contatta l&#39;assistenza, potrebbe essere necessario disporre delle seguenti informazioni:

   * Indirizzo IP del server per l’istanza Author, incluso il numero di porta (per impostazione predefinita, il numero di porta è 4502.)
   * Nome utente e password del servizio di Experience Manager dal passaggio precedente.

1. Ad Experience Manager, Adobe Enterprise Customer Care fornisce le credenziali FTP e l’accesso al feature pack 18912.
1. Quando ricevi il feature pack 18912, installalo.

   Per ulteriori informazioni sull&#39;utilizzo di Distribuzione software e pacchetti in Experience Manager, consulta [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md) .
