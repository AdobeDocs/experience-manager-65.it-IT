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
ht-degree: 89%

---

# Personalizzazione e targeting dei contenuti {#personalization}

## Personalizzazione e targeting dei contenuti {#personalization-and-content-targeting}

AEM fornisce un set di strumenti per la creazione e modifica di contenuti con destinazione e la presentazione di esperienze personali.

## Modalità di targeting {#targeting-mode}

[Puoi creare contenuti mirati (di destinazione) utilizzando la modalità di targeting di AEM. ](/help/sites-authoring/content-targeting-touch.md) La modalità di targeting e i componenti di destinazione forniscono gli strumenti necessari per creare i contenuti da usare nelle esperienze delle attività di marketing.

## Attività {#activities}

Le attività definiscono e organizzano le iniziative di marketing. Le attività comprendono il pubblico di destinazione e il periodo di tempo in cui il targeting viene applicato.

Ad esempio, il catalogo dei prodotti We.Retail include teaser che focalizzano l’attenzione sui prodotti stagionali. L&#39;attività &quot;Sports estivi&quot; definisce i segmenti di mercato a cui i teaser si rivolgono durante i mesi estivi.

Le attività identificano anche il [motore di destinazione](/help/sites-authoring/personalization.md#targeting-engine) utilizzato dalle tue pagine.

Usa la [console Attività](/help/sites-authoring/activitylib.md) per creare e gestire le attività dei tuoi marchi. Puoi anche creare delle attività mentre [realizzi contenuti mirati](/help/sites-authoring/content-targeting-touch.md).

## Esperienze {#experiences}

Per ogni attività, definisci una o più esperienze che identificano il pubblico di destinazione. AEM ti consente di controllare il contenuto che comprende ogni esperienza.

La definizione del pubblico si basa sulla segmentazione del mercato creata con AEM o Adobe Target. Quando un visitatore apre una pagina web, la logica della pagina determina a che tipo di pubblico appartiene e visualizza il contenuto che hai creato per quel pubblico.

Ad esempio, un&#39;attività definisce le esperienze per due segmenti di pubblico distinti: le donne over 30 anni e le donne under 30 anni. La pagina Donne del sito Web We.Retail mostra diversi prodotti per ogni esperienza.

È possibile definire le esperienze per un&#39;attività. Usa la [console Attività](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) o la [modalità Targeting](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) per aggiungere le esperienze a un&#39;attività.

## Offerte {#offers}

Un&#39;offerta è un contenuto visualizzato in una certa ubicazione della pagina per una certa esperienza. Utilizza offerte diverse per le diverse esperienze e massimizza l&#39;efficacia dei contenuti per il tuo pubblico.

Ad esempio, la pagina Donne del sito web di esempio We.Retail può utilizzare le offerte come immagine teaser che appare nella parte superiore della pagina. Le offerte utilizzate come teaser sono diverse per l&#39;esperienza Donna Over 30 e per l&#39;esperienza Donna Under 30.

Usa la [console Offerte](/help/sites-authoring/offerlib.md) per creare offerte da utilizzare in più esperienze. Crea le offerte per un uso singolo o aggiungi le offerte da una libreria di offerte durante la [creazione di contenuti personalizzati](/help/sites-authoring/content-targeting-touch.md).

## Motore di targeting {#targeting-engine}

Il motore di destinazione è il meccanismo che definisce la logica per la creazione dei contenuti mirati. Le [attività](/help/sites-authoring/activitylib.md) sono configurate per utilizzare uno di due motori di targeting disponibili: AEM e Adobe Target.

### AEM {#aem}

AEM fornisce un motore di destinazione integrato che elabora le richieste delle pagine e determina il contenuto da visualizzare. Quando utilizzi il motore di targeting di AEM, puoi usare solo i segmenti creati con AEM per definire il pubblico delle esperienze.

### Adobe Target {#adobe-target}

Il motore di targeting di Adobe Target permette di tenere traccia delle informazioni raccolte dalle visite della pagina in Adobe Target.

* Con questo motore di destinazione, si utilizzano i segmenti importati da Adobe Target per definire il pubblico delle esperienze.
* Le attività che sfruttano Adobe Target vengono [sincronizzate con Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Puoi usare questo motore di targeting dopo averlo [integrato con Adobe Target](/help/sites-administering/opt-in.md).
