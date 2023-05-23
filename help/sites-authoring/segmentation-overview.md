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

La segmentazione è un concetto chiave per la creazione di una campagna. Nella maggior parte dei casi, prima di avviare la campagna dovrai aver già definito i segmenti.

I visitatori del sito hanno interessi e obiettivi diversi quando arrivano su un sito. Comprendere questi obiettivi e soddisfare le aspettative è un importante fattore di successo per il marketing online.

La segmentazione consente di ottenere questo risultato analizzando e caratterizzando i:

* attività sul sito web
* profilo
* attività su altri siti web

Il contenuto può quindi essere mirato in modo specifico per le esigenze e gli interessi del visitatore, a seconda dei segmenti di corrispondenza.

## Utilizzo della segmentazione {#using-segmentation}

I segmenti sono definiti in [Configurazione della segmentazione](/help/sites-administering/campaign-segmentation.md). Vengono utilizzati per gestire il contenuto effettivo visualizzato da un pubblico specifico.

## Terminologia di segmentazione {#segmentation-terminology}

Quando si parla di segmentazione, viene spesso utilizzata la seguente terminologia:

**Visitatore** Un visitatore è una persona che visita un sito web. La visita di quella persona in genere inizia da una pagina di riferimento, quindi passa a una o più visualizzazioni di pagina sul tuo sito web. Puoi creare un profilo comportamentale dai dettagli della visita di quella persona.

**Utente** Un utente è un visitatore che si è registrato sul sito Web per ricevere un profilo di account. Per generare il loro profilo forniscono un’identificazione aggiuntiva, ad esempio un indirizzo e-mail e il genere, tra gli altri. È inoltre possibile raccogliere ulteriori informazioni, tra cui le attività della community e i modelli di acquisto. In base alle informazioni fornite nel profilo, è possibile creare un profilo demografico.

**Caratteristica** Una caratteristica è una proprietà di un visitatore che può essere utilizzata per determinare l’appartenenza a un segmento specifico.

**Segmento** Un segmento è una raccolta di visitatori che condividono determinate caratteristiche. I segmenti devono essere distinti, con solo un minimo di sovrapposizione con altri segmenti.

**Caratteristiche comportamentali** Le caratteristiche comportamentali sono quelle relative al comportamento di un visitatore sul sito web. Comprendono:

* Interesse nel sito web, inclusi pagine visitate e prodotti acquistati.
* Interesse nel sito Web di provenienza, inclusi termini di ricerca utilizzati o annunci pubblicitari su cui il visitatore ha fatto clic.
* Interesse in altri siti; questo viene determinato tramite strumenti quali Spyjax.
* Fedeltà del visitatore; durata della visita, frequenza delle visite.

**Caratteristiche demografiche** Queste sono le caratteristiche della popolazione selezionata, tra cui:

* Età
* Reddito
* Dimensioni della famiglia
* Stato civile
* Genere
* Dove si trova

**Caratteristiche derivate** Alcuni tratti demografici sono difficili da determinare senza la registrazione, ma possono essere derivati dalla combinazione di tratti comportamentali e demografici.

Ad esempio, la combinazione dell’URL di riferimento (come tratto comportamentale) con i dati demografici (acquisiti da strumenti come [Google Ad Planner](https://www.google.com/adplanner/)) permette ai proprietari dei siti di ricavare i tratti demografici dei loro visitatori

**Sottosegmento** Un segmento può essere suddiviso in diversi sottosegmenti. Questo viene effettuato mediante la definizione di caratteristiche aggiuntive.

**Pagina teaser** Una pagina teaser si rivolge a un pubblico specifico. Contiene dei contenuti riutilizzabili che possono essere utilizzati nel paragrafo del teaser.

**Campagna** Una campagna è una raccolta di pagine teaser e pagine di marketing e-mail, come newsletter o inviti. In genere una campagna ha una durata limitata e viene sostituita da un’altra campagna.

**Paragrafo teaser** Questo è un paragrafo che richiama il contenuto da un’altra pagina a seconda di una strategia di selezione. Tale strategia di selezione può basarsi su segmenti e campagne.

**Elenco** Un elenco viene estratto da un segmento di utenti registrati. Ad esempio, la località da cui dipende il contenuto del paragrafo teaser.

>[!NOTE]
>
>Consulta [Segmentazione](/help/sites-administering/campaign-segmentation.md) per ulteriori informazioni sui segmenti dell’AEM.
