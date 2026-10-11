---
title: Configurazione dei servizi di archiviazione per le bozze e gli invii
description: Scopri come configurare l’archiviazione per le bozze e gli invii
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: fa155e29-cba2-5e77-9efd-4824be5ce4c8
    internal-label: Forms Portal
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%
---
# Configurazione dei servizi di archiviazione per le bozze e gli invii {#configuring-storage-services-for-drafts-and-submissions}

## Panoramica {#overview}

Con AEM Forms puoi archiviare:

* **Bozze**: modulo work-in-progress che gli utenti finali compileranno e salveranno per un momento successivo e invieranno successivamente.

* **Invii**: moduli inviati contenenti i dati forniti dall&#39;utente.

I servizi di metadati e dati del portale AEM Forms forniscono supporto per bozze e invii. Per impostazione predefinita, i dati vengono memorizzati nell’istanza Publish, che viene quindi replicata all’inverso nell’istanza Autore configurata per essere disponibile per la percolazione ad altre istanze Publish.

Il problema dell’approccio preconfigurato è che memorizza tutti i dati sull’istanza Publish, compresi quelli che possono essere informazioni personali identificabili (PII, Personal Identifiable Information).

Oltre all’approccio predefinito sopra indicato, è disponibile un’implementazione alternativa per inviare direttamente i dati del modulo all’elaborazione invece di salvarli localmente. I clienti che hanno dubbi sull’archiviazione di dati potenzialmente sensibili nell’istanza di pubblicazione possono scegliere l’implementazione alternativa in cui i dati vengono inviati a un server di elaborazione. Poiché l’elaborazione viene eseguita sull’istanza di authoring, in genere rimane in un’area protetta.

>[!NOTE]
>
>Quando si utilizza l’azione di invio Forms Portal o si abilita l’opzione Memorizza dati nel portale dei moduli in un modulo adattivo, i dati del modulo vengono memorizzati nell’archivio di AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati nell’archivio di AEM. Per memorizzare le bozze e i dati dei moduli inviati, è necessario integrare il componente bozze e invio con un archivio sicuro come il database aziendale.
>
>Per ulteriori informazioni, vedere [Esempio per l&#39;integrazione del componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

## Configurazione delle bozze e dei servizi di invio di Forms Portal {#configuring-forms-portal-drafts-and-submissions-services}

Nella configurazione della console Web di AEM ( `https://[host]:'port'/system/console/configMgr`), fare clic per aprire **Configurazione bozza e invio portale Forms** in modalità di modifica.

Specifica i valori per le proprietà in base ai requisiti come descritto di seguito:

### Servizi predefiniti per l’archiviazione dei dati nell’istanza di pubblicazione {#out-of-the-box-services-to-store-data-on-publish-instance}

I dati vengono replicati in modo inverso nell’istanza di authoring configurata.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>Servizio dati bozza portale Forms(Identificatore per servizio dati bozza (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati bozza portale Forms (identificatore per il servizio metadati bozza (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio dati invio portale Forms (identificatore per il servizio dati invio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati invio portale Forms (identificatore per il servizio metadati invio (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Servizi predefiniti per l’archiviazione dei dati nell’istanza di elaborazione remota {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

I dati vengono inviati direttamente all’istanza remota configurata

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>Servizio dati bozza portale Forms(Identificatore per servizio dati bozza (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati bozza portale Forms (identificatore per il servizio metadati bozza (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio dati invio portale Forms (identificatore per il servizio dati invio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati invio portale Forms (identificatore per il servizio metadati invio (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Oltre alla configurazione specificata in precedenza, fornire informazioni sull’istanza di elaborazione remota configurata.

Nella configurazione della console Web di AEM ( `https://[host]:'port'/system/console/configMgr`), fare clic per aprire **Servizio impostazioni di AEM DS** in modalità di modifica. Nella finestra di dialogo Servizio impostazioni di AEM DS fornire informazioni sull&#39;elaborazione dell&#39;URL del server, del nome utente del server di elaborazione e della password.

>[!NOTE]
>
>Viene inoltre fornito un esempio di implementazione per l’archiviazione dei dati utente in un database. Per informazioni su come configurare i servizi dati e metadati per memorizzare i dati utente in un database esterno, vedere [Esempio per l&#39;integrazione del componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).
