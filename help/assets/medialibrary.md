---
title: Utilizza Media Library per la gestione di base delle risorse digitali
description: "[!DNL Experience Manager Assets] e Media Library per la gestione delle risorse."
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# Utilizza Media Library per la gestione di base delle risorse {#manage-assets-using-media-library}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=en) |
| AEM 6.5 | Questo articolo |

La piattaforma [!DNL Adobe Experience Manager] offre funzionalità diverse per la gestione delle risorse. Media Library consente agli utenti di caricare un numero limitato di risorse nell’archivio, cercare e utilizzare tali risorse nelle pagine web ed eseguire semplici attività di gestione delle risorse sulle risorse.

Media Library è una soluzione leggera di gestione delle risorse digitali (DAM) fornita con licenza [!DNL Adobe Experience Manager Sites]. [!DNL Sites] è un&#39;offerta WCM (Web Content Management). Media Library funziona con tutte le funzionalità di Experience Manager.

La licenza di [!DNL Adobe Experience Manager Assets] è disponibile separatamente per l&#39;acquisto. [!DNL Experience Manager Assets] consente la gestione affidabile delle risorse tramite casi d&#39;uso aziendali, personalizzazioni per metadati, schemi, ricerche e interfaccia utente e molte altre funzionalità oltre a quelle fornite da Media Library.

## Requisiti delle licenze {#avail-media-library-license}

I clienti con licenza [!DNL Sites] possono utilizzare Media Library. Funziona con tutti i componenti di [!DNL Experience Manager].

Media Library viene installato come parte di Sites. Non è richiesta alcuna licenza o pacchetto aggiuntivo oltre alla licenza e all’installazione di Sites.

## Confronto tra [!DNL Assets] e Media Library {#assets-and-media-library}

Experience Manager Assets fornisce funzionalità DAM di livello enterprise. La funzionalità Assets viene fornita con [!DNL Experience Manager] in un singolo pacchetto. Tuttavia, gli utenti che non hanno acquistato una licenza Assets non sono autorizzati a utilizzare le funzioni avanzate di DAM. Senza licenza Assets, sono disponibili solo [funzionalità di Media Library](#use-media-library).

Se si desidera impedire l&#39;utilizzo involontario delle funzionalità di [!DNL Assets] per le quali non si dispone di una licenza, rimuovere tutti i flussi di lavoro, i componenti, le tassonomie, le opzioni e l&#39;amministratore di [!DNL Assets] specifici di [!DNL Assets] da [!DNL Experience Manager]. In questo modo si evita che gli utenti utilizzino accidentalmente le funzionalità di [!DNL Assets] per le quali non è stata concessa la licenza.

## Usa Media Library {#use-media-library}

Media Library fornisce funzioni di base di DAM per i seguenti casi d’uso:

* Pagine Web create con [!DNL Adobe Experience Manager Sites].
* Moduli adattivi e comunicazioni creati con [!DNL Adobe Experience Manager Forms].
* Esperienze di schermata digitale create con [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API REST HTTP per operazioni headless.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Per utilizzare la funzionalità Media Library, è possibile utilizzare l&#39;interfaccia utente predefinita di [!DNL Experience Manager]. Media Library fa parte dell&#39;installazione di [!DNL Experience Manager Sites] e non è richiesta alcuna interfaccia o componente aggiuntivo separato. Utilizzando l’interfaccia esistente, gli utenti di Media Library sono autorizzati a eseguire le seguenti attività:

* Creare cartelle per organizzare le risorse.
* Caricare le risorse.
* Risorse Publish.
* Modificare, spostare e copiare le risorse.
* Sfogliare, filtrare e cercare le risorse (inclusa la ricerca per similarità).
* Per impostazione predefinita, aggiungi e modifica i valori nei campi dei metadati, ad eccezione del campo Tag avanzati, disponibili nella scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] di una risorsa.
* Aggiungere ed eliminare rappresentazioni statiche.
* Scarica cartelle, risorse e rappresentazioni delle risorse.
* Creare le versioni delle risorse.
* Crea ed esegui attività di revisione sulle risorse.
* Annotare le risorse.
* Aggiungere risorse a [!DNL Sites] pagine tramite Content Finder.
* Usa [!DNL Content Fragments].
* Utilizzare API REST HTTP e GraphQL per [!DNL Content Fragments] e risorse multimediali di riferimento, con licenza Sites.
* Integrazione del Marketing Cloud.
* Personalizzare ed estendere l’interfaccia utente per la gestione delle risorse.
* Accedi a Query Builder (API) per estendere la funzionalità di ricerca.
* Creare tag statici.
* Creare progetti e attività.
* Flusso di attività (timeline).
* Commenti e annotazioni.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Molti casi d&#39;uso avanzati di DAM sono stati soddisfatti da [!DNL Experience Manager Assets]. La licenza di Media Library ti autorizza a soddisfare solo i casi d’uso elencati utilizzando Media Library. Se un caso d’uso non è elencato, non utilizzarlo con la licenza Media Library. In caso di domande, contatta l’Assistenza clienti Adobe.

Non è possibile utilizzare smart tag, collegamento [!DNL Asset], selettore [!DNL Asset], assegnazione di tag in blocco, modificare i flussi di lavoro delle risorse o l&#39;interfaccia utente standard [!DNL Adobe Experience Manager] per accedere a Media Library senza licenza [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Funzioni DAM in [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html)
>* [[!DNL Experience Manager] 6.5 Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 descrizione del prodotto on-premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)
