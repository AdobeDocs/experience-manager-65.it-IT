---
title: Bundle OSGI
seo-title: OSGI Bundles
description: Suggerimenti per gestire i bundle OSGi
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Bundle OSGI{#osgi-bundles}

## Utilizzare le versioni semantiche {#use-semantic-versioning}

Le best practice concordate per la numerazione delle versioni semantiche sono disponibili all&#39;indirizzo [https://semver.org/](https://semver.org/).

## Non incorporare più classi e jar di quanto strettamente necessario nei bundle OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Le librerie comuni devono essere suddivise in bundle separati. Questo consentirà loro di essere riutilizzati nei vostri bundle. Quando si racchiude un *JAR* in un bundle OSGI, assicurati di controllare le fonti online per vedere se qualcuno ha già fatto questo prima. Alcuni luoghi comuni per trovare i pacchetti di wrapper esistenti sono: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes e il SpringSource Enterprise Bundle Repository.

## A seconda delle versioni del bundle necessarie più basse {#depend-on-the-lowest-needed-bundle-versions}

Per la compilazione delle dipendenze temporali nei file POM, dipende sempre dalla versione più bassa necessaria che espone l’API necessaria. Ciò consentirà una maggiore compatibilità con le versioni precedenti e faciliterà il backporting delle correzioni alle versioni precedenti.

## Esportare un set minimo di pacchetti dai bundle OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Non appena un pacchetto è stato esportato, abbiamo creato un’API da cui gli altri possono dipendere. Accertati di esportare il meno possibile e assicurati che ciò che viene esportato sia un’API. È molto più facile prendere un metodo/classe privato e renderlo pubblico che prendere qualcosa che è stato precedentemente esportato e renderlo privato.

Le implementazioni devono sempre essere posizionate in un *impl* pacchetto. Per impostazione predefinita, la *maven-bundle-plugin* esporta qualsiasi elemento del progetto che non abbia un *impl* a nome.

## Definire sempre esplicitamente una versione semantica per ogni pacchetto esportato {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Questo consentirà ai consumatori della tua API di evolvere insieme a te. In questo modo, segui sempre le best practice relative alle versioni semantiche. Questo consente ai consumatori della tua API di sapere quali tipi di modifiche aspettarsi in una nuova versione.

## Includi informazioni sui metadati se esposti {#include-metatype-information-where-exposed}

Specificando informazioni significative sul tipo di metrica, i tuoi servizi e componenti risulteranno più facili da comprendere nella console Felix. Un elenco delle annotazioni e degli attributi SCR si trova in: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
