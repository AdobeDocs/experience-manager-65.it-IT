---
title: Utilizzo di Maven for Communities
seo-title: Utilizzo di Maven for Communities
description: Jar API di AEM Communities e Jar API di AEM Uber
seo-description: Jar API di AEM Communities e Jar API di AEM Uber
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# Utilizzo di Maven for Communities {#using-maven-for-communities}

## Panoramica {#overview}

Questa sezione della documentazione di AEM Communities è oltre a:

* [Creazione di progetti AEM con Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Esistono ora due artefatti &quot;uber&quot; che sostituiscono singoli artefatti:

* Jar API di AEM [Communities](#communities-api-jar-artifact)
* Jar API di AEM [Uber](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Artifact API community {#communities-api-jar-artifact}

Di seguito è riportato un esempio di GAV per il Jar API di AEM Communities:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

Verificate che la versione specificata corrisponda alla versione del pacchetto Community installata per AEM Communities. Per verificare il numero di versione installato:

1. Effettua l’accesso con privilegi amministrativi.
1. Passa a Gestione [](../../help/sites-administering/package-manager.md)pacchetti. Ad esempio, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Individuate il pacchetto *cq-socialcommunity-pkg-1.x.xxx*
1. Estraete la versione dal nome del pacchetto:
   * La prima versione di AEM 6.3 è 1.11.170.
   * I Feature Pack saranno versioni 1.12.xxx.

>[!NOTE]
>
>Si consiglia di essere aggiornati con la versione più recente di Communities.
>
>Visitate la sezione [Ultime release](deploy-communities.md#latest-releases) per identificare la versione più recente.


## Esempio di dipendenza del cielo {#maven-dependency-example}

È necessario specificare lo jar dell&#39;API Communities prima dell&#39;API Uber.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
