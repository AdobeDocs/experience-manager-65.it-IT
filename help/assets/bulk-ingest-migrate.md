---
title: Installare il 18912 del feature pack per la migrazione in blocco delle risorse
description: Il Feature Pack 18912 consente di acquisire in blocco le risorse tramite FTP o di migrare le risorse da Dynamic Media Classic a Dynamic Medie su Adobe Experience Manager. Questo feature pack opzionale è disponibile dal supporto Adobe.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Installare il 18912 del feature pack per la migrazione in blocco delle risorse{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del 18912 del feature pack è *facoltativa*.

Il Feature Pack 18912 consente di acquisire in blocco le risorse direttamente in modalità Dynamic Medie - Scene7 su Adobe Experience Manager tramite FTP. Consente inoltre di migrare le risorse da Dynamic Media Classic alla modalità Dynamic Medie - Scene7 su Experience Manager. Il feature pack è disponibile da [Adobe Professional Services](https://business.adobe.com/it/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>È possibile utilizzare il feature pack per eseguire da solo la migrazione in massa delle risorse da Dynamic Media Classic alla modalità Dynamic Medie - Scene7 in Experience Manager. È inoltre possibile eseguire la migrazione in massa delle risorse utilizzando la funzione FTP in Dynamic Media Classic. Tuttavia, Adobe *not* consiglia di utilizzare uno di questi metodi a causa della complessità.
>
>Di conseguenza, questo feature pack per la migrazione è supportato *solo* come parte di un progetto di migrazione se eseguito tramite [Adobe Professional Services](https://business.adobe.com/it/customers/consulting-services/main.html).

Prima di installare il feature pack, è necessario creare un utente del servizio e fornire tali informazioni al supporto Adobe.

Vedere anche [Configurare Dynamic Medie - Modalità Scene7](/help/assets/config-dms7.md).

**Per installare 18912 di feature pack per la migrazione di risorse in blocco:**

1. Nell&#39;istanza di Experience Manager, passa a **[!UICONTROL Strumento]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]** e seleziona **[!UICONTROL Crea utente]**. L&#39;utente del servizio deve disporre di *autorizzazioni di lettura/scrittura* per `/content/dam.`
1. Nei campi **[!UICONTROL ID]** e **[!UICONTROL Password]** immettere un nome utente e una password, ad esempio **Utente FTP**. Questo nome viene visualizzato nella timeline come l’utente che ha creato la risorsa. Quando una risorsa viene caricata da FTP, viene considerata creata quando viene caricata sul server FTP e inviata all&#39;Experience Manager.
1. Contatta l&#39;[Assistenza clienti Adobe per Experience Manager](https://experienceleague.adobe.com/i?support-solution=General#support) per richiedere l&#39;accesso al 18912 del feature pack per il download. Quando si contatta l’assistenza potrebbe essere necessario disporre delle seguenti informazioni:

   * Indirizzo IP del server per l’istanza di authoring, incluso il numero di porta (per impostazione predefinita, il numero di porta è 4502).
   * Experience Manager di nome utente e password del servizio del passaggio precedente.

1. Adobe L’Assistenza clienti per Experience Manager fornisce le credenziali FTP e l’accesso al feature pack 18912.
1. Quando si riceve il feature pack 18912, installarlo.

   Per ulteriori informazioni sull&#39;utilizzo di Distribuzione software e pacchetti in Experience Manager, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md).
