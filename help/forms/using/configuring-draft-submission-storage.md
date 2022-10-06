---
title: Configurazione dei servizi di archiviazione per bozze e invii
seo-title: Configuring storage services for drafts and submissions
description: Scopri come configurare lo storage per bozze e invii
seo-description: Learn how to configure storage for drafts and submissions
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Configurazione dei servizi di archiviazione per bozze e invii {#configuring-storage-services-for-drafts-and-submissions}

## Panoramica {#overview}

Con AEM Forms puoi archiviare:

* **Bozze**: Modulo in corso di lavorazione che gli utenti finali compilano e salvano per un momento successivo e inviano successivamente.

* **Invii**: Moduli inviati contenenti i dati forniti dall’utente.

I servizi di dati e metadati del portale AEM Forms supportano bozze e invii. Per impostazione predefinita, i dati vengono memorizzati nell’istanza di pubblicazione, che viene quindi replicata all’inverso nell’istanza di authoring configurata per essere disponibile per l’esecuzione ad altre istanze di pubblicazione.

Il problema con l’approccio preconfigurato esistente è che memorizza tutti i dati sull’istanza di pubblicazione, inclusi i dati che possono essere PII (Personal Identifiable Information).

Oltre all’approccio predefinito di cui sopra, è disponibile anche un’implementazione alternativa per spingere direttamente i dati del modulo all’elaborazione anziché salvarli localmente. I clienti che nutrono dubbi sull’archiviazione di dati potenzialmente sensibili nell’istanza di pubblicazione possono scegliere l’implementazione alternativa in cui i dati vengono inviati a un server di elaborazione. Poiché l’elaborazione viene eseguita sull’istanza di authoring, in genere rimane in un’area protetta.

>[!NOTE]
>
>Quando si utilizza l’azione Invia di Forms Portal o si abilita l’opzione Archivia dati in forms portal in forma adattiva, i dati del modulo vengono memorizzati AEM archivio. In un ambiente di produzione, si consiglia di non archiviare le bozze o i dati del modulo inviati in AEM archivio. Per memorizzare le bozze e i dati dei moduli inviati, è invece necessario integrare le bozze e il componente di invio con un archivio protetto, ad esempio un database aziendale.
>
>Per ulteriori informazioni, consulta [Esempio per l&#39;integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

## Configurazione di progetti e servizi di invio del portale Forms {#configuring-forms-portal-drafts-and-submissions-services}

Nella configurazione della console Web AEM ( `https://[host]:'port'/system/console/configMgr`), fai clic per aprire **Configurazione bozza e invio del portale Forms** in modalità di modifica.

Specifica i valori delle proprietà in base ai requisiti come descritto di seguito:

### Servizi preconfigurati per archiviare dati nell’istanza di pubblicazione {#out-of-the-box-services-to-store-data-on-publish-instance}

I dati vengono replicati inversamente nell’istanza di authoring configurata.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>Servizio dati bozza di Forms Portal (identificatore del servizio dati bozza) (<strong>draft.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati bozza di Forms Portal (identificatore del servizio di metadati bozza) (<strong>draft.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di invio dati di Forms Portal (identificatore del servizio di invio dati) (<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di invio dei metadati (identificatore del servizio di invio dei metadati) di Forms Portal<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Servizi preconfigurati per archiviare dati in un’istanza di elaborazione remota {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

I dati vengono inviati direttamente all’istanza remota configurata

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>Servizio dati bozza di Forms Portal (identificatore del servizio dati bozza) (<strong>draft.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati bozza di Forms Portal (identificatore del servizio di metadati bozza) (<strong>draft.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di invio dati di Forms Portal (identificatore del servizio di invio dati) (<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di invio dei metadati (identificatore del servizio di invio dei metadati) di Forms Portal<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Oltre alla configurazione specificata sopra, fornisci informazioni sull&#39;istanza di elaborazione remota configurata.

Nella configurazione della console Web AEM ( `https://[host]:'port'/system/console/configMgr`), fai clic per aprire **Servizio impostazioni di DS AEM** in modalità di modifica. Nella finestra di dialogo Servizio impostazioni DS AEM, fornire informazioni sull&#39;URL del server di elaborazione, il nome utente del server di elaborazione e la password.

>[!NOTE]
>
>Viene inoltre fornita un’implementazione di esempio per la memorizzazione dei dati utente in un database. Per informazioni su come configurare i servizi dati e metadati per memorizzare i dati utente in un database esterno, consulta [Esempio per l&#39;integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).
