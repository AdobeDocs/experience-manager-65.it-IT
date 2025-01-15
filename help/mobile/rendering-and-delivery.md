---
title: Rendering e consegna
description: Scopri come eseguire il rendering del contenuto Adobe Experience Manager tramite i servlet predefiniti di Sling per eseguire il rendering di JSON e altri formati.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# Rendering e consegna{#rendering-and-delivery}

{{ue-over-mobile}}

È possibile eseguire facilmente il rendering del contenuto Adobe Experience Manager (AEM) tramite [Sling Default Servlets](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) per eseguire il rendering di [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) e altri formati.

In genere, questi rendering predefiniti percorrono l’archivio e restituiscono il contenuto così com’è.

AEM, tramite Sling, supporta anche lo sviluppo e la distribuzione di renderer sling personalizzati per assumere il controllo completo dello schema e del contenuto renderizzati.

I rendering predefiniti di Content Services colmano il gap tra i predefiniti di Sling e lo sviluppo personalizzato, consentendo la personalizzazione e il controllo di molti aspetti dei contenuti renderizzati senza sviluppo.

Il diagramma seguente mostra il rendering di Content Services.

![chlimage_1-15](assets/chlimage_1-15.png)

## Richiesta JSON {#requesting-json}

Utilizza **&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** per richiedere JSON.

<table>
 <tbody>
  <tr>
   <td>RISORSA</td>
   <td>una risorsa entità in /content/entities<br /> o <br /> una risorsa contenuto in /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>FACOLTATIVO</strong><br /> </p> <p>configurazione di esportazione trovata in /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Se omessa, viene applicata la configurazione di esportazione predefinita </p> </td>
  </tr>
  <tr>
   <td>PROFONDITÀ-INT</td>
   <td><strong>FACOLTATIVO</strong><br /> <br /> ricorsione di profondità per il rendering degli elementi figlio utilizzata nel rendering Sling</td>
  </tr>
 </tbody>
</table>

## Creazione di configurazioni di esportazione {#creating-export-configs}

È possibile creare configurazioni di esportazione per personalizzare il rendering JSON.

È possibile creare un nodo di configurazione in */apps/mobileapps/caas/exportConfigs.*

| Nome nodo | Nome della configurazione (per il selettore di rendering) |
|---|---|
| jcr:primaryType | nt:unstructured |

La tabella seguente mostra le proprietà delle configurazioni di esportazione:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predefinito (se non impostato)</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>includi tutto</td>
   <td>sling:resourceType</td>
   <td>escludi i dettagli per i nodi con sling:resourceType specificato dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>non escludere nulla</td>
   <td>sling:resourceType</td>
   <td>includi dettagli solo per i nodi con sling:resourceType specificato dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>non escludere nulla</td>
   <td>Prefissi di proprietà</td>
   <td>escludi dall’esportazione JSON le proprietà che iniziano con i prefissi specificati</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>non escludere nulla</td>
   <td>Nomi di proprietà</td>
   <td>escludi proprietà specificate dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>includi tutto</td>
   <td>Nomi di proprietà</td>
   <td><p>se excludePropertyPrefixes è impostato<br />, verranno incluse le proprietà specificate nonostante la corrispondenza con il prefisso che viene escluso,</p> <p>else (escludi proprietà ignorate) include solo queste proprietà</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>includi tutto</td>
   <td>nomi figlio</td>
   <td>escludi elementi figlio specificati dall’esportazione JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Stringa[]<br /> <br /> </td>
   <td>non escludere nulla</td>
   <td>nomi figlio</td>
   <td>includi solo gli elementi figlio specificati dall’esportazione JSON, escludi altro</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Stringa[]<br /> <br /> </td>
   <td>non rinominare nulla</td>
   <td>&lt;nome_proprietà_effettiva&gt;,&lt;nome_proprietà_sostitutiva&gt;</td>
   <td>rinominare le proprietà utilizzando le sostituzioni</td>
  </tr>
 </tbody>
</table>

### Sostituzioni esportazione tipo di risorsa {#resource-type-export-overrides}

Crea un nodo di configurazione in */apps/mobileapps/caas/exportConfigs.*

| nome | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

La tabella seguente mostra le proprietà:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predefinito (se non impostato)</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Per i seguenti tipi di risorse sling, non restituire l’esportazione JSON CaaS predefinita.<br /> Restituisci un'esportazione JSON cliente eseguendo il rendering della risorsa come;<br /> &lt;RISORSA&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurazioni di esportazione Content Services esistenti {#existing-content-services-export-configs}

Content Services include due configurazioni di esportazione:

* impostazione predefinita (nessuna configurazione specificata)
* pagina (per eseguire il rendering delle pagine del sito)

#### Configurazione di esportazione predefinita {#default-export-configuration}

La configurazione di esportazione predefinita di Content Services viene applicata se è specificata una configurazione nell&#39;URI richiesto.

&lt;RISORSA>.caas[.&lt;INT-PROFONDITÀ>].json

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
   <td>jcr:,sling:,cq:,oak:,page-</td>
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
   <td>Override Sling JSON</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configurazione esportazione pagina {#page-export-configuration}

Questa configurazione estende l’impostazione predefinita per includere il raggruppamento di elementi secondari sotto un nodo secondario.

&lt;SITE_PAGE>.caas.page[.&lt;INT-PROFONDITÀ>].json

### Risorse aggiuntive {#additional-resources}

Consulta le risorse seguenti per ulteriori informazioni su Content Services:

* [Sviluppo di modelli](/help/mobile/administer-mobile-apps.md)
* [Authoring di Content Services](/help/mobile/develop-content-as-a-service.md)
* [Amministrazione di Content Services](/help/mobile/developing-content-services.md)
