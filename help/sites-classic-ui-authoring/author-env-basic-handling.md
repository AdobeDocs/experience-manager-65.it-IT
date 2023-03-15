---
title: Operazioni di base
seo-title: Basic Handling
description: Panoramica sulle operazioni di base per l’utilizzo dell’ambiente di authoring di AEM. Usa la console Sites come base.
seo-description: An overview of basic handling when using the AEM author environment. It uses the Sites console as a basis.
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 94%

---

# Operazioni di base{#basic-handling}

>[!NOTE]
>
>* Questa pagina offre una panoramica delle operazioni di base nell’ambiente di creazione AEM. Usa la console **Sites** come base.
>
>* Alcune funzionalità non sono disponibili su tutte le console e/o certe funzionalità aggiuntive sono disponibili solo in determinate console. In altre sezioni puoi trovare informazioni specifiche sulle singole console e le relative funzionalità.
>* AEM supporta l’utilizzo di scelte rapide da tastiera in numerose aree, in particolare per l’[utilizzo delle console](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) e la [modifica delle pagine](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>


## Schermata di benvenuto {#the-welcome-screen}

Nell’interfaccia classica, sono disponibili diverse console in cui è possibile usare i consueti sistemi di navigazione e di avvio delle azioni, quali clic, doppio clic e [selezione di voci nei menu di scelta rapida](#context-menus).

Subito dopo l’accesso viene visualizzata la schermata introduttiva, che fornisce un elenco di collegamenti alle console e ai servizi:

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Console {#consoles}

Le console principali sono:

<table>
 <tbody>
  <tr>
   <td><strong>Console</strong></td>
   <td><strong>Scopo</strong></td>
  </tr>
  <tr>
   <td><strong>Benvenuto</strong></td>
   <td>Offre una panoramica e collegamenti di accesso diretto alle principali funzioni di AEM.</td>
  </tr>
  <tr>
   <td><strong>Risorse digitali</strong><br /> </td>
   <td>Queste console consentono di importare e <a href="/help/sites-classic-ui-authoring/classicui-assets.md">gestire le risorse digitali</a> quali immagini, video, documenti e file audio. Puoi usare queste risorse da qualunque sito web in esecuzione nell’istanza di AEM. </td>
  </tr>
  <tr>
   <td><strong>Lanci</strong></td>
   <td>Questa console consente di gestire i <a href="/help/sites-classic-ui-authoring/classic-launches.md">lanci</a> e sviluppare i contenuti per rilasci futuri di una o più pagine Web attivate.<br /> <i>Nota: Nell’interfaccia touch molte delle funzionalità sono disponibili nella console Sites e nella barra laterale Riferimenti.</i><i>Se necessario, questa console è disponibile dalla console Strumenti; selezionate Operazioni, quindi Lanci. </i></td>
  </tr>
  <tr>
   <td><strong>Casella in entrata </strong></td>
   <td>In molti casi, le attività secondarie di un flusso di lavoro coinvolgono più persone, ognuna delle quali deve completare un passaggio prima che il lavoro possa essere passato alla persona successiva. La Casella in entrata permette di visualizzare tutte le notifiche relative a tali attività. Consultate <a href="/help/sites-administering/workflows.md">Lavorare con flussi di lavoro</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Assegnazione dei tag</strong></td>
   <td>Questa console consente di gestire i tag. I tag sono parole o termini con cui è possibile e annotare i contenuti per facilitarne la ricerca e l’organizzazione. Per ulteriori informazioni consultate <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Uso e Gestione dei tag</a>.</td>
  </tr>
  <tr>
   <td><strong>Strumenti</strong></td>
   <td>Le <a href="/help/sites-administering/tools-consoles.md">console Strumenti</a> permettono di accedere a console e strumenti specifici per la gestione dei siti Web, delle risorse digitali e altri aspetti dell’archivio dei contenuti.</td>
  </tr>
  <tr>
   <td><strong>Utenti</strong></td>
   <td>Queste console consentono di gestire i diritti di accesso di utenti e gruppi. Per informazioni, consultate <a href="/help/sites-administering/security.md">Amministrazione degli utenti e sicurezza</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Siti Web</strong></td>
   <td>Le console Siti e Siti Web consentono di <a href="/help/sites-classic-ui-authoring/classic-page-author.md">creare, visualizzare e gestire i siti Web</a> in esecuzione nell’istanza di AEM. È possibile creare, copiare, spostare ed eliminare pagine di siti Web, avviare flussi di lavoro e attivare (pubblicare) le pagine. È inoltre possibile attivare la pagina quando viene aperta per la modifica.<br /> </td>
  </tr>
  <tr>
   <td><strong>Flussi di lavoro</strong></td>
   <td>Per flusso di lavoro si intende una serie di passaggi necessari per completare determinate attività. In molti casi, un’attività coinvolge più persone, ognuna delle quali deve completare un proprio passaggio prima che il lavoro possa essere passato alla persona successiva. La console Flusso di lavoro permette di generare modelli di flussi di lavoro e di gestire le istanze dei flussi di lavoro in corso. Consultate <a href="/help/sites-administering/workflows.md">Lavorare con flussi di lavoro</a>.<br /> </td>
  </tr>
 </tbody>
</table>

La console **Siti Web** offre due riquadri che consentono di navigare e gestire le pagine:

* Riquadro a sinistra

   Mostra la struttura ad albero dei siti web e le relative pagine.

   Contiene inoltre informazioni su altri aspetti o su AEM, compresi progetti, blueprint e risorse.

* Riquadro a destra

   Mostra le pagine (nella posizione selezionata nel riquadro a sinistra) e può essere utilizzato per eseguire azioni.

Consente di [gestire le pagine](/help/sites-authoring/managing-pages.md) mediante la barra degli strumenti, un menu di scelta rapida o l’apertura della pagina per ulteriori interventi.

>[!NOTE]
>
>Tutte le console condividono le stesse operazioni di base. Questa sezione descrive la console **Siti Web** in quanto è la console primaria per le operazioni di authoring.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Accedere all’Aiuto   {#accessing-help}

In diverse console (ad esempio Siti web) è disponibile anche il pulsante **Aiuto**, che permette di accedere a Condivisione pacchetti o al sito della documentazione.

![chlimage_1-10](assets/chlimage_1-10a.png)

Quando modifichi una pagina, nella [barra laterale è disponibile anche un pulsante di accesso all’Aiuto](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navigazione con la console Siti web {#navigating-with-the-websites-console}

Nella console **Siti web** le pagine di contenuto sono elencate in una struttura ad albero (riquadro a sinistra). Per semplificare la navigazione, le varie sezioni della struttura ad albero possono essere espanse (+) o compresse (-):

* Con un singolo clic sul nome della pagina (nel riquadro di sinistra) è possibile:

   * Visualizzare l’elenco delle pagine figlio nel riquadro di destra
   * Espandere la struttura nel riquadro di sinistra

      Per motivi di prestazioni questa azione dipende dal numero dei nodi figlio. In un’installazione standard questo metodo di espansione funziona se è presente un massimo di `30` nodi figlio.

* Anche il doppio clic sul nome della pagina (nel riquadro a sinistra) permette di espandere l’albero. Tuttavia, poiché la pagina viene contemporaneamente aperta, tale effetto non risulta evidente.

>[!NOTE]
>
>Puoi modificare il valore predefinito (`30`) a livello della console nelle configurazioni specifiche delle applicazioni, nel widget di amministrazione del sito:
>
>Nel nodo di amministrazione del sito:
>
>Impostate il valore della proprietà:
>`treeAutoExpandMax`
>su:
>`/apps/wcm/core/content/siteadmin`
>
>In alternativa, a livello globale nel tema:
>Impostate il valore di:
>`TREE_AUTOEXPAND_MAX`
>in:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Per ulteriori informazioni, consulta [SiteAdmin in CQ Widget API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin).

## Informazioni sulla pagina nella console Siti web {#page-information-on-the-websites-console}

Nel riquadro a destra nella console **Siti web** è disponibile una vista a elenco con le seguenti informazioni sulle pagine:

![page-info](assets/page-info.png)

Sono disponibili le seguenti informazioni; un sottoinsieme di questi campi figura come impostazione predefinita:

<table>
 <tbody>
  <tr>
   <td><strong>Colonna</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Miniatura </td>
   <td>Miniatura della pagina</td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Titolo visualizzato sulla pagina</td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>Nome utilizzato da AEM per fare riferimento alla pagina</td>
  </tr>
  <tr>
   <td>Pubblicato</td>
   <td>Indica se la pagina è stata pubblicata e specifica la data e l’ora di pubblicazione.</td>
  </tr>
  <tr>
   <td>Modificato</td>
   <td>Indica se la pagina è stata modificata e specifica la data e l’ora di modifica. Per salvare eventuali modifiche, è necessario attivare la pagina.</td>
  </tr>
  <tr>
   <td>Pubblicazione Scene7</td>
   <td>Indica se la pagina è stata pubblicata su Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Stato</td>
   <td>Indica lo stato corrente della pagina, specificando ad esempio se la pagina fa parte di un flusso di lavoro o Live Copy oppure se al momento è bloccata.</td>
  </tr>
  <tr>
   <td>Impression</td>
   <td>Mostra l’attività sulla pagina in termini di numero di hit.</td>
  </tr>
  <tr>
   <td>Modello</td>
   <td>Indica il modello su cui è basata la pagina.</td>
  </tr>
  <tr>
   <td>Nel flusso di lavoro</td>
   <td>Indica se la pagina è inserita in un flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Bloccato da</td>
   <td>Indica se una pagina è stata bloccata e l’account utente che l’ha bloccata.</td>
  </tr>
  <tr>
   <td>Live Copy </td>
   <td>Indica se la pagina fa parte di una Live Copy.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Per selezionare le colonne visibili, passa il cursore del mouse sul titolo di una colonna. Nel menu a discesa che compare, scegli **Colonne**.

Lo stato di pubblicazione è indicato dai colori accanto alle pagine nelle colonne **Pubblicato** e **Modificato**:

| **Colonna** | **Colore** | **Descrizione** |
|---|---|---|
| Pubblicato | Verde | La pubblicazione è stata eseguita correttamente. Il contenuto è stato pubblicato. |
| Pubblicato | Giallo | La pubblicazione è in sospeso. Il sistema non ha ricevuto la conferma della pubblicazione. |
| Pubblicato | Rosso | La pubblicazione non è riuscita. La connessione con l’istanza di pubblicazione non è disponibile. Può anche indicare che il contenuto è stato disattivato. |
| Pubblicato | *Vuoto* | La pagina non è mai stata pubblicata. |
| Modificato | Blu | La pagina è stata modificata dopo l’ultima pubblicazione. |
| Modificato | *Vuoto* | La pagina non è mai stata modificata oppure non è stata modificata dopo l’ultima pubblicazione. |

## Menu di scelta rapida {#context-menus}

Nell’interfaccia classica, la navigazione e le azioni vengono eseguite mediante operazioni consuete, quali clic e doppio clic. A seconda della situazione corrente, sono inoltre disponibili diversi menu di scelta rapida (solitamente accessibili mediante clic con il pulsante destro del mouse):

![chlimage_1-11](assets/chlimage_1-11a.png)
