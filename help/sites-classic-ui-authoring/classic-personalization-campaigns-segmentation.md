---
title: Segmentazione
seo-title: Understanding Segmentation
description: La segmentazione è un concetto chiave per la creazione di una campagna. In molti casi, è necessario che i segmenti siano già definiti prima che venga avviata una campagna.
seo-description: Segmentation is a key consideration when creating a campaign. In most cases, you will need to have segments already defined before starting your campaign.
uuid: 609d83b3-df0e-44ad-8e27-90b676d2666b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bb75f4ab-d983-45f6-98a3-da8bd9b63751
exl-id: 9092977b-b558-42a3-8092-4615fbc0a08e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 72%

---

# Segmentazione{#understanding-segmentation}

La segmentazione è un concetto chiave per la creazione di una campagna. In molti casi, è necessario che i segmenti siano già definiti prima che venga avviata una campagna.

I visitatori che arrivano a un sito hanno interessi e obiettivi diversi. Per il successo di operazioni di marketing online, è importante comprendere tali obiettivi e soddisfare le aspettative dei visitatori.

La segmentazione consente di conseguire tale scopo mediante l’analisi e la caratterizzazione delle seguenti caratteristiche del visitatore:

* attività sul sito web
* profilo
* attività su altri siti web

Il contenuto può quindi essere mirato per le esigenze e gli interessi del visitatore, a seconda dei segmenti di corrispondenza.

## Utilizzo della segmentazione {#using-segmentation}

I segmenti sono definiti in [Configurazione della segmentazione](/help/sites-administering/campaign-segmentation.md). Vengono utilizzati per gestire il contenuto effettivo visualizzato da un pubblico specifico.

## Terminologia di segmentazione {#segmentation-terminology}

Quando si parla di segmentazione, viene spesso utilizzata la seguente terminologia:

**Visitatore** Un visitatore è una persona che visita un sito web. La sua visita inizia in genere da una pagina di riferimento, per procedere alla visualizzazione di una o più pagine del sito web. In base ai dettagli della visita, è possibile delineare un profilo comportamentale.

**Utente** Un utente è un visitatore che si registra con il sito web per ricevere un profilo di account. Per generare il profilo, l’utente fornisce informazioni aggiuntive, ad esempio indirizzo e-mail e genere. È inoltre possibile raccogliere informazioni aggiuntive, quali attività nella community e pattern di acquisto. Sulla base delle informazioni fornite nel profilo, è possibile creare un profilo demografico.

**Caratteristica** Una caratteristica è una proprietà di un visitatore che può essere utilizzata per determinare l’appartenenza a un segmento specifico.

**Segmento** Un segmento è una raccolta di visitatori che condividono determinate caratteristiche. I segmenti devono essere distinti, con solo un minimo di sovrapposizione con altri segmenti.

**Caratteristiche comportamentali** Le caratteristiche comportamentali sono quelle relative al comportamento di un visitatore sul sito web. Comprendono:

* Interesse nel sito web, inclusi pagine visitate e prodotti acquistati.
* Interesse nel sito Web di provenienza, inclusi termini di ricerca utilizzati o annunci pubblicitari su cui il visitatore ha fatto clic.
* Interesse in altri siti; questo viene determinato tramite strumenti quali Spyjax.
* Fedeltà del visitatore; durata e frequenza delle visite.

**Caratteristiche demografiche** Queste caratteristiche comprendono:

* Età
* Reddito
* Dimensione del nucleo familiare
* Stato civile
* Genere
* Dove si trova

**Caratteristiche derivate**

Alcune caratteristiche demografiche sono difficili da determinare senza la registrazione, ma possono essere derivate dalla combinazione di caratteristiche comportamentali e demografiche.

Ad esempio, la combinazione dell’URL di riferimento (come tratto comportamentale) con i dati demografici (acquisiti da strumenti come [Google Ad Planner](https://www.google.com/adplanner/)) permette ai proprietari dei siti di ricavare i tratti demografici dei loro visitatori

**Sottosegmento** Un segmento può essere suddiviso in diversi sottosegmenti. Questo viene effettuato mediante la definizione di caratteristiche aggiuntive.

**Pagina teaser** Una pagina teaser viene indirizzata a un pubblico specifico. Contiene dei contenuti riutilizzabili che possono essere utilizzati nel paragrafo del teaser.

**Campaign** Una campagna è una raccolta di pagine teaser e pagine di marketing e-mail, come newsletter o inviti. In genere una campagna ha una durata limitata e alla sua scadenza viene sostituita da un’altra campagna.

**Paragrafo teaser** Si tratta di un paragrafo che richiama il contenuto di un’altra pagina a seconda di una strategia di selezione. Tale strategia di selezione può basarsi su segmenti e campagne.

**Elenco** Un elenco viene estratto da un segmento di utenti registrati. Ad esempio, la località da cui dipende il contenuto del paragrafo teaser.

>[!NOTE]
>
>Vedi [Segmentazione](/help/sites-administering/campaign-segmentation.md) per ulteriori informazioni sui segmenti in AEM.
