---
title: Bundle OSGi
seo-title: OSGI Bundles
description: Suggerimenti per la gestione dei bundle OSGi
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

# Bundle OSGi{#osgi-bundles}

## Usa controllo delle versioni semantiche {#use-semantic-versioning}

Le best practice concordate per la numerazione delle versioni semantiche sono disponibili all’indirizzo [https://semver.org/](https://semver.org/).

## Non incorporare più classi e file jar di quanto strettamente necessario nei bundle OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Le librerie comuni devono essere suddivise in bundle separati. Questo ne consentirà il riutilizzo in tutti i bundle. Quando si esegue il wrapping di un *JAR* in un bundle OSGI, assicurati di controllare le origini online per verificare se qualcuno l’ha già fatto in precedenza. Alcuni luoghi comuni in cui trovare i bundle wrapper esistenti sono: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes e SpringSource Enterprise Bundle Repository.

## Dipende dalle versioni più basse necessarie del bundle {#depend-on-the-lowest-needed-bundle-versions}

Per le dipendenze dei tempi di compilazione nei file POM, dipende sempre dalla versione più bassa necessaria che espone l’API necessaria. Questo consentirà una maggiore compatibilità con le versioni precedenti e semplificherà il backporting delle correzioni per le versioni precedenti.

## Esportare un set minimo di pacchetti dai bundle OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Non appena un pacchetto è stato esportato, abbiamo creato un’API da cui gli altri possono dipendere. Assicurati di esportare il meno possibile e assicurati che ciò che viene esportato sia un’API. È molto più facile prendere un metodo/classe privato e renderlo pubblico che prendere qualcosa che è stato precedentemente esportato e renderlo privato.

Le implementazioni devono sempre essere posizionate in un *impl* pacchetto. Per impostazione predefinita, il *maven-bundle-plugin* esporta qualsiasi elemento del progetto che non ha un *impl* nel suo nome.

## Definisci sempre in modo esplicito una versione semantica per ciascun pacchetto esportato {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Questo consentirà ai consumatori della tua API di evolversi insieme a te. In questo caso, segui sempre le best practice per il controllo delle versioni semantiche. In questo modo i consumatori della tua API potranno sapere quali tipi di modifiche aspettarsi in una nuova versione.

## Includi informazioni sul metatipo se esposte {#include-metatype-information-where-exposed}

Specificando informazioni significative sui metatipi, i servizi e i componenti saranno più facili da comprendere nella console Felix. Un elenco di annotazioni e attributi SCR è disponibile all’indirizzo: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
