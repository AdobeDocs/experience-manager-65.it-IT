---
title: Contenuto sandbox iniziale
description: Scopri come utilizzare il modello Pagina nella Sandbox per creare una pagina principale per una versione inglese di un sito web e una pagina figlia dalla pagina principale.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---

# Contenuto sandbox iniziale {#initial-sandbox-content}

In questa sezione vengono create le pagine seguenti che utilizzano tutte [modello pagina](initial-app.md#createthepagetemplate):

* Sito sandbox SCF, che reindirizza alla versione inglese della pagina principale.

   * SCF Sandbox: la pagina principale per la versione inglese del sito.

   * SCF Play: elemento secondario della pagina principale in cui eseguire la riproduzione.

Questa esercitazione non approfondisce [copie per lingua](../../help/sites-administering/tc-prep.md). È invece progettato in modo che la pagina principale possa implementare il rilevamento della lingua preferita per l’utente tramite l’intestazione HTML e reindirizzare alla pagina principale appropriata per la lingua. La convenzione prevede l’utilizzo del codice del paese di due lettere per il nome del nodo della pagina, ad esempio &quot;en&quot; per l’inglese e &quot;fr&quot; per il francese.

## Crea prime pagine {#create-first-pages}

Ora che c’è un [modello pagina](initial-app.md#createthepagetemplate), puoi stabilire la pagina root del sito web nella directory /content.

1. L’interfaccia utente standard fornisce attualmente i blueprint per la creazione di siti. Poiché questo tutorial sta creando un sito semplice, è utile l’interfaccia utente classica.

   Per passare all’interfaccia classica, seleziona la navigazione globale e passa il puntatore del mouse sul lato destro dell’icona Progetti. Seleziona la *Passa all’interfaccia classica* che viene visualizzata:

   ![classic-ui](assets/classic-ui.png)

   La possibilità di passare all’interfaccia classica deve essere [abilitato da un amministratore](../../help/sites-administering/enable-classic-ui.md).

1. Dalla sezione [pagina iniziale dell’interfaccia classica](http://localhost:4502/welcome.html), seleziona **[!UICONTROL Siti Web]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   In alternativa, puoi accedere direttamente all’interfaccia classica per i siti web navigando su [/siteadmin](http://localhost:4502/siteadmin)

1. Nel riquadro dell&#39;elenco delle cartelle selezionare **[!UICONTROL Siti Web]** e quindi nella barra degli strumenti seleziona **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**.

   In **[!UICONTROL Crea pagina]** immetti quanto segue:

   * Titolo: `SCF Sandbox Site`
   * Nome: `an-scf-sandbox`
   * Seleziona **[!UICONTROL Un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. Nel riquadro dell&#39;elenco delle cartelle selezionare la pagina creata. `/Websites/SCF Sandbox Site`e fai clic su **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**:

   * Titolo: `SCF Sandbox`
   * Nome: `en`
   * Seleziona **[!UICONTROL Un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

1. Nel riquadro dell&#39;elenco delle cartelle selezionare la pagina creata. `/Websites/SCF Sandbox Site/SCF Sandbox`e fai clic su **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**

   * Titolo: `SCF Play`
   * Nome: `play`
   * Seleziona **[!UICONTROL Un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

1. Questo è il modo in cui il sito web viene ora visualizzato nella console Siti web. Le pagine figlie dell&#39;elemento selezionato nel riquadro dell&#39;elenco delle cartelle vengono visualizzate nel riquadro di destra, dove possono essere gestite.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Questa è la visualizzazione dell’archivio di ciò che è stato creato utilizzando lo strumento Sito web e il modello:

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## Aggiungere il percorso di progettazione {#add-the-design-path}

Quando ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` è stato creato utilizzando la sezione progettazioni della console Strumenti, la proprietà &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

È stato definito, il che offre la possibilità facoltativa di fare riferimento alle risorse di progettazione in uno script utilizzando `currentDesign.getPath()`. Per esempio

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nome: `cq:designPath`
   * Tipo: `String`
   * Valore: `/etc/designs/an-scf-sandbox`

* Fai clic sul pulsante verde `[+] Add`

L’archivio dovrebbe essere visualizzato come segue:

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* Clic **[!UICONTROL Salva tutto]**

In caso di problemi durante il salvataggio della configurazione, effettua di nuovo l’accesso e configura di nuovo.

>[!NOTE]
>
>L&#39;uso di `cq:designPath` è facoltativo e non è correlato al [utilizzo di clientlibs](develop-app.md#includeclientlibsintemplate), necessari quando i componenti SCF utilizzano [clientlibs](client-customize.md#clientlibs-for-scf) per gestire JS e CSS.
