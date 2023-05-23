---
title: Personalizzazione e targeting dei contenuti
seo-title: Personalization and Content Targeting
description: Scopri in che modo AEM può creare contenuti personalizzati
seo-description: Learn how AEM can create personalized content
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 35%

---

# Personalizzazione e targeting dei contenuti {#personalization}

## Personalizzazione e targeting dei contenuti {#personalization-and-content-targeting}

L’AEM fornisce un framework di strumenti per la creazione e modifica di contenuti mirati e la presentazione di esperienze personalizzate.

## Modalità di targeting {#targeting-mode}

[Puoi creare contenuti mirati (di destinazione) utilizzando la modalità di targeting di AEM. ](/help/sites-authoring/content-targeting-touch.md) La modalità di targeting e i componenti di destinazione forniscono gli strumenti necessari per creare i contenuti da usare nelle esperienze delle attività di marketing.

## Attività {#activities}

Le attività definiscono e organizzano le attività di marketing. Le attività comprendono i tipi di pubblico per i quali esegui il targeting e il periodo di tempo in cui il targeting viene applicato.

Ad esempio, il catalogo dei prodotti We.Retail include teaser che focalizzano l&#39;attenzione sui prodotti stagionali. L’attività Sport estivi definisce i segmenti di marketing target dei teaser durante i mesi estivi.

Le attività identificano anche [motore di targeting](/help/sites-authoring/personalization.md#targeting-engine) che le tue pagine utilizzano.

Utilizza il [Console Attività](/help/sites-authoring/activitylib.md) per creare e gestire le attività dei tuoi marchi. Puoi anche creare delle attività mentre [realizzi contenuti mirati](/help/sites-authoring/content-targeting-touch.md).

## Esperienze {#experiences}

Per ogni attività, definisci una o più esperienze che identificano il pubblico di destinazione. AEM ti consente di controllare il contenuto che comprende ogni esperienza.

I tipi di pubblico si basano su segmenti di marketing creati in AEM o Adobe Target. Quando un visitatore apre una pagina web, la logica della pagina determina il pubblico a cui appartiene e visualizza il contenuto creato per tale pubblico.

Ad esempio, un&#39;attività definisce le esperienze per due segmenti di pubblico distinti: le donne over 30 anni e le donne under 30 anni. La pagina Donne del sito web We.Retail mostra prodotti diversi per ogni esperienza.

Puoi definire le esperienze per un’attività. È possibile utilizzare [Console Attività](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) o [Modalità di targeting](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) per aggiungere esperienze a un’attività.

## Offerte {#offers}

Un’offerta è un contenuto che viene visualizzato in una posizione su una pagina per un’esperienza. Utilizza offerte diverse per esperienze diverse per massimizzare l’efficacia dei contenuti per il tuo pubblico.

Ad esempio, la pagina Donne del sito web di esempio We.Retail può utilizzare le offerte come immagini teaser che appaiono nella parte superiore della pagina. Un’offerta diversa viene utilizzata come teaser per l’esperienza Femmina over 30 e per l’esperienza Femmina under 30.

Utilizza il [Console Offerte](/help/sites-authoring/offerlib.md) per creare offerte da utilizzare in più esperienze. Creare offerte monouso o aggiungere offerte da una libreria di offerte quando [authoring di contenuti di destinazione](/help/sites-authoring/content-targeting-touch.md).

## Motore di targeting {#targeting-engine}

Il motore di targeting è il meccanismo che guida la logica per il contenuto di destinazione. Le [attività](/help/sites-authoring/activitylib.md) sono configurate per utilizzare uno di due motori di targeting disponibili: AEM e Adobe Target.

### AEM {#aem}

AEM fornisce un motore di targeting integrato che elabora le richieste delle pagine e determina il contenuto da visualizzare. Quando utilizzi il motore di targeting di AEM, puoi usare solo i segmenti creati con AEM per definire il pubblico delle esperienze.

### Adobe Target {#adobe-target}

Il motore di targeting di Adobe Target permette di tenere traccia delle informazioni raccolte dalle visite della pagina in Adobe Target.

* Quando utilizzi questo motore di targeting, puoi utilizzare i segmenti importati da Adobe Target per definire i tipi di pubblico per le esperienze.
* Le attività che utilizzano il motore di Adobe Target sono [sincronizzato con Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Puoi usare questo motore di targeting dopo averlo [integrato con Adobe Target](/help/sites-administering/opt-in.md).
