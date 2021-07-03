---
title: Installazione del feature pack 18912 per la migrazione di massa delle risorse
description: Il Feature Pack 18912 consente di caricare in massa le risorse tramite FTP oppure di migrare le risorse da Dynamic Media Classic a Dynamic Media in AEM. Questo pacchetto di funzioni opzionale è disponibile dal supporto Adobe.
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
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Installazione del feature pack 18912 per la migrazione di massa delle risorse{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del feature pack 18912 è *opzionale*.

Il Feature Pack 18912 consente di caricare in massa le risorse direttamente in Dynamic Media - Modalità Scene7 in AEM tramite FTP oppure di migrare le risorse da Dynamic Media Classic in Dynamic Media - Modalità Scene7 in AEM. Il pacchetto di funzioni è disponibile da [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Anche se è possibile utilizzare il pacchetto di funzioni per eseguire la migrazione in massa delle risorse da Dynamic Media Classic a Dynamic Media - Modalità Scene 7 in modalità AEM o per eseguire la migrazione in massa delle risorse utilizzando la funzione FTP in Dynamic Media Classic, questo metodo è consigliato da Adobe *not* a causa della complessità in questione.
>
>Di conseguenza, i pacchetti di funzioni di migrazione, come questo, sono supportati *solo* come parte di un progetto di migrazione quando viene eseguito tramite [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Prima di installare il feature pack, è necessario creare un utente del servizio e fornire tali informazioni al supporto di Adobe.

Vedi anche [Configurazione di Dynamic Media - Modalità Scene7](/help/assets/config-dms7.md).

**Per installare feature pack 18912 per la migrazione di massa delle risorse**

1. Nella tua istanza AEM, passa a **[!UICONTROL Strumenti > Protezione > Utenti]** e seleziona **[!UICONTROL Crea utente]**. L&#39;utente del servizio deve disporre delle autorizzazioni di *lettura/scrittura* per `/content/dam.`
1. Nei campi **[!UICONTROL ID]** e **[!UICONTROL Password]** , immetti un nome utente e una password; ad esempio, **FTP User**. Questo nome viene visualizzato nella timeline come utente che ha creato la risorsa. Quando una risorsa viene caricata da FTP, viene considerata una creazione quando viene caricata sul server FTP e inviata a AEM.
1. Contatta [Adobe Enterprise Customer Care per Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) per richiedere l&#39;accesso al feature pack 18912 per il download. Quando si contatta l&#39;assistenza, potrebbe essere necessario disporre delle seguenti informazioni:

   * Indirizzo IP del server per l’istanza Author, incluso il numero di porta (per impostazione predefinita, il numero di porta è 4502.)
   * AEM nome utente e password del servizio dal passaggio precedente.

1. Adobe Enterprise Customer Care for AEM fornisce le credenziali FTP e l&#39;accesso al feature pack 18912.
1. Quando ricevi il feature pack 18912, installalo.

   Per ulteriori informazioni sull&#39;utilizzo di Distribuzione software e pacchetti in AEM, consulta [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md) .
