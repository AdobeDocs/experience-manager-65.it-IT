---
title: Operazioni di base
description: Panoramica delle operazioni di base nell’ambiente di authoring di Adobe Experience Manager. Utilizza la console Sites come base.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 4%

---

# Operazioni di base{#basic-handling}

>[!NOTE]
>
>* Questa pagina offre una panoramica delle operazioni di base nell’ambiente di authoring Adobe Experience Manager (AEM). Usa la console **Sites** come base.
>
>* Alcune funzionalità non sono disponibili in tutte le console, mentre altre sono disponibili in alcune console. Informazioni specifiche sulle singole console e sulle relative funzionalità sono descritte più dettagliatamente in altre pagine.
>* Sono disponibili scelte rapide da tastiera in tutto il AEM. In particolare quando [si utilizzano le console](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) e [si modificano le pagine](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>

## Schermata di benvenuto {#the-welcome-screen}

L&#39;interfaccia utente classica offre una selezione di console utilizzando meccanismi noti per la navigazione e l&#39;avvio di azioni, tra cui clic, doppio clic e [menu di scelta rapida](#context-menus).

Dopo l&#39;accesso, viene visualizzata la schermata iniziale. Fornisce un elenco di collegamenti a console e servizi:

![schermata_shot_2012-01-30alle61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Console {#consoles}

Le console principali sono:

<table>
 <tbody>
  <tr>
   <td><strong>Console</strong></td>
   <td><strong>Scopo</strong></td>
  </tr>
  <tr>
   <td><strong>Benvenuti</strong></td>
   <td>Offre una panoramica e un accesso diretto (tramite collegamenti) alle funzionalità principali dell’AEM.</td>
  </tr>
  <tr>
   <td><strong>Assets digitale</strong><br /> </td>
   <td>Queste console ti consentono di importare e <a href="/help/sites-classic-ui-authoring/classicui-assets.md">gestire risorse digitali</a> quali immagini, video, documenti e file audio. Queste risorse possono quindi essere utilizzate da qualsiasi sito web in esecuzione sulla stessa istanza AEM. </td>
  </tr>
  <tr>
   <td><strong>Lanci</strong></td>
   <td>Questo consente di gestire i <a href="/help/sites-classic-ui-authoring/classic-launches.md">lanci</a>; questi consentono di sviluppare il contenuto per una versione futura di una o più pagine Web attivate.<br /> <i>Nota: nell'interfaccia touch sono disponibili molte delle stesse funzionalità nella console Sites, insieme alla barra Riferimenti.</i> <i>Se necessario, questa console è disponibile dalla console Strumenti; selezionare Operazioni, quindi Avvii.</i></td>
  </tr>
  <tr>
   <td><strong>Casella in entrata </strong></td>
   <td>Spesso sono coinvolte più persone nelle sottoattività di un flusso di lavoro e ogni persona deve completare il proprio passaggio prima di consegnare il lavoro alla persona successiva. La Casella in entrata consente di visualizzare le notifiche relative a tali attività. Vedi <a href="/help/sites-administering/workflows.md">Utilizzo dei flussi di lavoro</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Assegnazione dei tag</strong></td>
   <td>Le console di assegnazione tag consentono di gestire i tag. I tag sono nomi brevi o frasi che puoi utilizzare per classificare e annotare parti di contenuto in modo da semplificarne la ricerca e l’organizzazione. Per ulteriori informazioni, vedere <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Utilizzo e gestione dei tag</a>.</td>
  </tr>
  <tr>
   <td><strong>Strumenti</strong></td>
   <td>Le <a href="/help/sites-administering/tools-consoles.md">console Strumenti</a> consentono di accedere a console e strumenti specifici per la gestione dei siti Web, delle risorse digitali e di altri aspetti dell'archivio dei contenuti.</td>
  </tr>
  <tr>
   <td><strong>Utenti</strong></td>
   <td>Queste console consentono di gestire i diritti di accesso di utenti e gruppi. Per informazioni dettagliate, vedere <a href="/help/sites-administering/security.md">Amministrazione utenti e sicurezza</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Siti Web</strong></td>
   <td>Le console Sites/Websites ti consentono di <a href="/help/sites-classic-ui-authoring/classic-page-author.md">creare, visualizzare e gestire siti Web</a> in esecuzione nell'istanza AEM. Tramite queste console puoi creare, copiare, spostare ed eliminare pagine web, avviare flussi di lavoro e attivare (pubblicare) pagine. È inoltre possibile aprire una pagina per la modifica.<br /> </td>
  </tr>
  <tr>
   <td><strong>Flussi di lavoro</strong></td>
   <td>Un flusso di lavoro è una serie definita di passaggi che descrivono il processo di completamento di alcune attività. Spesso sono coinvolte più persone in un'attività e ogni persona deve completare il proprio passaggio prima di consegnare il lavoro alla persona successiva. La console Flusso di lavoro consente di creare modelli di flusso di lavoro e gestire le istanze di flusso di lavoro in esecuzione. Vedi <a href="/help/sites-administering/workflows.md">Utilizzo dei flussi di lavoro</a>.<br /> </td>
  </tr>
 </tbody>
</table>

La console **Siti Web** offre due riquadri per la navigazione e la gestione delle pagine:

* Riquadro sinistro

  Mostra la struttura ad albero dei siti Web e le pagine all&#39;interno di tali siti.

  Mostra anche informazioni su altri aspetti dell’AEM, inclusi progetti, progetti e risorse.

* Riquadro destro

  Mostra le pagine (nella posizione selezionata nel riquadro a sinistra) e può essere utilizzato per intervenire.

Da qui è possibile [gestire le pagine](/help/sites-authoring/managing-pages.md) utilizzando la barra degli strumenti, un menu di scelta rapida o aprendo una pagina per ulteriori azioni.

>[!NOTE]
>
>Le operazioni di base sono le stesse su tutte le console. Questa sezione si concentra sulla console **Siti Web** in quanto è la console principale utilizzata durante l&#39;authoring.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Accedere all’Aiuto   {#accessing-help}

Su varie console (ad esempio, Siti Web) è disponibile un pulsante **Guida**. Facendo clic su **Guida** verrà aperto Condivisione pacchetti o il sito della documentazione.

![chlimage_1-10](assets/chlimage_1-10a.png)

Durante la modifica di una pagina, la barra laterale [presenta anche un pulsante per accedere alla Guida](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navigazione con la console Siti web {#navigating-with-the-websites-console}

Nella console **Siti Web** le pagine di contenuto sono elencate in una struttura ad albero (riquadro a sinistra). Per semplificare la navigazione, è possibile espandere (+) o comprimere (-) le sezioni della struttura ad albero come richiesto:

* Facendo clic sul nome della pagina nel riquadro a sinistra, si effettua quanto segue:

   * Elenca le pagine figlie nel riquadro di destra
   * Espande la struttura nel riquadro sinistro.

     Per motivi di prestazioni, questa azione dipende dal numero di nodi secondari. Con un&#39;installazione standard, questo metodo di espansione funziona quando sono presenti al massimo `30` nodi secondari.

* Facendo doppio clic sul nome della pagina (riquadro sinistro), la struttura si espande, anche se l&#39;apertura della pagina non è così evidente.

>[!NOTE]
>
>Questo valore predefinito ( `30`) può essere modificato per console nelle configurazioni specifiche dell&#39;applicazione del widget siteadmin:
>
>Sul nodo siteadmin:
>
>Imposta il valore della proprietà:
>`treeAutoExpandMax`
>il:
>`/apps/wcm/core/content/siteadmin`
>
>O globalmente nel tema:
>Imposta il valore di:
>`TREE_AUTOEXPAND_MAX`
>in:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Per ulteriori dettagli, consulta [SiteAdmin nell&#39;API del widget CQ](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin).

## Informazioni pagina nella console Siti web {#page-information-on-the-websites-console}

Il riquadro destro della console **Siti Web** fornisce una visualizzazione elenco con informazioni sulle pagine:

![informazioni-pagina](assets/page-info.png)

Sono disponibili gli elementi seguenti. Per impostazione predefinita viene visualizzato un sottoinsieme di questi campi:

<table>
 <tbody>
  <tr>
   <td><strong>Colonna</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Miniatura </td>
   <td>Mostra una miniatura per la pagina.</td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Titolo visualizzato nella pagina</td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>Il nome AEM si riferisce alla pagina</td>
  </tr>
  <tr>
   <td>Pubblicato</td>
   <td>Indica se la pagina è stata pubblicata e fornisce la data e l’ora di pubblicazione.</td>
  </tr>
  <tr>
   <td>Modificato</td>
   <td>Indica se la pagina è stata modificata e fornisce la data e l’ora della modifica. Per salvare eventuali modifiche, devi attivare la pagina.</td>
  </tr>
  <tr>
   <td>Scene7 Publish</td>
   <td>Indica se la pagina è stata pubblicata in Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Stato</td>
   <td>Indica lo stato della pagina, ad esempio se la pagina fa parte di un flusso di lavoro o di una Live Copy o se è bloccata.</td>
  </tr>
  <tr>
   <td>Impression</td>
   <td>Mostra l’attività su una pagina in numero di hit.</td>
  </tr>
  <tr>
   <td>Modello</td>
   <td>Indica il modello su cui si basa una pagina.</td>
  </tr>
  <tr>
   <td>Nel flusso di lavoro</td>
   <td>Indica quando la pagina si trova in un flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Bloccato da</td>
   <td>Indica quando una pagina è stata bloccata e l'account utente che l'ha bloccata.</td>
  </tr>
  <tr>
   <td>Live Copy </td>
   <td>Indica quando la pagina fa parte di una Live Copy.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Per selezionare le colonne visibili, posiziona il cursore del mouse sul titolo di una colonna. Viene visualizzato un menu a discesa e da qui puoi utilizzare l&#39;opzione **Colonne**.

I colori accanto alle pagine nelle colonne **Pubblicato** e **Modificato** indicano lo stato della pubblicazione:

| **Colonna** | **Colore** | **Descrizione** |
|---|---|---|
| Pubblicato | Verde | Pubblicazione completata. Il contenuto viene pubblicato. |
| Pubblicato | Giallo | Pubblicazione in sospeso. Il sistema non ha ancora ricevuto la conferma della pubblicazione. |
| Pubblicato | Rosso | Pubblicazione non riuscita. Non esiste alcuna connessione con l’istanza Publish. Questo può anche significare che il contenuto è stato disattivato. |
| Pubblicato | *vuoto* | Questa pagina non è mai stata pubblicata. |
| Modificato | Blu | La pagina è stata modificata dall&#39;ultima pubblicazione. |
| Modificato | *vuoto* | La pagina non è mai stata modificata o non è stata modificata dall&#39;ultima pubblicazione. |

## Menu di scelta rapida {#context-menus}

L’interfaccia classica utilizza meccanismi noti per la navigazione e l’avvio di azioni, tra cui il clic e il doppio clic. A seconda della situazione attuale, sono disponibili anche diversi menu di scelta rapida (aperti con il pulsante destro del mouse):

![chlimage_1-11](assets/chlimage_1-11a.png)
