---
title: Rendering e distribuzione
seo-title: Rendering e distribuzione
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b

---


# Rendering e distribuzione{#rendering-and-delivery}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Il rendering del contenuto AEM può essere facilmente eseguito tramite i servlet [predefiniti](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) Sling per eseguire il rendering di [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) e altri formati.

Tali rendering out-of-the-box generalmente passano alla directory archivio e restituiscono il contenuto così com&#39;è.

AEM, tramite Sling, supporta anche lo sviluppo e la distribuzione di renderer di sling personalizzati per acquisire il controllo completo dello schema e del contenuto renderizzati.

I renderer predefiniti di Content Services colmano il divario tra i predefiniti Sling e lo sviluppo personalizzato out-of-the-box, consentendo la personalizzazione e il controllo di molti aspetti del contenuto di cui è stato effettuato il rendering senza necessità di sviluppo.

Nel diagramma seguente è illustrato il rendering dei servizi di contenuto.

![chlimage_1-15](assets/chlimage_1-15.png)

## Richiesta JSON {#requesting-json}

Usa **&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** per richiedere JSON.

<table>
 <tbody>
  <tr>
   <td>RISORSA</td>
   <td>una risorsa di entità in /content/entities<br /> o <br /> una risorsa di contenuto in /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>FACOLTATIVO</strong><br /> </p> <p>una configurazione di esportazione trovata in /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /><br /> Se omesso, verrà applicata la configurazione di esportazione predefinita </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>ricorsività di profondità FACOLTIONAL</strong><br /> <br /> per il rendering di elementi figlio come utilizzato nel rendering Sling</td>
  </tr>
 </tbody>
</table>

## Creazione di configurazioni di esportazione {#creating-export-configs}

Potete creare configurazioni di esportazione per personalizzare il rendering JSON.

Potete creare un nodo di configurazione in */apps/mobileapps/caas/exportConfigs.*

| Nome nodo | Nome della configurazione (per il selettore di rendering) |
|---|---|
| jcr:primaryType | nt:unstructured |

La tabella seguente mostra le proprietà di Export Configs:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predefinito (if, not set)</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Stringa[]</td>
   <td>include tutto</td>
   <td>sling:resourceType</td>
   <td>escludere dettagli per i nodi con sling:resourceType specificato dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Stringa[]</td>
   <td>exclude nulla</td>
   <td>sling:resourceType</td>
   <td>includere solo i dettagli per i nodi con sling:resourceType specificato dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Stringa[]</td>
   <td>exclude nulla</td>
   <td>Prefissi di proprietà</td>
   <td>escludere le proprietà che iniziano con i prefissi specificati dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Stringa[]</td>
   <td>exclude nulla</td>
   <td>Nomi proprietà</td>
   <td>escludere proprietà specificate dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Stringa[]</td>
   <td>include tutto</td>
   <td>Nomi proprietà</td>
   <td><p>se excludePropertyPrefixes impostato<br /> include proprietà specificate nonostante la corrispondenza del prefisso sia esclusa,</p> <p>else (le proprietà di esclusione vengono ignorate) includono solo queste proprietà</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Stringa[]</td>
   <td>include tutto</td>
   <td>nomi figlio</td>
   <td>escludere elementi figlio specificati dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Stringa[]<br /> <br /> </td>
   <td>exclude nulla</td>
   <td>nomi figlio</td>
   <td>includi solo elementi figlio specificati dall’esportazione JSON, escludi altri</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Stringa[]<br /> <br /> </td>
   <td>rename nothing</td>
   <td>&lt;nome_proprietà_effettiva&gt;,&lt;nome_proprietà_sostitutivo&gt;</td>
   <td>rinominare le proprietà utilizzando le sostituzioni</td>
  </tr>
 </tbody>
</table>

### Sovrapposizioni per l&#39;esportazione del tipo di risorsa {#resource-type-export-overrides}

Create un nodo di configurazione in */apps/mobileapps/caas/exportConfigs.*

| nome | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

Nella tabella seguente sono riportate le proprietà:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predefinito (if, not set)</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>Stringa[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Per i seguenti tipi di risorse di sling, non restituire l'esportazione predefinita CaaS json.<br /> Restituire l’esportazione di un singolo cliente eseguendo il rendering della risorsa come;<br /> &lt;RESOURCE&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurazioni di esportazione di Content Services esistenti {#existing-content-services-export-configs}

Content Services include due configurazioni di esportazione:

* default (nessuna configurazione specificata)
* page (per eseguire il rendering delle pagine del sito)

#### Configurazione esportazione predefinita {#default-export-configuration}

Se nell&#39;URI richiesto è specificata una configurazione, verrà applicata la configurazione di esportazione predefinita di Content Services.

&lt;RESOURCE>.caas[.&lt;DEPTH-INT>].json

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,quercia:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sovrapposizioni JSON Sling</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapp/caas/components/data/contentRiferimento<br /> mobileapp/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configurazione esportazione pagina {#page-export-configuration}

Questa configurazione estende l&#39;impostazione predefinita per includere il raggruppamento di elementi secondari sotto un nodo figlio.

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### Additional Resources {#additional-resources}

Consultate le risorse di seguito per ulteriori argomenti in Content Services:

* [Sviluppo di modelli](/help/mobile/administer-mobile-apps.md)
* [Authoring di Content Services](/help/mobile/develop-content-as-a-service.md)
* [Amministrazione di Content Services](/help/mobile/developing-content-services.md)

