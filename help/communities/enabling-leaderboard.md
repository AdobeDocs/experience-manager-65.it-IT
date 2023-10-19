---
title: Funzione classifica
description: Scopri in che modo il componente Classifica consente di vedere come interagiscono i membri della community classificandoli in base ai punti ottenuti e alle competenze acquisite.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 9%

---

# Funzione classifica {#leaderboard-feature}

## Introduzione {#introduction}

Il `Leaderboard` Questo componente consente di comprendere in che modo i membri interagiscono all’interno della community, classificandoli in base ai punti ottenuti (punteggio di base) o alle loro competenze (punteggio avanzato).

Prima di includere il componente classifica in una pagina, è necessario configurare [Punteggio community e badge](/help/communities/implementing-scoring.md).

Questa sezione della documentazione descrive:

* Aggiunta di `Leaderboard` da componente a [sito community](/help/communities/overview.md#community-sites).
* Impostazioni di configurazione per `Leaderboard` componente.

### Aggiunta di una classifica a una pagina {#adding-a-leaderboard-to-a-page}

Per aggiungere una `Leaderboard` a una pagina in modalità di authoring, individua il componente

* `Communities / Leaderboard`

Trascinarlo nella posizione desiderata su una pagina.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

La prima volta che viene inserito in una pagina di un sito community, viene visualizzato questo componente:

![classifica](assets/leaderboard.png)

### Configurazione della classifica {#configuring-leaderboard}

Seleziona la inserita `Leaderboard` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configure-new](assets/configure-new.png)

![configure-lead board](assets/configure-leaderboard.png)

#### Scheda Impostazioni {#settings-tab}

Sotto **[!UICONTROL Impostazioni]** , specificare le informazioni relative al membro visualizzate:

* **Nome visualizzato**

  Nome descrittivo da visualizzare per la bacheca, che riflette le regole selezionate per la visualizzazione di badge e punteggi.
Il valore predefinito è `Leaderboard` se non viene immesso alcun valore.

* **Badge**

  Se questa opzione è selezionata, nella classifica verrà inclusa una colonna per le icone dei badge.
L&#39;impostazione predefinita è deselezionata.

* **Nome badge**

  Se questa opzione è selezionata, nella classifica viene inclusa una colonna per il nome del badge.
L&#39;impostazione predefinita è deselezionata.

* **Usa avatar**

  Se questa opzione è selezionata, l&#39;immagine avatar del membro viene inclusa nella classifica, accanto al collegamento del nome al suo profilo membro.
L&#39;impostazione predefinita è deselezionata.

#### Scheda Regole {#rules-tab}

Sotto **Regole** , il sito community e le relative regole di punteggio e badge

* **Percorso regola**

  (Obbligatorio) Posizione in cui è configurata la regola Punteggio/Distintivo.

* **Regola punteggio**

  (Obbligatorio) Regola specifica che genera i punteggi da visualizzare.

* **Regola assegnazione badge**

  (Obbligatorio) Regola specifica che genera il badge da visualizzare.

* **Limite di visualizzazione**

  Numero di membri da visualizzare per pagina. Il valore predefinito è 10.

### Esempio: classifica partecipanti {#example-participants-leaderboard}

Questa classifica riporta i risultati dell’applicazione delle regole di punteggio di base.

Configurazione componente classifica:

* Scheda Impostazioni:

   * Nome visualizzato = `Participation Board`
   * `checked`:

      * Badge
      * Nome badge
      * Usa avatar

* Scheda Regole:

   * Percorso regola = `/content/sites/<site name>/jcr:content`
   * Regola punteggio = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regola assegnazione badge = `/libs/settings/community/badging/rules//reference-badging`
   * Limite di visualizzazione = `10`

![Participanti-classifica](assets/participants-leaderboard.png)

### Esempio: classifica degli esperti {#example-experts-leaderboard}

Questa classifica riporta i risultati dell’applicazione di regole di punteggio avanzate.

Configurazione componente classifica:

* Scheda Impostazioni:

   * Nome visualizzato = `Expertise Board`
   * `checked`:

      * Badge
      * Usa avatar

* Scheda Regole:

   * Percorso regola = `/content/sites/<site name>/jcr:content`
   * Regola punteggio = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regola assegnazione badge = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite di visualizzazione = `10`

![esperti-classifica](assets/experts-leaderboard.png)

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sulla classifica](/help/communities/leaderboard.md) pagina per sviluppatori.

Le istruzioni per la creazione delle regole sono fornite nella [Punteggio community e badge](/help/communities/implementing-scoring.md) per gli amministratori.
