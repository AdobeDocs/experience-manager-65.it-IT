---
title: Configurazione dell’ambiente dell’account
description: Con AEM è possibile configurare il proprio account e alcuni aspetti dell’ambiente di authoring
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 63%

---

# Configurazione dell’ambiente dell’account  {#configuring-your-account-environment}

Con AEM è possibile configurare il proprio account e alcuni aspetti dell’ambiente di authoring.

Utilizza l’opzione [Utente](/help/sites-authoring/user-properties.md#user-settings) nell’[intestazione](/help/sites-authoring/basic-handling.md#the-header) e la relativa finestra di dialogo [Preferenze](#userpreferences) per modificare le opzioni utente.

Per prima cosa, accedi all’opzione [Utente](/help/sites-authoring/user-properties.md#user-settings) nell’intestazione.

## Impostazioni utente {#user-settings}

Le impostazioni **Utente** consentono di accedere a:

* Impersona

   * Con la funzionalità [Impersona come](/help/sites-administering/security.md#impersonating-another-user) un utente può lavorare per conto di un altro utente.

* Profilo

   * Offre un collegamento semplice alle [impostazioni utente](/help/sites-administering/security.md))

* [Preferenze](/help/sites-authoring/user-properties.md#my-preferences)

   * Consente di specificare varie preferenze di impostazione specifiche dell’utente.

![schermata_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### Preferenze {#my-preferences}

Puoi accedere alla finestra di dialogo **Preferenze** tramite l’opzione [Utente](/help/sites-authoring/user-properties.md#user-settings) nell’intestazione.

Ogni utente può impostare autonomamente determinate proprietà.

![schermata_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **Lingua**

  Consente di definire la lingua da usare nell’interfaccia dell’ambiente di authoring. Seleziona la lingua desiderata dall’elenco disponibile.

  Questa configurazione viene utilizzata anche per l’interfaccia classica.

* **Gestione finestre**

  Ciò definisce il comportamento o l’apertura delle finestre. Puoi selezionare:

   * **Finestre multiple** (predefinito)

      * Le pagine vengono aperte in una nuova finestra.

   * **Finestra singola**

      * Le pagine vengono aperte nella finestra corrente.

* **Mostra azioni desktop per Assets**

  Questa opzione richiede l’utilizzo di un’app desktop AEM.

* **Colore annotazione**

  Definisce il colore predefinito utilizzato per le annotazioni.

   * Fai clic sul blocco di colori per aprire il selettore di campioni e selezionare un colore.
   * In alternativa, immetti nel campo il codice esadecimale del colore desiderato.

* **Presentazione data relativa**

  Per migliorare la leggibilità, AEM riproduce le date degli ultimi sette giorni come date relative (ad esempio, Tre giorni fa) e le date più lontane come date esatte (ad esempio, 20 marzo 2017).

  Questa opzione definisce il modo in cui il sistema visualizza le date. Sono disponibili le seguenti opzioni:

   * **Mostra sempre data esatta**: viene sempre visualizzata la data esatta e non una data relativa.
   * **1 giorno**: viene visualizzata la data relativa per le date entro un giorno; in caso contrario viene visualizzata una data esatta.

   * **7 giorni (impostazione predefinita)**: viene visualizzata la data relativa per date entro sette giorni; in caso contrario viene visualizzata una data esatta.

   * **1 mese**: viene visualizzata la data relativa per le date entro un mese; in caso contrario viene visualizzata una data esatta.

   * **1 anno**: viene visualizzata la data relativa per le date entro un anno; in caso contrario viene visualizzata una data esatta.

   * **Mostra sempre data relativa**: non vengono mai visualizzate date esatte, ma solo date relative.

* **Abilita scelte rapide**

  AEM supporta diverse scelte rapide da tastiera per rendere più efficiente l’authoring.

   * [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [Scelte rapide da tastiera per le console](/help/sites-authoring/keyboard-shortcuts.md)

  Questa opzione abilita le scelte rapide da tastiera. Per impostazione predefinita sono abilitate, ma possono essere disabilitate, ad esempio, se un utente ha determinati requisiti di accessibilità.

* **Usa esperienza di authoring classica**

  Questa opzione abilita l&#39;authoring delle pagine basato su [interfaccia utente classica](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md). Per impostazione predefinita viene utilizzata l’interfaccia utente standard.

* **Abilita pagina iniziale di Assets**

  Questa opzione è disponibile solo se l’amministratore di sistema ha abilitato l’esperienza Pagina iniziale di Assets per l’intera organizzazione.

* **Configurazione Stock**

  Questa opzione consente di specificare la configurazione di Adobe Stock preferita ed è disponibile solo se l&#39;amministratore di sistema ha abilitato l&#39;[integrazione di Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
