---
title: Migrazione all’interfaccia utente touch
description: Scopri la migrazione di Adobe Experience Manager all’interfaccia utente touch e come ti interessa.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 3%

---

# Migrazione all’interfaccia utente touch{#migration-to-the-touch-ui}

A partire dalla versione 6.0, Adobe Experience Manager (AEM) ha introdotto una nuova interfaccia utente denominata *interfaccia touch* (nota anche semplicemente come *interfaccia touch*). È allineato al Adobe Experience Cloud e alle linee guida generali dell’interfaccia utente di Adobe. Questa è diventata l&#39;interfaccia utente standard in AEM con l&#39;interfaccia legacy orientata al desktop denominata *interfaccia classica*.

Se utilizzi l’AEM con l’interfaccia classica, adotta un’azione per migrare l’istanza. Questa pagina ha lo scopo di fungere da trampolino di lancio fornendo collegamenti a singole risorse.

>[!NOTE]
>
>Tale progetto di migrazione può avere un impatto significativo sulla tua istanza. Per le linee guida consigliate, consulta [Gestione dei progetti - Best practice](/help/managing/best-practices.md).

## Nozioni di base {#the-basics}

Durante la migrazione, tieni presente le seguenti differenze principali tra l’interfaccia utente classica e l’interfaccia touch:

<table>
 <tbody>
  <tr>
   <td>Interfaccia classica</td>
   <td>Interfaccia touch</td>
  </tr>
  <tr>
   <td>È descritto nell’archivio JCR come struttura di nodi. Ogni nodo che rappresenta un elemento dell'interfaccia utente viene chiamato widget <em>ExtJS</em> ed è sottoposto a rendering sul lato client da <code>ExtJS</code>.</td>
   <td>Descritto anche nell’archivio JCR come struttura di nodi. Tuttavia, in questo caso, ogni nodo fa riferimento a un tipo di risorsa Sling (componente Sling), che è responsabile del rendering. L’interfaccia utente viene quindi sottoposta a rendering lato server.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>non utilizzato</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>utilizzato</li>
     <li>ad esempio <br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Nodi finestra di dialogo:</p>
    <ul>
     <li>Nome: <code>dialog</code></li>
     <li><code>jcr:primaryType</code>: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Nodi finestra di dialogo:</p>
    <ul>
     <li>Nome: <code>cq:dialog</code></li>
     <li><code>jcr:primaryType</code>: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Posizione JavaScript:</p>
    <ul>
     <li>Le parti imperative sono direttamente incorporate utilizzando listener o gestite in clientlibs.</li>
    </ul> </td>
   <td><p>Posizione JavaScript:</p>
    <ul>
     <li>Le parti imperative non possono essere incorporate nella definizione del dialogo; separazione delle responsabilità.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestione degli eventi:</p>
    <ul>
     <li>I widget per finestre di dialogo fanno riferimento direttamente al codice JavaScript.</li>
    </ul> </td>
   <td><p>Gestione degli eventi:</p>
    <ul>
     <li>JavaScript osserva gli eventi di dialogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Rendering eseguito dal client:
    <ul>
     <li>Il client crea in modo dinamico i componenti dell’interfaccia utente.</li>
     <li>Richieste client (pull) definizione componente (come JSON) dal server.</li>
    </ul> </td>
   <td>Rendering eseguito dal server:
    <ul>
     <li>Il client richiede le pagine insieme alla relativa interfaccia utente.</li>
     <li>Il server invia (invia) l'interfaccia utente come documenti HTML utilizzando i componenti dell'interfaccia utente Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

In altre parole, la migrazione di una sezione dell&#39;interfaccia utente dall&#39;interfaccia classica all&#39;interfaccia touch significa portare un widget *ExtJS* in un *componente Sling*. Per semplificare questa operazione, l’interfaccia utente touch si basa sul framework dell’interfaccia utente Granite, che fornisce già alcuni componenti Sling per l’interfaccia utente (denominati componenti dell’interfaccia utente Granite).

Prima di iniziare, controlla lo stato e i consigli correlati:

* [Stato delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md)
* [Interfaccia utente di Recommendations per i clienti](/help/sites-deploying/ui-recommendations.md)

Le nozioni di base sullo sviluppo dell’interfaccia utente touch forniscono una solida base:

* [Concetti dell’interfaccia touch dell’AEM](/help/sites-developing/touch-ui-concepts.md)
* [Struttura dell’interfaccia utente touch dell’AEM](/help/sites-developing/touch-ui-structure.md)

## Migrazione in corso dell’authoring delle pagine {#migrating-page-authoring}

Le finestre di dialogo sono un fattore importante durante la migrazione dei componenti:

* [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md) (con interfaccia touch)
* [Migrazione da un componente classico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) - per aiutarti a convertire le finestre di dialogo dei componenti dell&#39;interfaccia classica in interfaccia touch

   * Nell’interfaccia touch è disponibile un livello di compatibilità per aprire una finestra di dialogo dell’interfaccia classica all’interno di un &quot;wrapper dell’interfaccia touch&quot;, ma questa opzione ha funzionalità limitate e non è consigliata a lungo termine.

* [Personalizzazione dei campi delle finestre di dialogo nell&#39;interfaccia utente touch](https://helpx.adobe.com/it/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creazione di un nuovo componente campo dell’interfaccia utente Granite](/help/sites-developing/granite-ui-component.md)
* [Personalizzazione dell&#39;authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md) (con l&#39;interfaccia touch)

## Migrazione delle console {#migrating-consoles}

Puoi anche personalizzare le console:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md) (per l&#39;interfaccia touch)

## Considerazioni correlate {#related-considerations}

Sebbene non siano direttamente correlate a una migrazione all’interfaccia utente touch, è consigliabile considerare alcuni problemi correlati allo stesso tempo, in quanto sono anche una pratica consigliata:

* [Modelli](/help/sites-developing/templates.md) - [Modelli modificabili](/help/sites-developing/page-templates-editable.md)
* [Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it)

>[!NOTE]
>
>Vedi anche [Sviluppo - Best practice](/help/sites-developing/best-practices.md).

## Ulteriori risorse {#further-resources}

Per informazioni complete sullo sviluppo dell’AEM, consulta la raccolta di risorse sotto:

* [Guida utente sullo sviluppo](/help/sites-developing/getting-started.md)
* [Documentazione dell&#39;interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Tutorials e video su Sites 6.5](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html?lang=it) di AEM
* [Guida introduttiva allo sviluppo per AEM Sites - Esercitazione WKND](/help/sites-developing/getting-started.md)
* [Gems AEM](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=it)
* [Strumenti di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Gli strumenti di modernizzazione dell’AEM sono un’iniziativa della comunità e non sono supportati o giustificati dall’Adobe.
