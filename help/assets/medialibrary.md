---
title: Confronta [!DNL Assets] e le offerte Media Library
description: Confronta  [!DNL Experience Manager Assets] e le funzioni di Media Library e conosce le differenze.
contentOwner: AG
role: Architetto, leader
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---


# [!DNL Experience Manager Assets] rispetto a  [!DNL Experience Manager] Media Library  {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] è una parte integrante della  [!DNL Experience Manager] piattaforma. Questa integrazione è considerata un importante vantaggio di [!DNL Experience Manager] e garantisce coerenza nella gestione dei contenuti e un’elevata produttività per gli autori dei contenuti.

## Cos’è [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] è una funzionalità di  [!DNL Experience Manager] che consente di gestire le risorse digitali (immagini, video, documenti, clip audio e altro) in un archivio basato su web. [!DNL Assets] include il supporto per metadati, rappresentazioni, Asset Finder e l’interfaccia di amministrazione.

## Che cos&#39;è la [!DNL Experience Manager] Media Library? {#what-is-the-aem-media-library}

La [!DNL Experience Manager] Media Library è una parte designata dell’ archivio di contenuti WCM [!DNL Experience Manager] in cui vengono memorizzate le immagini e altre risorse condivise. La libreria multimediale offre funzionalità di base per la gestione delle risorse digitali a WCM.

## Cosa ottengo da [!DNL Assets] che non fa parte di WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Le funzioni univoche disponibili solo per i clienti di [!DNL Assets] sono:

* La possibilità di estrarre e modificare metadati diversi da titolo, tag e descrizione.
* L’ [!DNL Assets] amministratore, disponibile dalla schermata di benvenuto.
* Tutti i passaggi del flusso di lavoro relativi a Digital Asset Management, ad esempio i profili di caricamento e acquisizione, eliminazione, gestione delle risorse secondarie, gestione dei metadati ed elaborazione.
* Librerie incluse `dam` nello spazio del pacchetto.

Per utilizzare queste funzioni è necessaria una licenza valida di [!DNL Assets].

## [!DNL Assets] è disponibile come pacchetto separato? {#is-aem-assets-available-as-a-separate-package}

No. Per semplificare l&#39;installazione e la distribuzione, tutte le applicazioni e i componenti aggiuntivi [!DNL Experience Manager] vengono forniti in un unico pacchetto con tutte le funzionalità incluse. Questo non implica che si dispone dell&#39;autorizzazione per utilizzare tutte le funzionalità del pacchetto.

## Voglio modificare i metadati delle risorse digitali. È necessario [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Se stai pianificando di modificare metadati diversi da titolo, descrizione e tag, è necessario concedere la licenza [!DNL Assets].

## Voglio utilizzare il predicato categoria sul mio sito web. È necessario [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sì, il predicato della categoria fa parte di [!DNL Assets] e richiede una licenza [!DNL Assets].

## Desidero ridimensionare automaticamente le immagini al momento dell’importazione. È necessario [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

No. Il ridimensionamento e la trasformazione automatica basata sul flusso di lavoro delle immagini statiche e la possibilità di gestire le rappresentazioni fanno parte della libreria multimediale [!DNL Experience Manager]. Queste funzioni non richiedono una licenza [!DNL Assets].

## Voglio ridimensionare le immagini utilizzando un componente immagine personalizzato. È necessario [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Il componente immagine fa parte di WCM. La libreria grafica utilizzata dal componente immagine (ma anche da [!DNL Assets]) fa parte della piattaforma [!DNL Experience Manager] e non richiede una licenza [!DNL Assets].

## Come posso impedire ai miei utenti di utilizzare [!DNL Assets] se non ho concesso la licenza [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Puoi rimuovere tutti i flussi di lavoro, i componenti, le tassonomie, le opzioni e l’ amministratore [!DNL Assets] specifici di [!DNL Experience Manager] da [!DNL Assets]. In questo modo si evita agli utenti di utilizzare accidentalmente le funzioni [!DNL Assets] che non sono state autorizzate.

## Desidero aggiungere immagini a una pagina e ritagliarle e ridimensionarle. È necessario [!DNL Assets]? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Per questo caso d’uso non è necessario acquistare [!DNL Assets], anche l’utilizzo della Libreria multimediale non è necessario per utilizzare le immagini su un sito web, in quanto il componente immagine intelligente consente di caricare le immagini direttamente nella pagina.

## Elenco dettagliato delle funzioni disponibili in [!DNL Assets] rispetto a Media Library {#listoffeatures}

[!DNL Experience Manager Assets]

* Raccolte e lightbox
* Proprietà e gestione avanzate dei metadati
* Adobe Asset Link (collegamento a Creative Cloud per enterprise)
* App desktop [!DNL Experience Manager] 
* Profili di elaborazione
* [!DNL Adobe InDesign Server] integrazione
* Modelli di risorse e framework di produttori di cataloghi
* [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator] e  [!DNL Adobe InDesign] integrazione
* Gestione delle risorse multilingue
* Integrazione PIM
* Gestione dei diritti
* Supporto Camera Raw
* Gestione e configurazione dei facet di ricerca
* Flussi di lavoro DAM predefiniti (ad esempio, servizio fotografico)
* Reporting e analisi delle risorse denominate Insights
* Gestione risorse 3D
* Risorse collegate
* Brand Portal
* Accesso self-service
* Sfoglia, cerca e scarica
* Raccolte e condivisione cartelle
* Strumenti di amministrazione e interfaccia
* Assegnazione tag avanzati
* Ricerca visiva

**Libreria multimediale**

* Proprietà dei metadati di base
* Gestione dei tag
* Controllo della versione
* Rendering statici
* Progetti, attività, creazione di flussi di lavoro
* Flusso di attività (timeline)
* Query Builder (API)
* Integrazione Marketing Cloud
* Personalizzazione ed estensione dell’interfaccia utente
* Commenti e annotazioni

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Descrizione del prodotto on-premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

