---
title: Pubblicazione delle pagine
seo-title: Publishing Pages
description: Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, devi renderli disponibili nel sito web pubblico.
seo-description: Once you have created and reviewed your content on the author environment, the goal is to make it available on your public website.
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 79%

---

# Pubblicazione delle pagine{#publishing-pages}

Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, devi renderli disponibili nel sito Web pubblico (l’ambiente di pubblicazione).

Questa operazione è denominata pubblicazione della pagina. Quando si rimuove una pagina dall’ambiente di pubblicazione, si parla di annullamento della pubblicazione. Quando si pubblica e si annulla la pubblicazione di una pagina, quest’ultima rimane disponibile nell’ambiente di authoring per ulteriori modifiche, finché non decidi di eliminarla.

Puoi pubblicare o annullare la pubblicazione di una pagina immediatamente o in una data/ora futura predefinita.

>[!NOTE]
>
>Alcuni termini correlati alla pubblicazione possono creare confusione:
>
>* **Pubblicare/Annullare la pubblicazione**
   >  Termini principali per le azioni che consentono di rendere o meno i contenuti disponibili al pubblico nell’ambiente di pubblicazione.
>
>* **Attivare/Disattivare**
   >  Sinonimi di pubblicare/annullare la pubblicazione.
>
>* **Replicare/Replica**
   >  Si tratta dei termini tecnici che descrivono lo spostamento di dati (ad esempio contenuto di pagina, file, codice, commenti degli utenti) da un ambiente all’altro, ad esempio per la pubblicazione o la replica inversa dei commenti degli utenti.
>


>[!NOTE]
>
>Se non disponi delle autorizzazioni necessarie per pubblicare una specifica pagina:
>
>* Viene avviato un flusso di lavoro per comunicare al soggetto adeguato la tua richiesta di pubblicazione.
>* Viene visualizzato brevemente un messaggio di notifica al riguardo.
>


## Pubblicazione di una pagina {#publishing-a-page}

Per attivare una pagina è possibile procedere in due modi:

