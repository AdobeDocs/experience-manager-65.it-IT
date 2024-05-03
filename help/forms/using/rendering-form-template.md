---
title: Rendering del modello di modulo per i moduli HTML5
description: I profili HTML5 forms sono associati ai rendering dei profili. I rendering profili sono pagine JSP responsabili della generazione della rappresentazione HTML del modulo chiamando il servizio OSGi di Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Rendering del modello di modulo per i moduli HTML5 {#rendering-form-template-for-html-forms}

## Endpoint di rendering {#render-endpoint}

I moduli HTML5 hanno il concetto di **Profili** che sono esposti come endpoint REST per abilitare il rendering mobile dei modelli di modulo. Questi profili hanno associato **Rendering profilo**. Si tratta di pagine JSP responsabili della generazione della rappresentazione HTML del modulo chiamando il servizio Forms OSGi. Il percorso JCR del nodo Profilo determina l’URL dell’endpoint di rendering. Il punto finale predefinito del rendering del modulo che punta al profilo &quot;predefinito&quot; è simile al seguente:

https://&lt;*host*>:&lt;*porta*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*percorso della cartella contenente il modulo xdp*>&amp;template=&lt;*nome dell’xdp*>

Ad esempio `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Per un profilo personalizzato, l’endpoint cambia di conseguenza. Ad esempio, il punto finale del profilo personalizzato con il nome hrforms è:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Se il modello risiede nell’archivio AEM in un’applicazione denominata FormSubmission, l’URI è:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parametri di rendering {#render-parameters}

I parametri di richiesta supportati durante il rendering del modulo come HTML sono:

<table>
 <tbody>
  <tr>
   <th><strong>Parametro </strong></th>
   <th><strong>Descrizione</strong></th>
  </tr>
  <tr>
   <td>modello<br /> </td>
   <td>Questo parametro specifica il nome del file modello.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Questo parametro specifica il percorso in cui risiedono il modello e le risorse associate. Questo percorso può essere il percorso del file system del server, un percorso dell’archivio o http o un percorso ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Questo parametro specifica l'URL in cui viene pubblicato l'xml dei dati del modulo.<br /> </td>
  </tr>
 </tbody>
</table>

### Unione di dati con modello di modulo {#merge-data-with-form-template}

| Parametro | Descrizione |
|---|---|
| dataRef | Questo parametro specifica **percorso assoluto** del file di dati unito al modello. Questo parametro può essere un URL di un servizio rest che restituisce i dati in formato xml. |
| dati | Questo parametro specifica i byte di dati con codifica UTF-8 che vengono uniti al modello. Se si specifica questo parametro, il modulo HTML5 ignora il parametro dataRef. |

### Trasmissione del parametro di rendering {#passing-the-render-parameter}

I moduli HTML5 supportano tre metodi per il passaggio dei parametri di rendering. Puoi trasmettere parametri tramite URL, coppie chiave-valore e nodo di profilo. Nel parametro di rendering, la coppia chiave-valore ha la precedenza massima seguita dal nodo di profilo. Il parametro di richiesta URL ha la precedenza minore.

* **Parametri di richiesta URL**: puoi specificare i parametri di rendering nell’URL. Nei parametri di richiesta dell’URL, i parametri sono visibili all’utente finale. Ad esempio, il seguente URL di invio contiene il parametro di modello nell’URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parametri della richiesta SetAttribute**: puoi specificare i parametri di rendering come coppia chiave-valore. Nei parametri della richiesta SetAttribute, i parametri non sono visibili all&#39;utente finale. Puoi inoltrare una richiesta da qualsiasi altra JSP al modulo di rendering dei profili HTML5 JSP e utilizzare *setAttribute* su richiesta per passare tutti i parametri di rendering. Questo metodo ha la precedenza più alta.

* **Parametri di richiesta nodo profilo:** Puoi specificare i parametri di rendering come proprietà del nodo di un nodo di profilo. Nei parametri di richiesta del nodo del profilo, i parametri non sono visibili all’utente finale. Il nodo del profilo è il nodo in cui viene inviata la richiesta. Per specificare i parametri come proprietà del nodo, utilizzate CRXDE lite.

### Invia parametri {#submit-parameters}

I moduli HTML5 inviano dati; eseguono script e servizi web lato server sui server AEM. Per informazioni dettagliate sui parametri utilizzati per eseguire script e servizi Web lato server sui server AEM, vedi [Proxy servizio HTML5 Forms](/help/forms/using/service-proxy.md).
