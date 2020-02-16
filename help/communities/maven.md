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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utilizzo di Maven for Communities {#using-maven-for-communities}

## Panoramica {#overview}

Questa sezione della documentazione di AEM Communities è oltre a:

* [Come creare progetti AEM con Apache Maven](../../help/sites-developing/ht-projects-maven.md)

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
2. Passa a Gestione [](../../help/sites-administering/package-manager.md)pacchetti. Ad esempio, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

3. individuare il pacchetto *cq-socialcommunity-pkg-1.x.xxx*
4. estraete la versione dal nome del pacchetto
   * la prima versione di AEM 6.3 è 1.11.170
   * i pacchetti di funzionalità saranno versioni 1.12.xxx

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
