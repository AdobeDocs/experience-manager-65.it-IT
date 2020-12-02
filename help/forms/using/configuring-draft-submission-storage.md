---
title: Configurazione dei servizi di archiviazione per bozze e invii
seo-title: Configurazione dei servizi di archiviazione per bozze e invii
description: Scoprite come configurare l'archiviazione per bozze e invii
seo-description: Scoprite come configurare l'archiviazione per bozze e invii
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---


# Configurazione dei servizi di archiviazione per bozze e invii {#configuring-storage-services-for-drafts-and-submissions}

## Panoramica {#overview}

Con  AEM Forms, potete memorizzare:

* **Bozze**: Modulo di lavoro in corso che gli utenti finali compilano e salvano per un secondo momento e che inviano successivamente.

* **Invii**: Moduli inviati contenenti i dati forniti dall&#39;utente.

 i servizi dati e metadati di AEM Forms Portal supportano le bozze e gli invii. Per impostazione predefinita, i dati vengono memorizzati nell’istanza di pubblicazione, che viene quindi replicata all’inverso nell’istanza di creazione configurata per essere disponibile per l’analisi ad altre istanze di pubblicazione.

Il problema con l&#39;attuale approccio out-of-the-box è che memorizza tutti i dati sull&#39;istanza pubblicata, compresi i dati che possono essere Dati personali (PII).

Oltre al suddetto approccio predefinito, è disponibile un&#39;implementazione alternativa per spostare direttamente i dati del modulo all&#39;elaborazione, anziché salvarli localmente. I clienti che nutrono dubbi sulla memorizzazione di dati potenzialmente sensibili nell’istanza di pubblicazione possono scegliere l’implementazione alternativa in cui i dati vengono inviati a un server di elaborazione. Poiché l’elaborazione viene eseguita sull’istanza di creazione, in genere rimane in un’area protetta.

>[!NOTE]
>
>Se si utilizza l&#39;azione di invio di Forms Portal o si abilita l&#39;opzione Archivia dati nel portale moduli in un modulo adattivo, i dati del modulo vengono memorizzati AEM archivio. In un ambiente di produzione, si consiglia di non memorizzare i dati delle bozze o dei moduli inviati AEM repository. Al contrario, è necessario integrare le bozze e il componente di invio con un archivio protetto come il database aziendale per memorizzare le bozze e i dati dei moduli inviati.
>
>Per ulteriori informazioni, vedere [Esempio per l&#39;integrazione del componente per bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

## Configurazione dei servizi di bozza e di invio di Forms Portal {#configuring-forms-portal-drafts-and-submissions-services}

Nella AEM Configurazione console Web ( `https://[host]:'port'/system/console/configMgr`), fare clic per aprire **Forms Portal Draft and Submission Configuration** in modalità di modifica.

Specificate i valori per le proprietà in base ai vostri requisiti come descritto di seguito:

### I servizi forniti per memorizzare i dati nell&#39;istanza di pubblicazione {#out-of-the-box-services-to-store-data-on-publish-instance}

I dati vengono replicati in modo inverso nell’istanza di creazione configurata.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>Servizio dati bozza di Forms Portal (identificatore per il servizio dati bozza (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di metadati bozza di Forms Portal (identificatore per il servizio di metadati bozza (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio dati di invio Forms Portal (identificatore per il servizio dati di invio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di invio metadati Forms Portal (identificatore per l'invio del servizio di metadati (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Servizi forniti per la memorizzazione dei dati nell&#39;istanza di elaborazione remota {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

I dati vengono inviati direttamente all&#39;istanza remota configurata

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>Servizio dati bozza di Forms Portal (identificatore per il servizio dati bozza (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di metadati bozza di Forms Portal (identificatore per il servizio di metadati bozza (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio dati di invio Forms Portal (identificatore per il servizio dati di invio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servizio di invio metadati Forms Portal (identificatore per l'invio del servizio di metadati (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Oltre alla configurazione specificata in precedenza, fornisci informazioni sull&#39;istanza di elaborazione remota configurata.

In Configurazione console Web AEM ( `https://[host]:'port'/system/console/configMgr`), fare clic per aprire **AEM Servizi impostazioni DS** in modalità di modifica. Nella finestra di dialogo Servizio impostazioni DS AEM, fornire informazioni sull&#39;URL del server di elaborazione, il nome utente e la password del server di elaborazione.

>[!NOTE]
>
>Viene inoltre fornita un&#39;implementazione di esempio per la memorizzazione dei dati utente in un database. Per informazioni su come configurare i servizi dati e metadati per la memorizzazione dei dati utente in un database esterno, vedere [Esempio per l&#39;integrazione di bozze e invii di componenti con database](/help/forms/using/integrate-draft-submission-database.md).

