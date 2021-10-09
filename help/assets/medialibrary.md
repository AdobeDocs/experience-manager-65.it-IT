---
title: Utilizzare Media Library per la gestione di base delle risorse digitali
description: '[!DNL Experience Manager Assets] e Media Library per la gestione delle risorse.'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: 823f36bb7eab6c74a07f90883fa040428d8f8420
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Utilizzare Media Library per la gestione delle risorse di base {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] Platform offre diverse funzionalità per la gestione delle risorse. Media Library consente agli utenti di caricare nell’archivio un numero limitato di risorse, di eseguire ricerche e utilizzarle nelle pagine web e di eseguire semplici attività di gestione delle risorse sulle risorse.

Media Library è una soluzione leggera di gestione delle risorse digitali (DAM) che viene fornita in omaggio con la licenza [!DNL Adobe Experience Manager Sites] . [!DNL Sites] è un’offerta WCM (Web Content Management). Media Library funziona con tutte le funzionalità di Experience Manager.

[!DNL Adobe Experience Manager Assets] licenza disponibile separatamente per l&#39;acquisto. [!DNL Experience Manager Assets] consente una gestione affidabile delle risorse tramite casi d’uso aziendali, personalizzazioni per metadati, schemi, ricerca e interfaccia utente e molte altre funzionalità oltre a quelle offerte da Media Library.

## Requisiti di licenza {#avail-media-library-license}

I clienti con [!DNL Sites] licenza possono utilizzare Media Library. Funziona con tutti i componenti di [!DNL Experience Manager].

Media Library viene installato come parte di Sites. Non è richiesta alcuna licenza o pacchetto aggiuntivo oltre alla licenza e all’installazione di Sites.

## [!DNL Assets] rispetto a Media Library {#assets-and-media-library}

Experience Manager Assets fornisce funzionalità DAM di livello enterprise. La funzionalità Assets viene fornita con [!DNL Experience Manager] in un unico pacchetto. Tuttavia, gli utenti che non hanno acquistato una licenza di Assets non hanno il diritto di utilizzare le funzioni avanzate di DAM. Senza la licenza Assets, sono disponibili solo [funzionalità Media Library](#use-media-library).

Se desideri evitare l’utilizzo non intenzionale di funzionalità [!DNL Assets] prive di licenza, rimuovi tutti i flussi di lavoro, i componenti, le tassonomie, le opzioni e l’amministratore [!DNL Assets] specifici di [!DNL Experience Manager]. [!DNL Assets] In questo modo si evita agli utenti di utilizzare accidentalmente le funzioni [!DNL Assets] che non sono state autorizzate.

## Utilizza Media Library {#use-media-library}

Media Library fornisce funzioni DAM di base per i seguenti casi d’uso:

* Pagine web create utilizzando [!DNL Adobe Experience Manager Sites].
* Moduli adattivi e comunicazioni create utilizzando [!DNL Adobe Experience Manager Forms].
* Esperienze video digitali create utilizzando [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API REST HTTP per operazioni headless.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Per utilizzare la funzionalità Media Library, è possibile utilizzare l&#39;interfaccia utente predefinita [!DNL Experience Manager]. Media Library fa parte dell&#39;installazione di [!DNL Experience Manager Sites] e non è richiesta alcuna interfaccia o componente aggiuntivo separato. Utilizzando l’interfaccia esistente, gli utenti di Media Library possono eseguire le seguenti attività:

* Crea cartelle per organizzare le risorse.
* Carica le risorse.
* Pubblicare le risorse.
* Modificare, spostare e copiare le risorse.
* Sfogliare, filtrare e cercare (include la ricerca per similarità) le risorse.
* Aggiungi i valori ai campi di metadati e modificali, ad eccezione del campo Tag avanzati, disponibili per impostazione predefinita nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa.
* Aggiungi ed elimina rappresentazioni statiche.
* Scaricare cartelle, risorse e rappresentazioni di risorse.
* Creare versioni delle risorse.
* Crea ed esegui attività di revisione sulle risorse.
* Annotare le risorse.
* Aggiungi le risorse alle pagine [!DNL Sites] tramite Content Finder.
* Utilizzo [!DNL Content Fragments].
* Utilizza le API REST HTTP e GraphQL per [!DNL Content Fragments] e le risorse multimediali a cui si fa riferimento, con licenza Sites.
* Integrazione del Marketing Cloud.
* Personalizza ed espandi l’interfaccia utente per la gestione delle risorse.
* Accedi all’API di Query Builder per estendere la funzionalità di ricerca.
* Creare tag statici.
* Progetti e attività di authoring.
* Flusso di attività (timeline).
* Commenti e annotazioni.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Molti casi d’uso avanzati di DAM sono soddisfatti da [!DNL Experience Manager Assets]. La licenza Media Library ti consente di soddisfare solo i casi d’uso elencati utilizzando Media Library. Se non è presente un caso d’uso, non utilizzarlo con una licenza Media Library. In caso di domande, contatta l’Assistenza clienti Adobe.

Tieni presente che non puoi utilizzare tag avanzati, collegamenti [!DNL Asset], selettore [!DNL Asset], assegnazione tag in blocco, modifica flussi di lavoro di risorse o interfaccia utente standard [!DNL Adobe Experience Manager] per accedere a Media Library senza una licenza [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Funzioni di DAM in [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Descrizione del prodotto on-premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

