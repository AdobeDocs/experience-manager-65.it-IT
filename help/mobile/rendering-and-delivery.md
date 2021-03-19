---
title: Rendering e consegna
seo-title: Rendering e consegna
description: Rendering e consegna
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 8%

---


# Rendering e consegna{#rendering-and-delivery}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

AEM contenuto può essere facilmente sottoposto a rendering tramite [Sling Default Servlets](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) per eseguire il rendering di [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) e altri formati.

I moduli di rendering preconfigurati generalmente passano all’archivio e restituiscono il contenuto così com’è.

AEM, tramite Sling, supporta anche lo sviluppo e la distribuzione di moduli di rendering sling personalizzati per assumere il controllo completo dello schema e del contenuto renderizzati.

I renderer predefiniti di Content Services colmano il divario tra i valori predefiniti Sling e lo sviluppo personalizzato preconfigurati che consentono di personalizzare e controllare molti aspetti dei contenuti renderizzati senza sviluppo.

Il diagramma seguente illustra il rendering dei servizi di contenuti.

![chlimage_1-15](assets/chlimage_1-15.png)

## Richiesta di JSON {#requesting-json}

Utilizza **&lt;RESOURCE.caas[.&lt;export-config>.][&lt;export-config>.** jsonto per richiedere JSON.]

<table>
 <tbody>
  <tr>
   <td>RISORSA</td>
   <td>una risorsa entità sotto /content/entity<br /> o <br /> una risorsa contenuto sotto /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>FACOLTATIVO</strong><br /> </p> <p>una configurazione di esportazione trovata in /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Se omessa, verrà applicata la configurazione di esportazione predefinita </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong></strong><br /> <br /> ricorsività OPTIONALdepth per il rendering di elementi figlio come utilizzato nel rendering Sling</td>
  </tr>
 </tbody>
</table>

## Creazione di configurazioni di esportazione {#creating-export-configs}

È possibile creare configurazioni di esportazione per personalizzare il rendering JSON.

Puoi creare un nodo di configurazione in */apps/mobileapps/caas/exportConfigs.*

| Nome nodo | Nome della configurazione (per il selettore di rendering) |
|---|---|
| jcr:primaryType | nt:unstructured |

La tabella seguente mostra le proprietà di Export Configs:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predefinito (se, non impostato)</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Stringa[]</td>
   <td>include tutto</td>
   <td>sling:resourceType</td>
   <td>escludere i dettagli dei nodi con sling:resourceType specificato dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Stringa[]</td>
   <td>escludere nulla</td>
   <td>sling:resourceType</td>
   <td>includere i dettagli solo per i nodi con sling:resourceType specificato dall'esportazione JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Stringa[]</td>
   <td>escludere nulla</td>
   <td>Prefissi di proprietà</td>
   <td>escludere le proprietà che iniziano con prefissi specificati dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Stringa[]</td>
   <td>escludere nulla</td>
   <td>Nomi di proprietà</td>
   <td>escludere proprietà specificate dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Stringa[]</td>
   <td>include tutto</td>
   <td>Nomi di proprietà</td>
   <td><p>se excludePropertyPrefixes set<br /> include proprietà specificate nonostante la corrispondenza del prefisso sia esclusa,</p> <p>else (escludi proprietà ignorate) include solo queste proprietà</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Stringa[]</td>
   <td>include tutto</td>
   <td>nomi figli</td>
   <td>escludere elementi figlio specifici dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Stringa[]<br /> <br /> </td>
   <td>escludere nulla</td>
   <td>nomi figli</td>
   <td>includere solo elementi figlio specificati dall’esportazione JSON, escludi altri</td>
  </tr>
  <tr>
   <td>rinominareProperties</td>
   <td>Stringa[]<br /> <br /> </td>
   <td>rinomina nulla</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>rinominare le proprietà utilizzando sostituzioni</td>
  </tr>
 </tbody>
</table>

### Sostituzioni dell&#39;esportazione del tipo di risorsa {#resource-type-export-overrides}

Crea un nodo di configurazione in */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

Nella tabella seguente sono illustrate le proprietà:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predefinito (se, non impostato)</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>&lt;selector_to_inc&gt;</td>
   <td>Stringa[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Per i seguenti tipi di risorse sling, non restituire l'esportazione json predefinita CaaS.<br /> Restituisci un’esportazione json del cliente eseguendo il rendering della risorsa come;<br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurazioni di esportazione di Content Services esistenti {#existing-content-services-export-configs}

Content Services include due configurazioni di esportazione:

* predefinito (nessuna configurazione specificata)
* pagina (per eseguire il rendering delle pagine del sito)

#### Configurazione esportazione predefinita {#default-export-configuration}

La configurazione di esportazione predefinita di Content Services viene applicata se una configurazione è specificata nell’URI richiesto.

&lt;resource>.caas[.&lt;depth-int>].json

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
   <td>jcr:,sling:,cq:,oak:,pge-</td>
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
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configurazione esportazione pagina {#page-export-configuration}

Questa configurazione estende l&#39;impostazione predefinita per includere il raggruppamento di elementi secondari sotto un nodo figlio.

&lt;site_page>.caas.page[.&lt;depth-int>].json

### Risorse aggiuntive {#additional-resources}

Consulta le risorse riportate di seguito per ulteriori argomenti in Content Services:

* [Sviluppo di modelli](/help/mobile/administer-mobile-apps.md)
* [Authoring dei servizi per i contenuti](/help/mobile/develop-content-as-a-service.md)
* [Amministrazione dei servizi di contenuti](/help/mobile/developing-content-services.md)

