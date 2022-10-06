---
title: API per l’utilizzo dei moduli inviati nel portale moduli
seo-title: APIs to work with submitted forms on forms portal
description: AEM Forms fornisce API che è possibile utilizzare per eseguire query e azioni sui dati dei moduli inviati nel portale dei moduli.
seo-description: AEM Forms provides APIs that you can use to query and take actions on submitted forms data in forms portal.
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
feature: Forms Portal
exl-id: a685889e-5d24-471c-926d-dbb096792bc8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 9%

---

# API per l’utilizzo dei moduli inviati nel portale moduli {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms fornisce API che è possibile utilizzare per eseguire query sui dati dei moduli inviati tramite il portale dei moduli. Inoltre, è possibile pubblicare commenti o aggiornare le proprietà dei moduli inviati utilizzando le API illustrate in questo documento.

>[!NOTE]
>
>Gli utenti che richiameranno le API devono essere aggiunti al gruppo di revisori come descritto in [Associazione dei revisori per l’invio a un modulo](/help/forms/using/adding-reviewers-form.md).

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

Restituisce un elenco di tutti i moduli idonei.

### Parametri URL {#url-parameters}

Questa API non richiede parametri aggiuntivi.

### Risposta {#response}

L&#39;oggetto response contiene un array JSON che include i nomi dei moduli e il relativo percorso di archivio. La struttura della risposta è la seguente:

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### Esempio {#example}

**URL richiesta**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**Risposta**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubmission {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

Restituisce i dettagli di tutti i moduli inviati. Tuttavia, puoi utilizzare i parametri URL per limitare i risultati.

### Parametri URL {#url-parameters-1}

Specifica i seguenti parametri nell’URL della richiesta:

<table>
 <tbody>
  <tr>
   <th>Parametro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>Specifica il percorso del repository CRX in cui si trova il modulo. Se non si specifica il percorso del modulo, viene restituita una risposta vuota.<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> (facoltativo)</td>
   <td>Specifica il punto iniziale nell'indice del set di risultati. Il valore predefinito è <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code> (facoltativo)</td>
   <td>Limita il numero di risultati. Il valore predefinito è <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (facoltativo)</td>
   <td>Specifica la proprietà per l'ordinamento dei risultati. Il valore predefinito è <strong>jcr:lastModified</strong>, che ordina i risultati in base all’ora dell’ultima modifica.</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (facoltativo)</td>
   <td>Specifica l'ordine dei risultati dell'ordinamento. Il valore predefinito è <strong>desc</strong>, che determina un ordine decrescente. Puoi specificare <code>asc</code> per ordinare i risultati in ordine crescente.</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (facoltativo)</td>
   <td>Specifica un elenco di proprietà del modulo separate da virgola da includere nei risultati. Le proprietà predefinite sono:<br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (facoltativo)</td>
   <td>Cerca il valore specificato nelle proprietà del modulo e restituisce moduli con valori corrispondenti. Il valore predefinito è <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### Risposta {#response-1}

L&#39;oggetto response contiene un array JSON che include i dettagli dei moduli specificati. La struttura della risposta è la seguente:

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### Esempio {#example-1}

**URL richiesta**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**Risposta**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

Aggiunge un commento all’istanza di invio specificata.

### Parametri URL {#url-parameters-2}

Specifica i seguenti parametri nell’URL della richiesta:

| Parametro | Descrizione |
|---|---|
| `submitID` | Specifica l&#39;ID metadati associato a un&#39;istanza di invio. |
| `Comment` | Specifica il testo da aggiungere al commento all&#39;istanza di invio specificata. |

### Risposta {#response-2}

Restituisce un ID commento in caso di pubblicazione corretta di un commento.

### Esempio {#example-2}

**URL richiesta**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**Risposta**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments   {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

Restituisce tutti i commenti inviati nell&#39;istanza di invio specificata.

### Parametri URL {#url-parameters-3}

Specifica il seguente parametro nell’URL della richiesta:

| Parametro | Descrizione |
|---|---|
| `submitID` | Specifica l&#39;ID metadati di un&#39;istanza di invio. |

### Risposta {#response-3}

L&#39;oggetto response contiene una matrice JSON che include tutti i commenti associati all&#39;ID di invio specificato. La struttura della risposta è la seguente:

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### Esempio {#example-3}

**URL richiesta**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**Risposta**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

Aggiorna il valore della proprietà specificata dell&#39;istanza di modulo inviata specificata.

### Parametri URL {#url-parameters-4}

Specifica i seguenti parametri nell’URL della richiesta:

| Parametro | Descrizione |
|---|---|
| `submitID` | Specifica l&#39;ID metadati associato a un&#39;istanza di invio. |
| `property` | Specifica la proprietà della maschera da aggiornare. |
| `value` | Specifica il valore della proprietà modulo da aggiornare. |

### Risposta {#response-4}

Restituisce un oggetto JSON con informazioni sull&#39;aggiornamento registrato.

### Esempio {#example-4}

**URL richiesta**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**Risposta**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```
