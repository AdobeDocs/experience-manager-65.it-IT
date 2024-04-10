---
title: Credenziali JWT nella console Adobe Developer obsolete
description: Informazioni sull’impatto della rimozione delle credenziali JWT in Adobe Developer Console su AEM
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# Credenziali JWT nella console Adobe Developer obsolete {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service deve fare riferimento a [questo articolo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) per ulteriori informazioni.

[Adobe Developer Console](https://developer.adobe.com/console) viene utilizzato per generare credenziali che consentano l’accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Uno di questi tipi di credenziali, le credenziali dell’account di servizio (JWT), è stato dichiarato obsoleto a favore delle credenziali da server a server OAuth. A partire dal 3 giugno 2024, non sarà possibile creare nuove credenziali dell’account di servizio (JWT) e, a partire dal 27 gennaio 2025, le credenziali JWT esistenti non funzioneranno. È possibile [consultare le informazioni sull’obsolescenza](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Questo articolo fornisce alcuni contesti aggiuntivi su come i clienti di AEM 6.5 devono gestire la rimozione.

In questo momento, l’aspetto principale è che le funzionalità AEM non supportano ancora le nuove credenziali da server a server OAuth. Il supporto sarà presto disponibile: entro la fine di aprile 2024 attraverso uno speciale pacchetto di compatibilità da installare per AEM 6.5, se si sta eseguendo il Service Pack 20 più recente o inferiore (Service Pack 21 e versioni successive lo includeranno automaticamente). È possibile che sia stata ricevuta un’e-mail con le istruzioni per la migrazione delle credenziali JWT, ma occorre tenere presente che è possibile e si dovrebbe rimandare la migrazione delle credenziali fino a quando AEM non supporterà il nuovo tipo di credenziali da server a server OAuth.

Le sezioni seguenti elencano gli scenari in cui i clienti devono (o in alcuni casi non devono) sostituire le credenziali dell’account di servizio (JWT) con le credenziali server-to-server OAuth, una volta che l’AEM li ha supportati a fine aprile. [Scopri come](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) sostituire le credenziali in futuro.

## Integrazione di AEM con altre soluzioni Adobe {#integrating-aem-with-other-adobe-solutions}

**Azione**: attendi di migrare fino a dopo la fine di aprile 2024, quando l’AEM lo supporterà.

**Versioni pertinenti dell’AEM**: Adobe Managed Services (Service Pack 20 e versioni successive).


L’interfaccia utente di authoring di AEM viene utilizzata per configurare le integrazioni con tutte le altre soluzioni Adobe. Ad esempio Adobe Target, Adobe Analytics, Adobe Launch, AFCS e molte altre.

![Integrazione di AEM con altre soluzioni](/help/sites-administering/assets/jwt-deprecation.png)

Ad esempio, ecco [le istruzioni](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=it) per configurare l’integrazione con Adobe Target. Chiave API in [Completamento della configurazione IMS in AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) deve essere migrata al tipo di credenziali server-to-server OAuth, una volta che l’AEM supporta tali credenziali alla fine di aprile. Le istruzioni verranno aggiornate e aggiornate alla fine di aprile per aiutarti ad applicare le nuove credenziali server-to-server OAuth.

## API di Cloud Manager {#cloud-manager-apis}

**Azione**: attendi di migrare fino a dopo la fine di aprile 2024, quando l’AEM lo supporterà.

**Versioni pertinenti dell’AEM**: Adobe Managed Services (Service Pack 20 e versioni successive).

I progetti Adobe Developer Console vengono creati in modo che possano richiamare le [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). È opportuno migrare le credenziali nel progetto Adobe Developer al tipo di credenziali da server a server OAuth, quando AEM e Cloud Manager ne forniranno il supporto.
