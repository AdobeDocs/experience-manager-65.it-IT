---
title: Migrazione all’interfaccia utente touch
seo-title: Migration to the Touch UI
description: Migrazione all’interfaccia utente touch
seo-description: Migration to the Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 6%

---

# Migrazione all’interfaccia utente touch{#migration-to-the-touch-ui}

A partire dalla versione 6.0, Adobe Experience Manager (AEM) ha introdotto una nuova interfaccia utente denominata *interfaccia touch* (noto anche come *interfaccia touch*). È allineato a Adobe Marketing Cloud e alle linee guida generali dell’interfaccia utente di Adobe. Questa è diventata l’interfaccia standard in AEM con l’interfaccia legacy, orientata al desktop, denominata *interfaccia classica*.

Se utilizzi AEM con l’interfaccia classica, devi intervenire per eseguire la migrazione dell’istanza. Questa pagina ha lo scopo di fungere da trampolino di lancio fornendo collegamenti a singole risorse.

>[!NOTE]
>
>Un tale progetto di migrazione può avere un impatto significativo sulla tua istanza. Vedi [Gestione dei progetti - Best practice](/help/managing/best-practices.md) per le linee guida consigliate.

## Nozioni di base {#the-basics}

Durante la migrazione è necessario tenere presente le seguenti differenze (principali) tra l’interfaccia classica e quella touch:

<table>
 <tbody>
  <tr>
   <td>Interfaccia classica</td>
   <td>Interfaccia utente touch</td>
  </tr>
  <tr>
   <td>È descritto nell’archivio JCR come una struttura di nodi. Ogni nodo che rappresenta un elemento dell’interfaccia utente è denominato <em>Widget ExtJS</em> ed è eseguito il rendering sul lato client tramite <code>ExtJS</code>.</td>
   <td>Anche descritto nell’archivio JCR come una struttura di nodi. Tuttavia, in questo caso ogni nodo fa riferimento a un tipo di risorsa Sling (componente Sling), che è responsabile del suo rendering. Quindi l'interfaccia utente viene (sostanzialmente) sottoposta a rendering lato server.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>non utilizzato</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>utilizzato</li>
     <li>per esempio<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
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
     <li>Le parti imperative sono direttamente incorporate utilizzando listener o gestite in clientlibs.</li>
    </ul> </td>
   <td><p>Posizione JavaScript:</p>
    <ul>
     <li>Le parti imperibili non possono essere incorporate nella definizione della finestra di dialogo; separazione delle responsabilità.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestione degli eventi:</p>
    <ul>
     <li>I widget di dialogo fanno riferimento direttamente al codice JavaScript.</li>
    </ul> </td>
   <td><p>Gestione degli eventi:</p>
    <ul>
     <li>Javascript osserva gli eventi di dialogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Rendering eseguito dal client:
    <ul>
     <li>Client crea in modo dinamico i componenti dell’interfaccia utente.</li>
     <li>Definizione del componente richieste client (Pull) (come JSON) dal server.</li>
    </ul> </td>
   <td>Rendering eseguito dal server:
    <ul>
     <li>Il client richiede le pagine insieme all’interfaccia utente correlata.</li>
     <li>Il server invia (push) l’interfaccia utente come documenti HTML; utilizzo dei componenti dell’interfaccia Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

In altre parole, la migrazione di una sezione dell’interfaccia utente dall’interfaccia classica all’interfaccia touch significa portare un *Widget ExtJS* a *Componente Sling*. Per facilitare questa fase, l’interfaccia utente touch si basa sul framework dell’interfaccia utente Granite, che fornisce già alcuni componenti Sling per l’interfaccia utente (denominati componenti dell’interfaccia Granite).

Prima di iniziare, controlla lo stato e i consigli correlati:

* [Stato delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md)
* [Interfaccia utente Recommendations per clienti](/help/sites-deploying/ui-recommendations.md)

Le nozioni di base per lo sviluppo dell’interfaccia touch forniscono una solida base:

* [Concetti dell’interfaccia AEM touch](/help/sites-developing/touch-ui-concepts.md)
* [Struttura dell’interfaccia utente AEM touch](/help/sites-developing/touch-ui-structure.md)

## Migrazione dell’authoring delle pagine {#migrating-page-authoring}

Le finestre di dialogo sono un fattore importante durante la migrazione dei componenti:

* [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md) (con interfaccia touch)
* [Migrazione da un componente Classic](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) : per convertire le finestre di dialogo dei componenti dell’interfaccia classica in un’interfaccia touch

   * Nell’interfaccia touch è disponibile un livello di compatibilità per aprire una finestra di dialogo dell’interfaccia classica all’interno di un wrapper per dell’interfaccia touch, ma questo ha funzionalità limitate e non è consigliato a lungo termine.

* [Personalizzazione dei campi di dialogo nell’interfaccia utente touch](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creazione di un nuovo componente campo dell’interfaccia Granite](/help/sites-developing/granite-ui-component.md)
* [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md) (con interfaccia touch)

## Migrazione delle console {#migrating-consoles}

È inoltre possibile personalizzare le console:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md) (per l’interfaccia touch)

## Considerazioni correlate {#related-considerations}

Anche se non è direttamente correlato a una migrazione all’interfaccia utente touch, esistono problemi correlati che è bene considerare allo stesso tempo, in quanto sono anche la pratica consigliata:

* [Modelli](/help/sites-developing/templates.md) - [Modelli modificabili](/help/sites-developing/page-templates-editable.md)
* [Componenti core](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Vedi anche [Sviluppo - Best practice](/help/sites-developing/best-practices.md).

## Ulteriori risorse {#further-resources}

Per informazioni complete sullo sviluppo di AEM vedere la raccolta di risorse in:

* [Guida utente allo sviluppo](/help/sites-developing/home.md)
* [Documentazione dell’interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Tutorials e video AEM 6.5 Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Guida introduttiva allo sviluppo per AEM Sites - Esercitazione WKND](/help/sites-developing/getting-started.md)
* [AEM gemme](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Strumenti di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Gli strumenti di modernizzazione AEM sono uno sforzo comunitario e non sono supportati o garantiti dall&#39;Adobe.
