---
title: Rendering del modello di modulo per i moduli HTML5
seo-title: Rendering del modello di modulo per i moduli HTML5
description: I profili dei moduli HTML5 sono associati ai rendering dei profili. I rendering dei profili sono pagine JSP responsabili della generazione della rappresentazione HTML del modulo mediante il servizio Forms OSGi.
seo-description: I profili dei moduli HTML5 sono associati ai rendering dei profili. I rendering dei profili sono pagine JSP responsabili della generazione della rappresentazione HTML del modulo mediante il servizio Forms OSGi.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---


# Rendering del modello di modulo per i moduli HTML5 {#rendering-form-template-for-html-forms}

## Endpoint di rendering {#render-endpoint}

I moduli HTML5 hanno il concetto di **Profili** esposti come endpoint REST per abilitare il rendering mobile dei modelli di modulo. Tali profili hanno associato **Modulo di rendering profili**. Sono pagine JSP responsabili della generazione della rappresentazione HTML del modulo mediante il servizio Forms OSGi. Il percorso JCR del nodo Profilo determina l’URL del punto finale di rendering. Il punto finale di rendering predefinito del modulo che punta al profilo &#39;predefinito&#39; è simile al seguente:

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*percorso della cartella contenente il nome xdp*>&amp;template=&lt;*nome dell&#39;xdp*>

Esempio, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Per un profilo personalizzato, l&#39;endpoint cambia di conseguenza. Ad esempio, il punto finale per il profilo personalizzato con le maschere del nome è:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Se il modello risiede nell&#39;archivio AEM in un&#39;applicazione denominata FormSubmission, l&#39;URI è:

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
   <td>template<br /> </td>
   <td>Questo parametro specifica il nome del file modello.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Questo parametro specifica il percorso in cui risiedono il modello e le risorse associate. Questo percorso può essere il percorso del file system del server o un percorso del repository oppure http o un percorso ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Questo parametro specifica l'URL al quale viene inviato il codice xml dei dati del modulo.<br /> </td>
  </tr>
 </tbody>
</table>

### Unisci dati con modello di modulo {#merge-data-with-form-template}

| Parametro | Descrizione |
|---|---|
| dataRef | Questo parametro specifica **percorso assoluto** del file di dati unito al modello. Questo parametro può essere un URL di un servizio di supporto che restituisce i dati in formato xml. |
| data | Questo parametro specifica i byte di dati codificati UTF-8 uniti al modello. Se questo parametro viene specificato, il modulo HTML5 ignora il parametro dataRef. |

### Passaggio del parametro di rendering {#passing-the-render-parameter}

I moduli HTML5 supportano tre metodi per passare i parametri di rendering. Puoi trasmettere i parametri tramite URL, coppie chiave-valore e nodo profilo. Nel parametro di rendering, la coppia chiave-valore ha la precedenza più alta seguita dal nodo del profilo. Il parametro Richiesta URL ha la precedenza minore.

* **Parametri** di richiesta URL: Potete specificare i parametri di rendering nell’URL. Nei parametri della richiesta URL, i parametri sono visibili all’utente finale. Ad esempio, il seguente URL di invio contiene il parametro di modello nell’URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parametri** della richiesta SetAttribute: Potete specificare i parametri di rendering come coppia chiave-valore. Nei parametri della richiesta SetAttribute, i parametri non sono visibili all&#39;utente finale. È possibile inoltrare una richiesta da qualsiasi altro JSP a JSP per il rendering del profilo di modulo HTML5 e utilizzare *setAttribute* su un oggetto di richiesta per trasmettere tutti i parametri di rendering. Questo metodo ha la precedenza più alta.

* **Parametri della richiesta del nodo del profilo:** puoi specificare i parametri di rendering come proprietà del nodo di un nodo del profilo. Nei parametri di richiesta del nodo del profilo, i parametri non sono visibili all&#39;utente finale. Il nodo del profilo è il nodo in cui viene inviata la richiesta. Per specificare i parametri come proprietà del nodo, utilizzare CRXDE lite.

### Invia parametri {#submit-parameters}

I moduli HTML5 inviano dati; eseguire script sul lato server e servizi Web sui server AEM. Per informazioni dettagliate sui parametri utilizzati per eseguire script sul lato server e servizi Web sui server AEM, vedere [HTML5 forms Service Proxy](/help/forms/using/service-proxy.md).
