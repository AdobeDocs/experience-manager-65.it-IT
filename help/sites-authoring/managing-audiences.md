---
title: Gestione dei tipi di pubblico
description: La console Pubblico consente di creare, organizzare e gestire i tipi di pubblico per il tuo account Adobe Target o gestire segmenti per ContextHub o ClientContext
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: 97e02986-049f-4747-a67a-6aa0677b281e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 63%

---

# Gestione dei tipi di pubblico{#managing-audiences}

La console Pubblico consente di creare, organizzare e gestire i tipi di pubblico per il tuo account Adobe Target o gestire segmenti per ContextHub o ClientContext:

* Aggiungere tipi di pubblico: tipi di pubblico Adobe Target o segmenti ContextHub.
* Gestisci tipi di pubblico.

Un pubblico, denominato *segmento* in ContextHub e ClientContext, è una classe di visitatori definita da criteri specifici che determinano chi visualizzerà un&#39;attività con targeting. Quando esegui il targeting di un’attività, puoi selezionare i tipi di pubblico direttamente nel processo di targeting oppure crearne di più nella console Pubblico.

Nella console Pubblico, i tipi di pubblico sono organizzati per marchio.

I tipi di pubblico sono disponibili in modalità Targeting per [la creazione di contenuti con targeting](/help/sites-authoring/content-targeting-touch.md), dove è anche possibile creare dei tipi di pubblico (ma è necessario creare i tipi di pubblico di Adobe Target nella console Tipi di pubblico). I tipi di pubblico creati in modalità Targeting vengono visualizzati nella console Pubblico.

I tipi di pubblico vengono visualizzati con un’etichetta che descrive il tipo di pubblico definito:

* CH - Segmento ContextHub
* CC - Segmento ClientContext
* AT - Pubblico Adobe Target

## Creazione di un segmento ContextHub nella console Pubblico {#creating-a-contexthub-segment-in-the-audiences-console}

Puoi creare un segmento ContextHub nella console Pubblico o durante il processo di targeting.

Per creare un segmento ContextHub nella console Pubblico:

