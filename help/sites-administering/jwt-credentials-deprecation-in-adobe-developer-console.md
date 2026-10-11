---
title: Credenziali JWT nella console Adobe Developer obsolete
description: Informazioni sull’impatto della rimozione delle credenziali JWT in Adobe Developer Console su AEM
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 70%
---
# Credenziali JWT nella console Adobe Developer obsolete {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service deve fare riferimento a [l&#39;articolo comparabile per AEMaaCS versione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=it) per ulteriori informazioni.

[Adobe Developer Console](https://developer.adobe.com/console) viene utilizzato per generare credenziali che consentano l’accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali da server a server OAuth. A partire dal 3 giugno 2024, non sarà possibile creare nuove credenziali dell’account di servizio (JWT) e, a partire dal 27 gennaio 2025, le credenziali JWT esistenti non funzioneranno. È possibile [consultare le informazioni sull’obsolescenza](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration).

Questo articolo fornisce alcuni contesti aggiuntivi su come i clienti di Adobe Experience Manager (AEM) 6.5 devono gestire la rimozione.

L’aspetto principale è che AEM ora supporta le nuove credenziali server-to-server OAuth per AEM. È possibile che sia stata ricevuta un’e-mail con le istruzioni per la migrazione delle credenziali JWT. Adesso è possibile eseguire questa migrazione.

Le sezioni seguenti elencano gli scenari in cui si deve (o in alcuni casi non si deve) sostituire le credenziali dell’account di servizio (JWT) con le credenziali da server a server OAuth, ora che AEM ne fornisce il supporto. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview) migrare le credenziali.

## Integrazione di AEM con altre soluzioni Adobe {#integrating-aem-with-other-adobe-solutions}

**Azione**: esegui la migrazione della configurazione in quanto AEM ora supporta le credenziali OAuth.

**Versioni rilevanti di AEM**: Adobe Managed Services (Service Pack 21 e versioni successive).

I clienti di AEM utilizzano AEM per configurare le integrazioni con tutte le altre soluzioni Adobe. Ad esempio, Adobe Target, Adobe Analytics e altre.

![Integrazione di AEM con altre soluzioni](/help/sites-administering/assets/jwt-deprecation.png)

Consulta [Configurazione delle integrazioni IMS per AEM](/help/sites-administering/setting-up-ims-integrations-for-aem.md) per informazioni dettagliate su come:

* creare configurazioni con le credenziali OAuth
* eseguire la migrazione delle configurazioni create con credenziali JWT per utilizzare quelle OAuth

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: conferma quando è possibile migrare questi elementi dalle credenziali JWT a quelle OAuth.

**Versioni rilevanti di AEM**: Adobe Managed Services (Service Pack 21 e versioni successive).

I progetti Adobe Developer Console vengono creati in modo che possano richiamare le [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È opportuno migrare le credenziali nel progetto Adobe Developer al tipo di credenziali da server a server OAuth, primna della scadenza del tipo di credenziali obsolete JWT, che non ci saranno più da gennaio.
