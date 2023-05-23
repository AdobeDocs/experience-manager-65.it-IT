---
title: Operazioni di base
description: Panoramica delle operazioni di base nell’ambiente di authoring AEM. Usa la console Sites come base.
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 7%

---

# Operazioni di base{#basic-handling}

>[!NOTE]
>
>* Questa pagina offre una panoramica delle operazioni di base nell’ambiente di authoring AEM. Usa la console **Sites** come base.
>
>* Alcune funzionalità non sono disponibili in tutte le console e/o altre sono disponibili in alcune console. Informazioni specifiche sulle singole console e sulle relative funzionalità saranno descritte più dettagliatamente in altre pagine.
>* AEM supporta l’utilizzo di scelte rapide da tastiera in numerose aree, in particolare per l’[utilizzo delle console](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) e la [modifica delle pagine](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>


## Schermata di benvenuto {#the-welcome-screen}

L’interfaccia classica offre una selezione di console utilizzando meccanismi noti per la navigazione e l’avvio di azioni quali clic, doppio clic e [menu di scelta rapida](#context-menus).

Al momento dell’accesso viene visualizzata la schermata iniziale, che fornisce un elenco di collegamenti alle console e ai servizi:

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
   <td>Offre una panoramica e un accesso diretto (tramite collegamenti) alle funzionalità principali dell’AEM.</td>
  </tr>
  <tr>
   <td><strong>Risorse digitali</strong><br /> </td>
   <td>Queste console consentono di importare e <a href="/help/sites-classic-ui-authoring/classicui-assets.md">gestire le risorse digitali</a> ad esempio immagini, video, documenti e file audio. Queste risorse possono quindi essere utilizzate da qualsiasi sito web in esecuzione sulla stessa istanza AEM. </td>
  </tr>
  <tr>
   <td><strong>Lanci</strong></td>
   <td>Questo consente di gestire <a href="/help/sites-classic-ui-authoring/classic-launches.md">lanci</a>; questi consentono di sviluppare il contenuto per una versione futura di una o più pagine web attivate.<br /> <i>Nota: nell’interfaccia touch, molte delle stesse funzionalità sono disponibili nella console Sites, insieme alla barra Riferimenti.</i> <i>Se necessario, questa console è disponibile dalla console Strumenti; seleziona Operazioni, quindi Avvii.</i></td>
  </tr>
  <tr>
   <td><strong>Casella in entrata </strong></td>
   <td>In molti casi un certo numero di persone sono coinvolte nelle sottoattività di un flusso di lavoro e ogni persona deve completare il proprio passaggio prima di consegnare il lavoro alla persona successiva. La Casella in entrata consente di visualizzare le notifiche relative a tali attività. Consulta <a href="/help/sites-administering/workflows.md">Utilizzo dei flussi di lavoro</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Assegnazione dei tag</strong></td>
   <td>Le console di assegnazione tag consentono di gestire i tag. I tag sono nomi brevi o frasi che puoi utilizzare per classificare e annotare parti di contenuto in modo da semplificarne la ricerca e l’organizzazione. Per ulteriori informazioni, consulta <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Utilizzo e gestione dei tag</a>.</td>
  </tr>
  <tr>
   <td><strong>Strumenti</strong></td>
   <td>Il <a href="/help/sites-administering/tools-consoles.md">Console Strumenti</a> fornisce l’accesso a console e strumenti specifici per la gestione dei siti web, delle risorse digitali e di altri aspetti dell’archivio dei contenuti.</td>
  </tr>
  <tr>
   <td><strong>Utenti</strong></td>
   <td>Queste console consentono di gestire i diritti di accesso di utenti e gruppi. Per maggiori dettagli, consulta <a href="/help/sites-administering/security.md">Amministrazione utenti e sicurezza</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Siti Web</strong></td>
   <td>Le console Siti/Siti Web consentono di: <a href="/help/sites-classic-ui-authoring/classic-page-author.md">creare, visualizzare e gestire siti Web</a> in esecuzione sull’istanza AEM. Tramite queste console puoi creare, copiare, spostare ed eliminare pagine web, avviare flussi di lavoro e attivare (pubblicare) pagine. Puoi anche aprire una pagina per la modifica.<br /> </td>
  </tr>
  <tr>
   <td><strong>Flussi di lavoro</strong></td>
   <td>Un flusso di lavoro è una serie definita di passaggi che descrivono il processo di completamento di alcune attività. In molti casi un certo numero di persone sono coinvolte in un'attività e ogni persona deve completare il proprio passaggio prima di consegnare il lavoro alla persona successiva. La console Flusso di lavoro consente di creare modelli di flusso di lavoro e gestire le istanze di flusso di lavoro in esecuzione. Consulta <a href="/help/sites-administering/workflows.md">Utilizzo dei flussi di lavoro</a>.<br /> </td>
  </tr>
 </tbody>
</table>

Il **Siti Web** console fornisce due riquadri per la navigazione e la gestione delle pagine:

* Riquadro sinistro

   Mostra la struttura ad albero dei siti Web e le pagine all&#39;interno di tali siti.

   Mostra anche informazioni su altri aspetti o AEM, inclusi progetti, progetti e risorse.

* Riquadro destro

   Mostra le pagine (nella posizione selezionata nel riquadro a sinistra) e può essere utilizzato per eseguire azioni.

Da qui puoi [gestire le pagine](/help/sites-authoring/managing-pages.md) utilizzando la barra degli strumenti, un menu di scelta rapida o aprendo una pagina per ulteriori azioni.

>[!NOTE]
>
>Le operazioni di base sono le stesse su tutte le console. Questa sezione si concentra sul **Siti Web** in quanto è la console principale utilizzata durante l’authoring.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Accedere all’Aiuto   {#accessing-help}

Su varie console (ad esempio siti web) è anche disponibile **Aiuto** disponibile, verrà aperto Condivisione pacchetti o il sito della documentazione.

![chlimage_1-10](assets/chlimage_1-10a.png)

Durante la modifica di una pagina, il [nella barra laterale è inoltre disponibile un pulsante per accedere all&#39;Aiuto](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navigazione con la console Siti web {#navigating-with-the-websites-console}

Il **Siti Web** in console le pagine di contenuto vengono elencate in una struttura ad albero (riquadro a sinistra). Per semplificare la navigazione, è possibile espandere (+) o comprimere (-) le sezioni della struttura ad albero come richiesto:

* Un singolo clic sul nome della pagina (nel riquadro a sinistra):

   * Elencare le pagine figlie nel riquadro di destra
   * Espandi inoltre la struttura nel riquadro a sinistra.

      Per motivi di prestazioni, questa azione dipende dal numero di nodi secondari. Con un&#39;installazione standard questo metodo di espansione funziona quando `30` o meno nodi secondari.

* Facendo doppio clic sul nome della pagina (riquadro a sinistra) si espanderà anche la struttura, anche se questo effetto non è così evidente quando la pagina viene aperta contemporaneamente.

>[!NOTE]
>
>Questo valore predefinito ( `30`) può essere modificata per console nelle configurazioni specifiche dell&#39;applicazione del widget siteadmin:
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
>Consulta [SiteAdmin nell’API del widget CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin) per ulteriori dettagli.

## Informazioni pagina nella console Siti web {#page-information-on-the-websites-console}

Riquadro destro della sezione **Siti Web** console fornisce una vista a elenco con informazioni sulle pagine:

![page-info](assets/page-info.png)

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
   <td>Pubblicazione Scene7</td>
   <td>Indica se la pagina è stata pubblicata in Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Stato</td>
   <td>Indica lo stato corrente della pagina, ad esempio se la pagina fa parte di un flusso di lavoro o di una Live Copy o se è attualmente bloccata.</td>
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
>Per selezionare le colonne visibili, posizionare il puntatore del mouse sul titolo di una colonna. Verrà visualizzato un menu a discesa, da qui puoi utilizzare il **Colonne** opzione.

I colori accanto alle pagine nel **Pubblicato** e **Modificato** le colonne indicano lo stato di pubblicazione:

| **Colonna** | **Colore** | **Descrizione** |
|---|---|---|
| Pubblicato | Verde | Pubblicazione completata. Il contenuto viene pubblicato. |
| Pubblicato | Giallo | Pubblicazione in sospeso. Il sistema non ha ancora ricevuto la conferma della pubblicazione. |
| Pubblicato | Rosso | Pubblicazione non riuscita. Non esiste alcuna connessione con l’istanza Publish. Questo può anche significare che il contenuto è stato disattivato. |
| Pubblicato | *blank* | Questa pagina non è mai stata pubblicata. |
| Modificato | Blu | La pagina è stata modificata dall&#39;ultima pubblicazione. |
| Modificato | *blank* | La pagina non è mai stata modificata o non è stata modificata dall&#39;ultima pubblicazione. |

## Menu di scelta rapida {#context-menus}

L’interfaccia classica utilizza meccanismi noti per la navigazione e l’avvio di azioni, tra cui il clic e il doppio clic. A seconda della situazione attuale, sono disponibili anche diversi menu di scelta rapida (solitamente aperti con il pulsante destro del mouse):

![chlimage_1-11](assets/chlimage_1-11a.png)
