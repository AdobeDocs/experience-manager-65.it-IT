---
title: Memorizzazione personalizzata per il componente bozze e invii
seo-title: Memorizzazione personalizzata per il componente bozze e invii
description: Scopri come personalizzare l’archiviazione dei dati utente per bozze e invii.
seo-description: Scopri come personalizzare l’archiviazione dei dati utente per bozze e invii.
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Memorizzazione personalizzata per il componente bozze e invii {#custom-storage-for-drafts-and-submissions-component}

## Panoramica {#overview}

 AEM Forms consente di salvare un modulo come bozza. La funzionalità bozza consente di mantenere un modulo di lavoro in corso, che può essere completato e inviato in un secondo momento da qualsiasi dispositivo.

Per impostazione predefinita,  AEM Forms memorizza i dati utente associati alla bozza e all&#39;invio di un modulo nel nodo `/content/forms/fp` nell&#39;istanza Pubblica. Inoltre, i componenti del  portale AEM Forms forniscono servizi dati che consentono di personalizzare l&#39;implementazione dell&#39;archiviazione dei dati utente per bozze e invii. Ad esempio, è possibile memorizzare i dati utente in un archivio dati.

## Prerequisiti  {#prerequisites}

* Abilita [componenti del portale moduli](/help/forms/using/enabling-forms-portal-components.md)
* Creare una pagina del portale dei moduli [](/help/forms/using/creating-form-portal-page.md)
* Abilitare i [moduli adattivi per il portale dei moduli](/help/forms/using/draft-submission-component.md)
* Informazioni [sull&#39;implementazione di storage personalizzato](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servizio dati bozza {#draft-data-service}

Per personalizzare l&#39;archiviazione dei dati utente per le bozze, è necessario implementare tutti i metodi dell&#39;interfaccia `DraftDataService`. Il codice di esempio seguente descrive metodi e argomenti.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>Il valore minimo per la lunghezza del campo ID bozza è 26 caratteri.  Adobe consiglia di impostare la lunghezza dell&#39;ID bozza su 26 o più caratteri.

## Servizio dati invio {#submission-data-service}

Per personalizzare la memorizzazione dei dati utente per gli invii, è necessario implementare tutti i metodi dell&#39;interfaccia `SubmitDataService`. Il codice di esempio seguente descrive metodi e argomenti.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Il portale Forms utilizza il concetto di identificatore univoco universale (UUID) per generare un ID univoco per ogni bozza e modulo inviato. Puoi anche generare un ID univoco personalizzato. È possibile implementare l’interfaccia FPKeyGeneratorService, ignorarne i metodi e sviluppare una logica personalizzata per generare un ID univoco personalizzato per ogni bozza e modulo inviato. Inoltre, imposta il livello di servizio per l’implementazione di generazione ID personalizzata maggiore di 0. Essa garantisce che venga utilizzata l&#39;implementazione personalizzata invece dell&#39;implementazione predefinita.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Puoi usare l’annotazione seguente per aumentare la classificazione del servizio per l’ID personalizzato generato con il codice precedente:

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Per utilizzare la nota di cui sopra, importa quanto segue nel progetto:

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```

