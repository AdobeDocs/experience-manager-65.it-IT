---
title: Supporto crittografia per le proprietà di configurazione
seo-title: Encryption Support for Configuration Properties
description: Supporto crittografia per le proprietà di configurazione
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Supporto crittografia per le proprietà di configurazione{#encryption-support-for-configuration-properties}

## Panoramica {#overview}

Questa funzione consente di memorizzare tutte le proprietà di configurazione OSGi in un modulo crittografato protetto anziché in un testo trasparente. Il modulo nell’interfaccia utente della console Web viene utilizzato per creare testo crittografato a partire da testo non crittografato utilizzando la chiave master di crittografia a livello di sistema.

È stato aggiunto il supporto del plug-in di configurazione OSGi per decrittografare la proprietà prima che venga utilizzata da un servizio.

>[!NOTE]
>
>I servizi che prevedono un valore crittografato devono utilizzare il controllo IsProtected per verificare se il valore è crittografato prima di tentare di decrittografarlo, in quanto potrebbe essere già stato decrittografato.

## Abilitazione del supporto per la crittografia {#enabling-encryption-support}

Questi passaggi mostrano come crittografare la password SMTP per il servizio Mail. Puoi completare questi passaggi per una proprietà OSGI da crittografare.

1. Vai alla Console Web AEM in *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Nell&#39;angolo in alto a sinistra, vai a **Principale - Supporto Crypto**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. La **Supporto Crypto della console Web Adobe Experience Manager** viene visualizzata la pagina .

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. In **Testo normale** immettere il testo dei dati sensibili che si desidera proteggere.
1. Seleziona **Protect**. Il testo protetto viene visualizzato come testo crittografato.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copiare il testo protetto dal passaggio 5 e incollarlo nel valore del modulo OSGI. In questo esempio, la crittografia **Password SMTP** viene aggiunto al *Servizio e-mail Day CQ*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Salva le proprietà del servizio Day CQ Mail. La password SMTP verrà ora inviata come valore crittografato.

## Supporto per decrittografia {#decryption-support}

AEM ora fornisce un plug-in di configurazione per decrittografare le proprietà di configurazione. Questo plug-in AEM decrittograferà automaticamente e recupererà le proprietà di cancellazione del testo.