1. Nella console di navigazione, fare clic su **Personalization**. Fai clic su **Tipi di pubblico**.
1. Fai clic su **Crea segmento ContextHub**.

   ![schermata_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. Nella finestra di dialogo **Nuovo segmento ContextHub**, inserisci un titolo, regola l&#39;incremento e fai clic su **Crea**. Il nuovo segmento ContextHub appare nell’elenco dei tipi di pubblico.

   >[!NOTE]
   >
   >Per ordinare l’elenco modificato in base all’ordine decrescente, tocca o fai clic su **Modificato**, così da visualizzare i tipi di pubblico appena creati.

Per ulteriori dettagli sulla creazione di segmenti utilizzando ContextHub, consulta la documentazione [Configurazione della segmentazione con ContextHub](/help/sites-administering/segmentation.md).

## Creazione di un pubblico di Adobe Target tramite la console Pubblico {#creating-an-adobe-target-audience-using-the-audience-console}

Puoi creare i tipi di pubblico di Adobe Target direttamente in AEM utilizzando la console Pubblico.

I tipi di pubblico sono definiti da regole che determinano chi è incluso in un’attività target. Una definizione di pubblico può includere più regole e ogni regola può includere più parametri.

Quando utilizzi più regole, queste vengono combinate tramite l&#39;operatore boolean AND, di conseguenza tutti i potenziali visitatori appartenenti al pubblico devono soddisfare tutte le condizioni definite per essere inclusi nell&#39;attività. Ad esempio, se definisci una regola per il sistema operativo AND una regola per il browser, verranno inclusi nell&#39;attività solo i visitatori che usano sia il sistema operativo sia il browser definiti nelle regole.

>[!NOTE]
>
>Se nel menu **Crea** non trovi **Crea pubblico di destinazione &#x200B;** non disponi delle autorizzazioni necessarie per creare un pubblico. Per creare tipi di pubblico è necessario disporre delle autorizzazioni di scrittura in **/etc/segmentation**. Per impostazione predefinita, gli autori dei contenuti del gruppo sono in possesso di autorizzazioni di scrittura.

Per creare un pubblico di Adobe Target:

1. Nella console di navigazione, fare clic su **Personalization**. Fai clic su **Tipi di pubblico**.

   ![schermata_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. Nella console Pubblico, fai clic su **Crea** e quindi **&#x200B; Crea pubblico Target**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Nella finestra di dialogo **Configurazione Adobe Target**, seleziona la configurazione di destinazione e fai clic su **OK**.
1. Nell&#39;area Regola n. 1 fare clic sul tipo di attributo e immettere le informazioni relative agli attributi nei campi disponibili. Al termine, seleziona il segno di spunta a destra dell’attributo per salvarlo. Per informazioni su tutti gli attributi, consulta [Attributi e relative opzioni](#attributes-and-their-options).
1. Fai clic su **Aggiungi regola** per aggiungere un’altra regola. Immetti tutte le regole necessarie. Le regole sono combinate con l’operatore boolean AND, il che significa che l’audience deve soddisfare tutti i requisiti di ciascuna regola per essere idonea a un’attività.
1. Fai clic su **Avanti**.
1. Immetti un nome per il pubblico e fai clic su **Salva**.
1. Fai clic su **Salva**. Il pubblico è elencato nell’elenco Pubblico.

### Attributi e relative opzioni {#attributes-and-their-options}

Puoi creare regole di targeting per ciascuno dei seguenti attributi:

| **Attributo** | **Descrizione** | **Per ulteriori informazioni** |
|---|---|---|
| **Mobile** | Puoi indirizzare l’attività a chi usa specifici dispositivi mobili, in base a parametri come dispositivo mobile, tipo di dispositivo, fornitore, dimensioni dello schermo (in pixel) e altro ancora. | Consulta la [documentazione Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=it) in Adobe Target. |
| **Personalizzati** | I parametri personalizzati sono parametri mbox. Se passi dei parametri mbox alle mbox o se utilizzi la funzione targetPageParams, tali parametri vengono visualizzati qui per poter essere utilizzati nei tipi di pubblico. | Consulta la [documentazione sui parametri personalizzati](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=it) in Adobe Target. |
| **Sistema operativo** | Puoi eseguire il targeting dei visitatori che utilizzano un determinato sistema operativo. | Eseguire il targeting degli utenti che utilizzano Linux®, Macintosh o Windows. |
| **Pagine del sito** | Puoi indirizzare l’attività ai visitatori che si trovano su una pagina specifica o con un parametro mbox specifico. | Consulta la [documentazione sulle pagine del sito](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=it) in Adobe Target. |
| **Browser** | Puoi eseguire il targeting degli utenti che usano un browser specifico o delle opzioni di browser specifiche quando visitano la tua pagina. | Consulta la [documentazione sulle opzioni del browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=it) in Adobe Target. |
| **Profilo visitatore** | Puoi indirizzare l’attività ai visitatori che soddisfano parametri di profilo specifici. | Consulta la [documentazione sul profilo del visitatore](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=it) in Adobe Target. |
| **Sorgenti di traffico** | Puoi indirizzare l’attività ai visitatori in base al motore di ricerca o alla pagina di destinazione che li rimanda al sito. | Consulta la [documentazione su Sorgenti di traffico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=it) in Adobe Target. |

## Modifica di un pubblico nella console Pubblico {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Puoi modificare solo i tipi di pubblico di Adobe Target creati nella stessa istanza AEM in cui stai modificando. Non è possibile modificare i tipi di pubblico di destinazione creati in ambienti AEM diversi.

Puoi modificare qualsiasi pubblico ContextHub o ClientContext dalla console Pubblico. Puoi modificare anche i tipi di pubblico di Adobe Target, ma solo quelli creati in AEM:

1. Nella console di navigazione, fare clic su **Personalization**. Fai clic su **Tipi di pubblico**.
1. Fai clic sull&#39;icona accanto al segmento ContextHub o ClientContext che desideri modificare e fai clic su **Modifica**.
1. Apporta le modifiche nell&#39;editor segmento. Consulta la documentazione di [ClientContext](/help/sites-administering/campaign-segmentation.md) o [ContextHub](/help/sites-developing/ch-configuring.md).
