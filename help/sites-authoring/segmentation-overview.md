---
title: Segmentazione durante la creazione di una campagna
description: La segmentazione è un concetto chiave per la creazione di una campagna.
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 31%

---

# Segmentazione{#understanding-segmentation}

La segmentazione è un concetto chiave per la creazione di una campagna. Nella maggior parte dei casi, è necessario che i segmenti siano già definiti prima di avviare la campagna.

I visitatori del sito hanno interessi e obiettivi diversi quando accedono a un sito. Comprendere questi obiettivi e soddisfare le aspettative è un importante fattore di successo per il marketing online.

La segmentazione consente di ottenere questo risultato analizzando e caratterizzando i seguenti elementi:

* attività sul sito web
* profilo
* attività su altri siti web

Il contenuto può quindi essere mirato in modo specifico alle esigenze e agli interessi del visitatore, a seconda dei segmenti a cui corrisponde.

## Utilizzo della segmentazione {#using-segmentation}

I segmenti sono definiti in [Configurazione della segmentazione](/help/sites-administering/campaign-segmentation.md). Vengono utilizzati per gestire il contenuto effettivo visualizzato da un pubblico specifico.

## Terminologia di segmentazione {#segmentation-terminology}

Quando si parla di segmentazione, viene spesso utilizzata la seguente terminologia:

**Visitatore** Un visitatore è una persona che visita un sito web. La visita di tale persona inizia in genere da una pagina di riferimento, quindi passa a una o più visualizzazioni di pagina sul tuo sito web. Puoi creare un profilo comportamentale dai dettagli della visita di quella persona.

**Utente** Un utente è un visitatore che si registra con il sito web per ricevere un profilo di account. Per generare il loro profilo, forniscono un’identificazione aggiuntiva, ad esempio un indirizzo e-mail e un genere. È inoltre possibile raccogliere informazioni aggiuntive, tra cui attività della community e modelli di acquisto, ancora una volta. In base alle informazioni fornite nel profilo, è possibile creare un profilo demografico.

**Caratteristica** Una caratteristica è una proprietà di un visitatore che può essere utilizzata per determinare l’appartenenza a un segmento specifico.

**Segmento** Un segmento è una raccolta di visitatori che condividono determinate caratteristiche. I segmenti devono essere distinti, con solo un minimo di sovrapposizione con altri segmenti.

**Caratteristiche comportamentali** Le caratteristiche comportamentali sono quelle relative al comportamento di un visitatore sul sito web. Comprendono:

* Interesse nel sito web, inclusi pagine visitate e prodotti acquistati.
* Interesse nel sito Web di provenienza, inclusi termini di ricerca utilizzati o annunci pubblicitari su cui il visitatore ha fatto clic.
* Interesse in altri siti; questo viene determinato tramite strumenti quali Spyjax.
* Fedeltà dei visitatori; durata della visita, frequenza delle visite.

**Caratteristiche demografiche** Queste caratteristiche comprendono:

* Età
* Reddito
* Dimensione familiare
* Stato civile
* Genere
* Dove si trova

**Caratteristiche derivate** Alcune caratteristiche demografiche sono difficili da determinare senza la registrazione, ma possono essere derivate dalla combinazione di caratteristiche comportamentali e demografiche.

Ad esempio, la combinazione dell’URL di riferimento (come tratto comportamentale) con i dati demografici (acquisiti da strumenti come [Google Ad Planner](https://www.google.com/adplanner/)) permette ai proprietari dei siti di ricavare i tratti demografici dei loro visitatori

**Sottosegmento** Un segmento può essere suddiviso in diversi sottosegmenti. Questo viene effettuato mediante la definizione di caratteristiche aggiuntive.

**Pagina teaser** Una pagina teaser viene indirizzata a un pubblico specifico. Contiene dei contenuti riutilizzabili che possono essere utilizzati nel paragrafo del teaser.

**Campaign** Una campagna è una raccolta di pagine teaser e pagine di marketing e-mail, come newsletter o inviti. In genere una campagna viene eseguita per un periodo limitato e viene sostituita da un’altra campagna.

**Paragrafo teaser** Si tratta di un paragrafo che richiama il contenuto di un’altra pagina a seconda di una strategia di selezione. Tale strategia di selezione può basarsi su segmenti e campagne.

**Elenco** Un elenco viene estratto da un segmento di utenti registrati. Ad esempio, la località da cui dipende il contenuto del paragrafo teaser.

>[!NOTE]
>
>Vedi [Segmentazione](/help/sites-administering/campaign-segmentation.md) per ulteriori informazioni sui segmenti in AEM.
