---
title: Supporto della crittografia per le proprietà di configurazione
description: Scopri il supporto della crittografia per le proprietà di configurazione fornito in AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Supporto della crittografia per le proprietà di configurazione{#encryption-support-for-configuration-properties}

## Panoramica {#overview}

Questa funzione consente di memorizzare tutte le proprietà di configurazione OSGi in un formato crittografato protetto anziché in testo non crittografato. Il modulo nell’interfaccia utente della console Web viene utilizzato per creare testo crittografato da testo non crittografato utilizzando la chiave master di crittografia a livello di sistema.

È stato aggiunto il supporto del plug-in di configurazione OSGi per decrittografare la proprietà prima che venga utilizzata da un servizio.

>[!NOTE]
>
>I servizi che prevedono un valore crittografato devono utilizzare il controllo IsProtected per verificare se il valore è crittografato prima di tentare di decrittografarlo, in quanto potrebbe essere già stato decrittografato.

## Abilitazione del supporto della crittografia {#enabling-encryption-support}

Questi passaggi mostrano come crittografare la password SMTP per il servizio di posta. Puoi completare questi passaggi per una proprietà OSGI che desideri crittografare.

1. Passa alla console web dell’AEM all’indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Nell’angolo in alto a sinistra, vai a **Principale - Supporto crittografia**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. Il **Supporto crittografia console Web Adobe Experience Manager** viene visualizzata.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. In **Testo normale** immettere il testo dei dati sensibili che si desidera proteggere.
1. Seleziona **Protect**. Il testo protetto viene visualizzato come testo crittografato.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copia il testo protetto dal passaggio 5 e incollalo nel valore del modulo OSGI. In questo esempio, la **Password SMTP** viene aggiunto al *Day CQ Mail Service*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Salva le proprietà del servizio di posta Day CQ. La password SMTP verrà ora inviata come valore crittografato.

## Supporto decrittografia {#decryption-support}

AEM fornisce ora un plug-in di configurazione per decrittografare le proprietà di configurazione. Questo plug-in AEM decrittografa e recupera automaticamente le proprietà di testo non crittografato.
