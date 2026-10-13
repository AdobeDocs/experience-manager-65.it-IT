---
title: Personalizzazione dei servizi dati per bozze e invii
description: Per impostazione predefinita, AEM Forms memorizza le bozze e i moduli adattivi inviati in un nodo predefinito sull’istanza Publish. Tuttavia, puoi configurare i servizi dati bozza e invio di AEM Forms per personalizzare l’archiviazione delle bozze e dei moduli adattivi inviati.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 5%
---
# Personalizzazione dei servizi dati per bozze e invii {#customizing-draft-and-submission-data-services}

## Panoramica {#overview}

AEM Forms consente agli utenti di salvare un modulo adattivo come bozza. La funzionalità bozza offre agli utenti la possibilità di gestire un modulo in corso di lavorazione. L’utente può quindi completare e inviare il modulo in qualsiasi momento da qualsiasi dispositivo.

Per impostazione predefinita, AEM Forms archivia i dati utente associati alla bozza e all&#39;invio nell&#39;istanza Publish nel nodo `/content/forms/fp`.

Tuttavia, i componenti del portale AEM Forms forniscono servizi di dati che ti consentono di personalizzare l’implementazione della memorizzazione dei dati utente per le bozze e gli invii. Ad esempio, puoi archiviare i dati in un archivio dati attualmente implementato nella tua organizzazione.

Per personalizzare l&#39;archiviazione dei dati utente, è necessario implementare i servizi [Dati bozza](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) e [Dati invio](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Prerequisiti {#prerequisites}

* Abilita [componenti di Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* Crea una [pagina portale Forms](/help/forms/using/creating-form-portal-page.md)
* Abilita [moduli adattivi per Forms Portal](/help/forms/using/draft-submission-component.md)
* Scopri [i dettagli di implementazione dell&#39;archiviazione personalizzata](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servizio dati bozza {#draft-data-service}

Per personalizzare l&#39;archiviazione dei dati delle bozze utente, è necessario fornire l&#39;implementazione per tutti i metodi dell&#39;interfaccia `DraftAFDataService`.

Nell&#39;esempio di codice seguente dell&#39;interfaccia viene fornita una descrizione dei metodi e dei relativi argomenti:

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") if there is update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## Servizio dati di invio {#submission-data-service}

Per personalizzare l&#39;archiviazione dei dati di invio degli utenti, è necessario fornire l&#39;implementazione per tutti i metodi dell&#39;interfaccia `SubmittedAFDataService`.

Nell&#39;esempio di codice seguente dell&#39;interfaccia viene fornita una descrizione dei metodi e dei relativi argomenti:

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```
