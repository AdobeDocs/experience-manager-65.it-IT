---
title: Personalizzazione e targeting dei contenuti
seo-title: Personalizzazione e targeting dei contenuti
description: Scopri come AEM può creare contenuti personalizzati
seo-description: Scopri come AEM può creare contenuti personalizzati
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalizzazione e targeting dei contenuti {#personalization}

## Personalizzazione e targeting dei contenuti {#personalization-and-content-targeting}

AEM fornisce un set di strumenti per la creazione e modifica di contenuti con destinazione e la presentazione di esperienze personali.

## Modalità di targeting {#targeting-mode}

[Puoi creare contenuti mirati (di destinazione) utilizzando la modalità di targeting di AEM. ](/help/sites-authoring/content-targeting-touch.md) La modalità di targeting e i componenti di destinazione forniscono gli strumenti per la creazione di contenuti per le esperienze delle vostre attività di marketing.

## Attività {#activities}

Le attività definiscono e organizzano le iniziative di marketing. Le attività comprendono il pubblico di destinazione e il periodo di tempo in cui il targeting viene applicato.

Ad esempio, il catalogo prodotti We.Retail include teaser che focalizzano l&#39;attenzione sui prodotti stagionali. L&#39;attività &quot;Sports estivi&quot; definisce i segmenti di mercato a cui i teaser si rivolgono durante i mesi estivi.

Le attività identificano anche il [motore di destinazione](/help/sites-authoring/personalization.md#targeting-engine) utilizzato dalle tue pagine.

Usa la [console Attività](/help/sites-authoring/activitylib.md) per creare e gestire le attività dei tuoi marchi. You can also create activities as you [author targeted content](/help/sites-authoring/content-targeting-touch.md).

## Esperienze {#experiences}

Per ogni attività, definisci una o più esperienze che identificano il pubblico di destinazione. AEM ti consente di controllare il contenuto che comprende ogni esperienza.

La definizione del pubblico si basa sulla segmentazione del mercato creata con AEM o Adobe Target. Quando un visitatore apre una pagina web, la logica della pagina determina a che tipo di pubblico appartiene e visualizza il contenuto che hai creato per quel pubblico.

Ad esempio, un&#39;attività definisce le esperienze per due segmenti di pubblico distinti: le donne over 30 anni e le donne under 30 anni. La pagina Web Women del sito Web We.Retail presenta diversi prodotti per ogni esperienza.

È possibile definire le esperienze per un&#39;attività. Usa la [console Attività](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) o la [modalità Targeting](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) per aggiungere le esperienze a un&#39;attività.

## Offerte {#offers}

Un&#39;offerta è un contenuto visualizzato in una certa ubicazione della pagina per una certa esperienza. Utilizza offerte diverse per le diverse esperienze e massimizza l&#39;efficacia dei contenuti per il tuo pubblico.

Ad esempio, la pagina Donne del sito Web di esempio We.Retail può utilizzare offerte come immagine teaser che appare nella parte superiore della pagina. Le offerte utilizzate come teaser sono diverse per l&#39;esperienza Donna Over 30 e per l&#39;esperienza Donna Under 30.

Usa la [console Offerte](/help/sites-authoring/offerlib.md) per creare offerte da utilizzare in più esperienze. Crea le offerte per un uso singolo o aggiungi le offerte da una libreria di offerte durante la [creazione di contenuti personalizzati](/help/sites-authoring/content-targeting-touch.md).

## Motore di destinazione {#targeting-engine}

Il motore di destinazione è il meccanismo che definisce la logica per la creazione dei contenuti mirati. Le [Attività](/help/sites-authoring/activitylib.md) sono configurate per l&#39;utilizzo di uno di due motori di targeting a tua disposizione: AEM e Adobe Target.

### AEM {#aem}

AEM fornisce un motore di destinazione integrato che elabora le richieste delle pagine e determina il contenuto da visualizzare. Quando utilizzi il motore di destinazione AEM, puoi usare solo i segmenti creati con AEM per definire il pubblico delle esperienze.

### Adobe Target {#adobe-target}

Il motore di destinazione Adobe Target permette di tenere traccia e raccogliere le informazioni sulle visite della pagina.

* Con questo motore di destinazione, si utilizzano i segmenti importati da Adobe Target per definire il pubblico delle esperienze.
* Le attività che sfruttano Adobe Target vengono [sincronizzate con Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).
