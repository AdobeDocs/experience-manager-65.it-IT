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
source-git-commit: c798eb79dc9f8e58cef86cf90af02622c3a2ed78
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 6%

---


# Contenuto sandbox iniziale {#initial-sandbox-content}

In questa sezione vengono create le seguenti pagine che utilizzano tutte il modello [di](initial-app.md#createthepagetemplate)pagina:

* Sito sandbox SCF, che verrà reindirizzato alla versione inglese della pagina principale.

   * SCF Sandbox - La pagina principale per la versione inglese del sito.

   * Riproduzione SCF - Elemento secondario della pagina principale in cui verrà riprodotta.

Sebbene questa esercitazione non contenga copie [della](../../help/sites-administering/tc-prep.md)lingua, è progettata in modo che la pagina principale possa implementare il rilevamento della lingua preferita per l’utente tramite l’intestazione HTML e reindirizzare alla pagina principale appropriata per la lingua. La convenzione prevede l’uso del codice del paese di due lettere per il nome del nodo della pagina, ad esempio &quot;en&quot; per l’inglese, &quot;fr&quot; per il francese e così via.

## Crea prime pagine {#create-first-pages}

Ora che è presente un modello [di](initial-app.md#createthepagetemplate)pagina, possiamo stabilire la pagina principale del sito Web nella directory /content.

1. L’interfaccia utente standard fornisce attualmente i modelli per la creazione di siti. Questa esercitazione consente di creare un sito semplice e l’interfaccia classica.

   Per passare all’interfaccia classica, selezionate la navigazione globale e passate il mouse sul lato destro dell’icona Progetti. Selezionate l’icona *Passa all’interfaccia* classica visualizzata:

   ![chlimage_1-36](assets/chlimage_1-36.png)

   La possibilità di passare all’interfaccia classica deve essere [abilitata da un amministratore](../../help/sites-administering/enable-classic-ui.md).

1. Nella pagina [di benvenuto dell’interfaccia](http://localhost:4502/welcome.html)classica, selezionate **[!UICONTROL Siti Web]**.

   ![chlimage_1-37](assets/chlimage_1-37.png)

   In alternativa, potete accedere direttamente all’interfaccia classica per i siti Web accedendo direttamente a [/siteadmin.](http://localhost:4502/siteadmin)

1. Nel riquadro Esplora risorse, selezionate **[!UICONTROL Siti]** Web, quindi nella barra degli strumenti selezionate **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**.

   Nella finestra di dialogo **[!UICONTROL Crea pagina]** , immettete quanto segue:

   * Titolo: `SCF Sandbox Site`
   * Nome: `an-scf-sandbox`
   * Selezionare **[!UICONTROL un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Nel riquadro Esplora risorse, selezionate la pagina appena creata `/Websites/SCF Sandbox Site`e fate clic su **[!UICONTROL Nuova]** > **[!UICONTROL Nuova pagina]**:

   * Titolo: `SCF Sandbox`
   * Nome: `en`
   * Selezionare **[!UICONTROL un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

1. Nel riquadro Esplora risorse, selezionate la pagina appena creata `/Websites/SCF Sandbox Site/SCF Sandbox`e fate clic su **[!UICONTROL Nuova]** > **[!UICONTROL Nuova pagina]**

   * Titolo: `SCF Play`
   * Nome: `play`
   * Selezionare **[!UICONTROL un modello di riproduzione sandbox SCF]**
   * Fai clic su **[!UICONTROL Crea]**

1. Il sito Web ora viene visualizzato nella console Siti Web. Le pagine figlie dell&#39;elemento selezionato nel riquadro di esplorazione vengono visualizzate nel riquadro di destra in cui è possibile gestirle.

   ![chlimage_1-39](assets/chlimage_1-39.png)

   Questa è la visualizzazione archivio di ciò che è stato creato con lo strumento Sito Web e il modello:

   ![chlimage_1-40](assets/chlimage_1-40.png)

## Aggiungere il percorso di progettazione {#add-the-design-path}

Quando ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` è stata creata utilizzando la sezione delle progettazioni della console Strumenti, la proprietà &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

è stato definito, che fornisce la possibilità facoltativa di fare riferimento alle risorse di progettazione in uno script utilizzando `currentDesign.getPath()`. Ad esempio

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nome: `cq:designPath`
   * Tipo: `String`
   * Valore: `/etc/designs/an-scf-sandbox`

* Fare clic sul verde `[+] Add`

Il repository deve essere visualizzato come segue:

![chlimage_1-41](assets/chlimage_1-41.png)

* Fate clic su **[!UICONTROL Salva tutto]**

In caso di problemi durante il salvataggio della configurazione, effettuate nuovamente l’accesso e configuratelo di nuovo.

>[!NOTE]
>
>L’utilizzo di `cq:designPath` è facoltativo e non è correlato all’ [utilizzo di clientlibs](develop-app.md#includeclientlibsintemplate), che sono essenzialmente necessari in quanto i componenti SCF utilizzano [clientlibs](client-customize.md#clientlibs-for-scf) per gestire i rispettivi JS e CSS.