* [dalla console Siti Web](#activating-a-page-from-the-websites-console)
* [dalla barra laterale nella pagina](#activating-a-page-from-sidekick)

>[!NOTE]
>
>È inoltre possibile attivare una struttura ad albero secondaria, composta da più pagine, utilizzando [Attiva albero](#howtoactivateacompletesectiontreeofyourwebsite) nella console Strumenti.

### Attivazione di una pagina dalla console Siti web {#activating-a-page-from-the-websites-console}

È possibile attivare le pagine dalla console Siti web. Dopo avere aperto una pagina e modificato il contenuto, torna alla console Siti web.

1. Nella console Siti web seleziona la pagina da attivare.
1. Seleziona **Attiva** nel menu principale o nel menu a discesa dell’elemento pagina selezionato.

   Per attivare il contenuto della pagina e di tutte le relative sottopagine, utilizza la console [**Strumenti**](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >Se necessario viene richiesto di attivare o riattivare tutte le risorse eventualmente collegate alla pagina. In questo caso seleziona o deseleziona le caselle di controllo per l’attivazione di tali risorse.

1. Se necessario viene richiesto di attivare o riattivare tutte le risorse eventualmente collegate alla pagina. In questo caso seleziona o deseleziona le caselle di controllo per l’attivazione di tali risorse.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. Il contenuto selezionato viene attivato in WCM AEM. Le pagine pubblicate vengono visualizzate in verde nella [console Siti web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console), con informazioni relative all’utente che ha attivato il contenuto e alla data/ora dell’attivazione.

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### Attivazione di una pagina dalla barra laterale {#activating-a-page-from-sidekick}

È inoltre possibile attivare la pagina quando viene aperta per la modifica.

Dopo avere aperto la pagina e modificato il contenuto:

1. Seleziona la scheda **Pagina** nella barra laterale.
1. Fai clic su **Attiva pagina**. Nella parte superiore destra della finestra viene visualizzato un messaggio di conferma dell’attivazione della pagina.

## Annullamento della pubblicazione di una pagina {#unpublishing-a-page}

Per rimuovere una pagina dall’ambiente di pubblicazione, è necessario disattivarne il contenuto.

Per disattivare la pagina:

1. Nella console Siti web seleziona la pagina da disattivare.
1. Seleziona **Disattiva** nel menu principale o nel menu a discesa dell’elemento pagina selezionato. Viene richiesto di confermare l’eliminazione.

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. Aggiorna la [console Siti web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). Il contenuto viene contrassegnato in rosso, per indicare che non è più pubblicato.

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## Attiva/Disattiva più tardi {#activate-deactivate-later}

### Attiva più tardi {#activate-later}

Per pianificare l’attivazione in un momento successivo:

1. Nella console Siti Web selezionate **Attiva più tardi** nel menu **Attiva**.
1. Nella la finestra di dialogo visualizzata specifica la data e l’ora dell’attivazione e fai clic su **OK**. Viene creata una versione della pagina che viene attivata al momento specificato.

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

Verrà avviato un flusso di lavoro per attivare tale versione della pagina alla data e all’ora specificate. In modo analogo, se scegli di eseguire la disattivazione in un secondo momento, verrà avviato un flusso di lavoro per disattivare tale versione della pagina alla data e all’ora specificate.

Per annullare questa attività di attivazione/disattivazione, accedi alla [console Flusso di lavoro](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) e interrompi il flusso di lavoro corrispondente.

### Disattiva più tardi {#deactivate-later}

Per pianificare la disattivazione in un momento successivo:

1. Nella console Siti Web passate alla **Disattiva** e seleziona **Disattiva più tardi**.

1. Nella la finestra di dialogo visualizzata specifica la data e l’ora della disattivazione e fai clic su **OK**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**Disattiva più tardi** avvia un flusso di lavoro che disattiva tale versione della pagina nel momento specificato.

Per annullare questa attività di disattivazione, accedi alla [console Flusso di lavoro](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) e interrompi il flusso di lavoro corrispondente.

## Attivazione/Disattivazione pianificata (ora di attivazione/disattivazione) {#scheduled-activation-deactivation-on-off-time}

Puoi pianificare il momento della pubblicazione o dell’annullamento della pubblicazione di una pagina tramite le opzioni **Ora di attivazione** e **Ora di disattivazione** nelle [Proprietà pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### Determinazione dello stato di pubblicazione di una pagina {#determining-page-publication-status-classic-ui}

Lo stato è visibile dalla [console Siti web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). I colori indicano lo stato di pubblicazione.

## Attivazione di una sezione (struttura ad albero) completa del sito web {#activating-a-complete-section-tree-of-your-website}

La scheda **Siti web** consente di attivare le singole pagine. Dopo avere inserito o aggiornato un numero considerevole di pagine di contenuto, tutte residenti sotto la stessa pagina principale, può essere più semplice attivare l’intero albero con una singola azione. Puoi anche eseguire una prova per simulare l’attivazione e identificare le pagine da attivare.

1. Apri **Strumenti** selezionando la console dalla **Benvenuto** e quindi fai doppio clic su **Replica** per aprire la console ( `https://localhost:4502/etc/replication.html`).

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. Nella console **Replica** fai clic su **Attiva albero**.

   La finestra seguente ( `https://localhost:4502/etc/replication/treeactivation.html`).

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. Inserisci il **Percorso iniziale**. Specifica il percorso della directory principale della sezione da attivare (pubblicare). Questa pagina e tutte le pagine sottostanti vengono considerate per l’attivazione o utilizzate per la simulazione, se è selezionata l’opzione Prova.
1. Attiva il criterio di selezione come necessario:

   * **Solo elementi modificati**: vengono attivate solo le pagine che sono state modificate.
   * **Solo elementi attivati**: vengono attivate solo le pagine che sono già state attivate in precedenza. Si tratta di una forma di riattivazione.
   * **Ignora elementi disattivati**: vengono ignorate tutte le pagine che sono state disattivate.

1. Seleziona l’azione da eseguire:

   1. Seleziona **Prova a secco** per controllare quali pagine *avrebbe* essere attivato. Questa è solo un&#39;emulazione, non verrà attivata alcuna pagina.

   1. Seleziona **Attiva** per attivare le pagine.
