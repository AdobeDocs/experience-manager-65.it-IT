---
title: Selezione dell’interfaccia utente in AEM
description: Configura l'interfaccia utilizzata per lavorare in AEM.
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# Selezione dell’interfaccia utente{#selecting-your-ui}

Sebbene l’interfaccia touch sia ora l’interfaccia utente standard e la parità delle funzioni sia quasi raggiunta con l’amministrazione e la modifica dei siti, in alcuni casi l’utente potrebbe voler passare alla [interfaccia classica](/help/sites-classic-ui-authoring/classicui.md). Ci sono diverse opzioni per farlo.

>[!NOTE]
>
>Per informazioni sullo stato delle funzioni di parità con l’interfaccia classica, consulta la sezione [Parità delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md) documento.

Puoi definire quale interfaccia utente usare in diverse aree:

* [Configurazione dell’interfaccia utente predefinita per l’istanza](#configuring-the-default-ui-for-your-instance)
Questo consente di impostare l’interfaccia utente predefinita da visualizzare all’accesso dell’utente, anche se l’utente può eseguire questa operazione e selezionare una diversa interfaccia per il proprio account o la sessione corrente.

* [Impostazione dell’authoring dell’interfaccia classica per il tuo account](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Questo consente di impostare l’interfaccia utente predefinita per la modifica delle pagine, anche se l’utente può selezionare una diversa interfaccia per il proprio account o la sessione corrente.

* [Passaggio all’interfaccia classica per la sessione corrente](#switching-to-classic-ui-for-the-current-session)
Consente di passare all’interfaccia classica per la sessione corrente.

* Per quanto riguarda [l’authoring delle pagine nel sistema implementa alcune impostazioni locali in relazione all’interfaccia utente](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Le varie opzioni per passare all’interfaccia classica non sono immediatamente disponibili e devono essere configurate in modo specifico per l’istanza in uso.
>
>Vedi [Abilitazione dell’accesso all’interfaccia classica](/help/sites-administering/enable-classic-ui.md) per ulteriori informazioni.

>[!NOTE]
>
>Le istanze aggiornate da una versione precedente manterranno l’interfaccia classica per la creazione delle pagine.
>
>Dopo l’aggiornamento, l’authoring delle pagine non passa automaticamente all’interfaccia touch, ma puoi configurarlo utilizzando l’ [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio). Vedi [Ignorare le impostazioni dell’interfaccia per l’editor](#ui-overrides-for-the-editor).

## Configurazione dell’interfaccia utente predefinita per la tua istanza {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l’interfaccia utente visualizzata all’avvio e all’accesso utilizzando [Mappatura radice](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Questo valore può essere ignorato dalle impostazioni predefinite dell’utente o dalle impostazioni della sessione.

## Impostazione dell’authoring dell’interfaccia classica per il tuo account {#setting-classic-ui-authoring-for-your-account}

Ogni utente può accedere alle proprie [preferenze utente](/help/sites-authoring/user-properties.md#userpreferences) per definire se utilizzare l’interfaccia classica per la creazione delle pagine (anziché l’interfaccia predefinita).

Questo può essere ignorato dalle impostazioni della sessione.

## Passaggio all’interfaccia classica per la sessione corrente {#switching-to-classic-ui-for-the-current-session}

Gli utenti desktop possono passare dall’interfaccia touch all’interfaccia classica (solo per desktop). Esistono diversi metodi per passare all’interfaccia classica per la sessione corrente:

* **Collegamenti di navigazione**

   >[!CAUTION]
   >
   >Questa opzione per passare all’interfaccia classica non è immediatamente disponibile, ma deve essere configurata in modo specifico per la tua istanza.
   >
   >
   >Vedi [Abilitazione dell’accesso all’interfaccia classica](/help/sites-administering/enable-classic-ui.md) per ulteriori informazioni.

   Se questa opzione è abilitata, ogni volta che passi il mouse su una console applicabile viene visualizzata un’icona (simbolo di un monitor); toccando o facendo clic su di essa si aprirà la posizione appropriata nell’interfaccia classica.

   Ad esempio, i collegamenti da **Sites** a **siteadmin**:

   ![syui-01](assets/syui-01.png)

* **URL**

   È possibile accedere all’interfaccia classica tramite l’URL della schermata di benvenuto all’indirizzo `welcome.html`. Ad esempio:

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >L’interfaccia touch è accessibile tramite `sites.html`. Ad esempio:
   >
   >
   >`https://localhost:4502/sites.html`

### Passaggio all’interfaccia classica durante la modifica di una pagina {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Questa opzione per passare all’interfaccia classica non è immediatamente disponibile, ma deve essere configurata in modo specifico per la tua istanza.
>
>Vedi [Abilitazione dell’accesso all’interfaccia classica](/help/sites-administering/enable-classic-ui.md) per ulteriori informazioni.

Se attivato, **Apri l’interfaccia classica** è disponibile dal **Informazioni pagina** finestra di dialogo:

![syui-02](assets/syui-02.png)

### Ignorare le impostazioni dell’interfaccia per l’editor {#ui-overrides-for-the-editor}

Le impostazioni definite da un utente o amministratore di sistema possono essere ignorate dal sistema nel caso di authoring delle pagine.

* Durante l’authoring delle pagine:

   * Viene forzato l’utilizzo dell’editor classico quando si accede alla pagina utilizzando `cf#` nell’URL. Ad esempio:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Viene forzato l’utilizzo dell’editor touch quando si utilizza `/editor.html` nell’URL o quando si utilizza un dispositivo touch. Ad esempio:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Qualsiasi forzatura è temporanea e valida solo per la sessione del browser

   * Viene impostato un cookie a seconda che sia abilitato o meno il tocco ( `editor.html`) o classica ( `cf#`).

* Quando si aprono le pagine attraverso `siteadmin`, si verificherà l&#39;esistenza di:

   * Il cookie
   * Una preferenza utente
   * Se non esistono, verrà utilizzata per impostazione predefinita le definizioni impostate in [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio).

>[!NOTE]
>
>Se [un utente ha già definito una preferenza per l’authoring delle pagine](#settingthedefaultauthoringuiforyouraccount), che non verrà ignorato modificando la proprietà OSGi.

>[!CAUTION]
>
>A causa dell’uso dei cookie, come già descritto, si sconsiglia di:
>
>* Modifica manuale dell’URL: un URL non standard potrebbe causare una situazione sconosciuta e la mancanza di funzionalità.
>* NON tenere entrambi gli editor aperti allo stesso tempo, ad esempio in due diverse finestre.

