---
title: Bundle OSGI
seo-title: Bundle OSGI
description: Suggerimenti per la gestione dei bundle OSGi
seo-description: Suggerimenti per la gestione dei bundle OSGi
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Bundle OSGI{#osgi-bundles}

## Utilizzare le versioni semantiche {#use-semantic-versioning}

Le best practice concordate per la numerazione delle versioni semantiche sono disponibili all&#39;indirizzo [https://semver.org/](https://semver.org/).

## Non incorporare più classi e jar di quanto strettamente necessario nei bundle OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Le librerie comuni devono essere raggruppate in pacchetti separati. In questo modo sarà possibile riutilizzarli nei bundle. Quando racchiudete un *JAR* in un pacchetto OSGI, verificate di aver controllato le origini online per verificare se qualcuno ha già fatto questo. Alcuni luoghi comuni per trovare i bundle esistenti sono: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes e SpringSource Enterprise Bundle Repository.

## Dipende dalle versioni bundle necessarie più basse {#depend-on-the-lowest-needed-bundle-versions}

Per le dipendenze in fase di compilazione nei file POM, dipende sempre dalla versione minima necessaria che espone l&#39;API necessaria. Ciò consentirà una maggiore compatibilità con le versioni precedenti e faciliterà il backport delle correzioni alle versioni precedenti.

## Esportare un set minimo di pacchetti dai bundle OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Non appena un pacchetto è stato esportato, abbiamo creato un&#39;API da cui gli altri utenti possono dipendere. Assicuratevi di esportare il meno possibile e assicuratevi che ciò che viene esportato sia un&#39;API. È molto più facile prendere un metodo/classe privato e renderlo pubblico che prendere qualcosa che è stato precedentemente esportato e renderlo privato.

Le implementazioni devono sempre essere collocate in un pacchetto *impl* separato. Per impostazione predefinita, il *maven-bundle-plugin* esporta qualsiasi elemento del progetto che non abbia un *impl* nel nome.

## Definire sempre esplicitamente una versione semantica per ciascun pacchetto esportato {#always-explicitly-define-a-semantic-version-for-each-package-exported}

In questo modo i consumatori delle API potranno evolvere insieme a voi. In questo modo, segui sempre le best practice relative alle versioni semantiche. In questo modo gli utenti dell&#39;API potranno sapere quali tipi di modifiche sono previste in una nuova versione.

## Includi informazioni sul tipo di dati in esposizione {#include-metatype-information-where-exposed}

Specificando informazioni significative per il tipo di dati, i vostri servizi e componenti saranno più facili da comprendere nella console Felix. Un elenco delle annotazioni e degli attributi SCR è disponibile all&#39;indirizzo: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
