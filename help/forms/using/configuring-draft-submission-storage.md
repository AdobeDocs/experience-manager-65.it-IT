---
title: Configurazione dei servizi di archiviazione per le bozze e gli invii
description: Scopri come configurare l’archiviazione per le bozze e gli invii
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Configurazione dei servizi di archiviazione per le bozze e gli invii {#configuring-storage-services-for-drafts-and-submissions}

## Panoramica {#overview}

Con AEM Forms puoi archiviare:

* **Bozze**: modulo work-in-progress che gli utenti finali compilano e salvano per un momento successivo e inviano successivamente.

* **Invii**: moduli inviati contenenti i dati forniti dall’utente.

I servizi di metadati e dati del portale AEM Forms forniscono supporto per bozze e invii. Per impostazione predefinita, i dati vengono memorizzati nell’istanza Publish, che viene quindi replicata all’inverso nell’istanza Autore configurata per essere disponibile per la percolazione ad altre istanze Publish.

Il problema dell’approccio preconfigurato è che memorizza tutti i dati sull’istanza Publish, compresi quelli che possono essere informazioni personali identificabili (PII, Personal Identifiable Information).

Oltre all’approccio predefinito sopra indicato, è disponibile un’implementazione alternativa per inviare direttamente i dati del modulo all’elaborazione invece di salvarli localmente. I clienti che hanno dubbi sull’archiviazione di dati potenzialmente sensibili nell’istanza di pubblicazione possono scegliere l’implementazione alternativa in cui i dati vengono inviati a un server di elaborazione. Poiché l’elaborazione viene eseguita sull’istanza di authoring, in genere rimane in un’area protetta.

>[!NOTE]
>
>Quando si utilizza l’azione di invio Forms Portal o si abilita l’opzione Memorizza dati nel portale dei moduli in un modulo adattivo, i dati del modulo vengono memorizzati nell’archivio AEM. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati nell’archivio AEM. Per memorizzare le bozze e i dati dei moduli inviati, è necessario integrare il componente bozze e invio con un archivio sicuro come il database aziendale.
>
>Per ulteriori informazioni, consulta [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

## Configurazione delle bozze e dei servizi di invio di Forms Portal {#configuring-forms-portal-drafts-and-submissions-services}

Nella configurazione della console web dell’AEM ( `https://[host]:'port'/system/console/configMgr`), fai clic per aprire **Configurazione bozza e invio portale Forms** in modalità di modifica.

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
   <td>Forms Portal Draft Data Service(Identificatore per bozza di servizio dati (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati bozza del portale Forms (identificatore per il servizio metadati bozza (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio dati di invio portale Forms (identificatore per il servizio dati di invio (<strong>submit.data.service</strong>))</td>
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
   <td>Forms Portal Draft Data Service(Identificatore per bozza di servizio dati (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati bozza del portale Forms (identificatore per il servizio metadati bozza (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio dati di invio portale Forms (identificatore per il servizio dati di invio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio metadati invio portale Forms (identificatore per il servizio metadati invio (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Oltre alla configurazione specificata in precedenza, fornire informazioni sull’istanza di elaborazione remota configurata.

Nella configurazione della console web dell’AEM ( `https://[host]:'port'/system/console/configMgr`), fai clic per aprire **Servizio impostazioni DS AEM** in modalità di modifica. Nella finestra di dialogo Servizio impostazioni DS AEM, fornire informazioni sull&#39;elaborazione dell&#39;URL del server, del nome utente del server di elaborazione e della password.

>[!NOTE]
>
>Viene inoltre fornito un esempio di implementazione per l’archiviazione dei dati utente in un database. Per informazioni su come configurare i servizi dati e metadati per memorizzare i dati utente in un database esterno, vedere [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).
