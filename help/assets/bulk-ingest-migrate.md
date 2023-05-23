---
title: Installare il 18912 del feature pack per la migrazione in blocco delle risorse
description: Il Feature Pack 18912 consente di acquisire in blocco le risorse tramite FTP o di migrare le risorse da Dynamic Media Classic a Dynamic Media su Adobe Experience Manager. Questo feature pack opzionale è disponibile dal supporto Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 1%

---

# Installare il 18912 del feature pack per la migrazione in blocco delle risorse{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del feature pack 18912 è *facoltativo*.

Il Feature Pack 18912 consente di acquisire in blocco le risorse direttamente in modalità Dynamic Media - Scene7 su Adobe Experience Manager tramite FTP. Consente inoltre di migrare le risorse da Dynamic Media Classic alla modalità Dynamic Media - Scene7 su Experience Manager. Il feature pack è disponibile da [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>È possibile utilizzare il feature pack per eseguire da solo la migrazione in massa delle risorse da Dynamic Media Classic alla modalità Dynamic Media - Scene7 in Experience Manager. È inoltre possibile eseguire la migrazione in massa delle risorse utilizzando la funzione FTP in Dynamic Media Classic. Tuttavia, l’Adobe *non* consiglia di utilizzare uno di questi metodi a causa della complessità richiesta.
>
>Il feature pack per la migrazione è *solo* supportato come parte di un progetto di migrazione quando eseguito tramite [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Prima di installare il feature pack, è necessario creare un utente del servizio e fornire tali informazioni al supporto Adobe.

Vedi anche [Configurare Dynamic Media - Modalità Scene7](/help/assets/config-dms7.md).

**Per installare il 18912 del feature pack per la migrazione in blocco delle risorse:**

1. Nell’istanza di Experience Manager, passa a **[!UICONTROL Strumento]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]** e seleziona **[!UICONTROL Crea utente]**. Questo utente del servizio deve avere *lettura/scrittura* autorizzazioni a `/content/dam.`
1. In **[!UICONTROL ID]** e **[!UICONTROL Password]** , immettere un nome utente e una password, ad esempio **Utente FTP**. Questo nome viene visualizzato nella timeline come l’utente che ha creato la risorsa. Quando una risorsa viene caricata da FTP, viene considerata creata quando viene caricata sul server FTP e inviata all&#39;Experience Manager.
1. Contatto [Adobe di assistenza clienti per Experience Manager](https://experienceleague.adobe.com/?support-solution=General&amp;lang=it#support) per richiedere l’accesso alle 18912 del feature pack per il download. Quando si contatta l’assistenza potrebbe essere necessario disporre delle seguenti informazioni:

   * Indirizzo IP del server per l’istanza di authoring, incluso il numero di porta (per impostazione predefinita, il numero di porta è 4502).
   * Experience Manager di nome utente e password del servizio del passaggio precedente.

1. Adobe L’Assistenza clienti per Experience Manager fornisce le credenziali FTP e l’accesso al feature pack 18912.
1. Quando si riceve il feature pack 18912, installarlo.

   Consulta [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md) per ulteriori informazioni sull’utilizzo di Distribuzione di software e pacchetti in Experience Manager.
