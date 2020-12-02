---
title: Contenuto sandbox iniziale
seo-title: Contenuto sandbox iniziale
description: Crea contenuto
seo-description: Crea contenuto
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 5%

---


# Contenuto sandbox iniziale {#initial-sandbox-content}

In questa sezione vengono create le seguenti pagine che utilizzano tutte il modello di pagina [](initial-app.md#createthepagetemplate):

* Sito sandbox SCF, che verrà reindirizzato alla versione inglese della pagina principale.

   * SCF Sandbox - La pagina principale per la versione inglese del sito.

   * Riproduzione SCF - Elemento secondario della pagina principale in cui verrà riprodotta.

Sebbene questa esercitazione non contenga copie in [lingua](../../help/sites-administering/tc-prep.md), è progettata in modo che la pagina principale possa implementare il rilevamento della lingua preferita per l&#39;utente tramite l&#39;intestazione HTML e reindirizzare alla pagina principale appropriata per la lingua. La convenzione prevede l’uso del codice del paese di due lettere per il nome del nodo della pagina, ad esempio &quot;en&quot; per l’inglese, &quot;fr&quot; per il francese e così via.

## Crea prime pagine {#create-first-pages}

Ora che è presente un [modello di pagina](initial-app.md#createthepagetemplate), è possibile stabilire la pagina principale del sito Web nella directory /content.

1. L’interfaccia utente standard fornisce attualmente i modelli per la creazione di siti. Questa esercitazione consente di creare un sito semplice e l’interfaccia classica.

   Per passare all’interfaccia classica, selezionate la navigazione globale e passate il mouse sul lato destro dell’icona Progetti. Selezionate l&#39;icona *Passa all&#39;interfaccia classica* che viene visualizzata:

   ![classic-ui](assets/classic-ui.png)

   La possibilità di passare all&#39;interfaccia classica deve essere [abilitata da un amministratore](../../help/sites-administering/enable-classic-ui.md).

1. Dalla [pagina di benvenuto dell&#39;interfaccia classica](http://localhost:4502/welcome.html), selezionare **[!UICONTROL Siti Web]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   In alternativa, accedete direttamente all&#39;interfaccia classica per i siti Web visitando [/siteadmin.](http://localhost:4502/siteadmin)

1. Nel riquadro Esplora risorse, selezionare **[!UICONTROL Siti Web]**, quindi nella barra degli strumenti selezionare **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**.

   Nella finestra di dialogo **[!UICONTROL Crea pagina]**, immettere quanto segue:

   * Titolo: `SCF Sandbox Site`
   * Nome: `an-scf-sandbox`
   * Selezionare **[!UICONTROL un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. Nel riquadro Esplora risorse, selezionare la pagina appena creata, `/Websites/SCF Sandbox Site`, quindi fare clic su **[!UICONTROL Nuova]** > **[!UICONTROL Nuova pagina]**:

   * Titolo: `SCF Sandbox`
   * Nome: `en`
   * Selezionare **[!UICONTROL un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

1. Nel riquadro Esplora risorse, selezionare la pagina appena creata, `/Websites/SCF Sandbox Site/SCF Sandbox`, quindi fare clic su **[!UICONTROL Nuova]** > **[!UICONTROL Nuova pagina]**

   * Titolo: `SCF Play`
   * Nome: `play`
   * Selezionare **[!UICONTROL un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

1. Il sito Web ora viene visualizzato nella console Siti Web. Le pagine figlie dell&#39;elemento selezionato nel riquadro di esplorazione vengono visualizzate nel riquadro di destra in cui è possibile gestirle.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Questa è la visualizzazione archivio di ciò che è stato creato con lo strumento Sito Web e il modello:

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## Aggiungere il percorso di progettazione {#add-the-design-path}

Quando ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` è stato creato utilizzando la sezione delle progettazioni della console Strumenti, la proprietà &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

è stato definito, che fornisce la possibilità opzionale di fare riferimento alle risorse di progettazione in uno script utilizzando `currentDesign.getPath()`. Esempio

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nome: `cq:designPath`
   * Tipo: `String`
   * Valore: `/etc/designs/an-scf-sandbox`

* Fare clic sul verde `[+] Add`

Il repository deve essere visualizzato come segue:

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* Fare clic su **[!UICONTROL Salva tutto]**

In caso di problemi durante il salvataggio della configurazione, effettuate nuovamente l’accesso e configuratelo di nuovo.

>[!NOTE]
>
>L&#39;utilizzo di `cq:designPath` è facoltativo e non è correlato all&#39; [uso di clientlibs](develop-app.md#includeclientlibsintemplate), che sono essenzialmente necessari in quanto i componenti SCF utilizzano [clientlibs](client-customize.md#clientlibs-for-scf) per gestire i rispettivi JS e CSS.
