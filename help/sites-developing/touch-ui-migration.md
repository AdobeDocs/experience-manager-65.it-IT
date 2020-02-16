---
title: Migrazione all’interfaccia utente touch
seo-title: Migrazione all’interfaccia utente touch
description: Migrazione all’interfaccia utente touch
seo-description: Migrazione all’interfaccia utente touch
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Migration to the Touch UI{#migration-to-the-touch-ui}

A partire dalla versione 6.0, Adobe Experience Manager (AEM) ha introdotto una nuova interfaccia utente denominata interfaccia ** touch (detta anche interfaccia *touch*). È allineata ad Adobe Marketing Cloud e alle linee guida generali dell&#39;interfaccia utente di Adobe. Questa è diventata l’interfaccia standard di AEM con l’interfaccia precedente, orientata al desktop, detta interfaccia *classica*.

Se utilizzi AEM con l’interfaccia classica, devi agire per migrare l’istanza. Questa pagina è destinata a fungere da trampolino di lancio, fornendo collegamenti alle singole risorse.

>[!NOTE]
>
>Tale progetto di migrazione potrebbe avere un impatto significativo sull’istanza. Consultate [Gestione dei progetti - Best practice](/help/managing/best-practices.md) per le linee guida consigliate.

## Nozioni di base {#the-basics}

Durante la migrazione, è importante tenere presente le seguenti (principali) differenze tra l’interfaccia classica e quella touch:

<table>
 <tbody>
  <tr>
   <td>Interfaccia classica</td>
   <td>Interfaccia utente touch</td>
  </tr>
  <tr>
   <td>Viene descritta nell'archivio JCR come una struttura di nodi. Ogni nodo che rappresenta un elemento dell’interfaccia utente è denominato widget <em></em> ExtJS ed è rappresentato sul lato client <code>ExtJS</code>.</td>
   <td>Anche descritto nell'archivio JCR come una struttura di nodi. Tuttavia, in questo caso ogni nodo fa riferimento a un tipo di risorsa Sling (componente Sling), responsabile del rendering. Quindi l'interfaccia utente è (sostanzialmente) rappresentata lato server.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>non utilizzato</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>utilizzato</li>
     <li>for example<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Nodi di dialogo:</p>
    <ul>
     <li>Nome: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Nodi di dialogo:</p>
    <ul>
     <li>Nome: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Posizione JavaScript:</p>
    <ul>
     <li>Le parti imperative vengono incorporate direttamente utilizzando listener o gestite in clientlibs.</li>
    </ul> </td>
   <td><p>Posizione JavaScript:</p>
    <ul>
     <li>Non è possibile incorporare parti immateriali nella definizione del dialogo; separazione delle responsabilità.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestione degli eventi:</p>
    <ul>
     <li>I widget di dialogo fanno direttamente riferimento al codice JavaScript.</li>
    </ul> </td>
   <td><p>Gestione degli eventi:</p>
    <ul>
     <li>Javascript osserva gli eventi di dialogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Rendering eseguito dal client:
    <ul>
     <li>Client crea in modo dinamico i componenti dell'interfaccia utente.</li>
     <li>Definizione di componente (come JSON) richieste dal client dal server.</li>
    </ul> </td>
   <td>Rendering eseguito dal server:
    <ul>
     <li>Il client richiede le pagine insieme all'interfaccia utente correlata.</li>
     <li>Il server invia (push) l’interfaccia utente come documenti HTML; utilizzo dei componenti dell’interfaccia utente Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

In altre parole, migrare una sezione dell’interfaccia utente dall’interfaccia classica all’interfaccia touch significa portare un widget ** ExtJS su un componente ** Sling. Per facilitare questa fase, l’interfaccia utente touch si basa sulla cornice dell’interfaccia Granite, che include già alcuni componenti Sling per l’interfaccia (chiamati componenti dell’interfaccia Granite).

Prima di iniziare, controllate lo stato e le raccomandazioni correlate:

* [Stato delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md)
* [Raccomandazioni in merito all&#39;interfaccia utente per i clienti](/help/sites-deploying/ui-recommendations.md)

Le basi dello sviluppo dell’interfaccia touch forniranno una solida base:

* [Concetti dell’interfaccia utente di AEM Touch](/help/sites-developing/touch-ui-concepts.md)
* [Struttura dell&#39;interfaccia utente di AEM Touch](/help/sites-developing/touch-ui-structure.md)

## Migrazione dell’authoring delle pagine {#migrating-page-authoring}

Le finestre di dialogo sono un fattore importante per la migrazione dei componenti:

* [Sviluppo di componenti](/help/sites-developing/developing-components.md) AEM (con l’interfaccia touch)
* [Migrazione da un componente classico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Strumento](/help/sites-developing/dialog-conversion.md) di conversione delle finestre di dialogo per convertire le finestre di dialogo dei componenti dell’interfaccia classica in interfaccia touch

   * Nell’interfaccia touch è disponibile un livello di compatibilità per aprire una finestra di dialogo dell’interfaccia classica all’interno di un wrapper dell’interfaccia touch, ma questo dispone di funzionalità limitate e non è consigliato a lungo termine.

* [Personalizzazione dei campi di dialogo nell’interfaccia utente touch](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creazione di un nuovo componente Campo interfaccia Granite](/help/sites-developing/granite-ui-component.md)
* [Personalizzazione dell’authoring](/help/sites-developing/customizing-page-authoring-touch.md) di pagina (con l’interfaccia touch)

## Migrazione delle console {#migrating-consoles}

Potete inoltre personalizzare le console:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md) (per l’interfaccia touch)

## Considerazioni correlate {#related-considerations}

Sebbene non siano direttamente correlati a una migrazione all’interfaccia utente touch, è consigliabile tenere presenti anche alcuni problemi correlati:

* [Modelli](/help/sites-developing/templates.md) - Modelli [modificabili](/help/sites-developing/page-templates-editable.md)
* [Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Vedere anche [Sviluppo - Best Practices](/help/sites-developing/best-practices.md).

## Ulteriori risorse {#further-resources}

Per informazioni complete sullo sviluppo di AEM, consulta la raccolta di risorse in:

* [Guida utente allo sviluppo](/help/sites-developing/home.md)
* [Documentazione di Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Esercitazioni e video sui siti AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Guida introduttiva allo sviluppo di siti AEM - Esercitazione WKND](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Strumenti di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Gli strumenti di modernizzazione di AEM sono uno sforzo della community e non sono supportati o giustificati da Adobe.

