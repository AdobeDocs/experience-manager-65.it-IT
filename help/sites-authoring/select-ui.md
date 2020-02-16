---
title: Selezione dell’interfaccia
seo-title: Selezione dell’interfaccia
description: Configura l’interfaccia da utilizzare per lavorare in AEM
seo-description: Configura l’interfaccia da utilizzare per lavorare in AEM
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Selezione dell’interfaccia{#selecting-your-ui}

Sebbene l’interfaccia touch ora è l’interfaccia utente standard, ed è stata quasi raggiunta la parità di funzionalità per l’amministrazione e la modifica dei siti, in alcune situazioni può essere utile passare all’[interfaccia classica](/help/sites-classic-ui-authoring/classicui.md). Sono disponibili diverse opzioni per eseguire questa operazione.

>[!NOTE]
>
>Per informazioni sullo stato delle funzioni disponibili rispetto all’interfaccia classica, consulta il documento [Stato delle funzioni nell’interfaccia touch](/help/release-notes/touch-ui-features-status.md).

È possibile definire l’interfaccia utente da usare in diverse aree:

* [Configurazione dell’interfaccia utente predefinita per la propria istanza](#configuring-the-default-ui-for-your-instance) Questo consente di impostare l’interfaccia utente predefinita da visualizzare quando l’utente effettua l’accesso. Tuttavia, l’utente può selezionare una diversa interfaccia per il proprio account o la sessione corrente.

* [Impostazione dell’interfaccia utente di authoring classica per il tuo account](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)  Imposta l’interfaccia utente predefinita per la modifica delle pagine. L’utente può selezionare una diversa interfaccia per il proprio account o per la sessione corrente.

* [Passaggio all’interfaccia classica per la sessione corrente](#switching-to-classic-ui-for-the-current-session) Consente di passare all’interfaccia classica per la sessione corrente.

* Per l’[authoring delle pagine il sistema implementa alcune impostazioni locali in base all’interfaccia utente](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Le diverse opzioni per passare all’interfaccia utente classica non sono immediatamente disponibili, ma devono essere configurate specificamente per l’istanza.
>
>See [Enabling Access to Classic UI](/help/sites-administering/enable-classic-ui.md) for more information.

>[!NOTE]
>
>Nelle istanze aggiornate da una versione precedente viene mantenuta l’interfaccia classica per la creazione e la modifica delle pagine.
>
>After upgrade, page authoring will not be automatically switched to the touch-enabled UI, but you can configure this using the [OSGi configuration](/help/sites-deploying/configuring-osgi.md) of the **WCM Authoring UI Mode Service** ( `AuthoringUIMode` service). Vedi [Ignorare le impostazioni dell’interfaccia per l’editor](#ui-overrides-for-the-editor).

## Configuring the Default UI for Your Instance {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l’interfaccia utente utilizzata all’avvio e all’accesso utilizzando la [mappatura della directory principale](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Tale impostazione può essere ignorata e sostituita dalle impostazioni predefinite dell’utente o dalle impostazioni della sessione.

## Impostazione della creazione nell’interfaccia classica del tuo account {#setting-classic-ui-authoring-for-your-account}

Ogni utente può accedere alle proprie [preferenze](/help/sites-authoring/user-properties.md#userpreferences) per definire se desidera utilizzare l’interfaccia classica per la creazione delle pagine (invece dell’interfaccia utente predefinita).

Tale impostazione può essere ignorata e sostituita dalle impostazioni della sessione.

## Passaggio all’interfaccia classica per la sessione corrente {#switching-to-classic-ui-for-the-current-session}

Gli utenti desktop possono passare dall’interfaccia touch all’interfaccia classica (solo per desktop). Esistono diversi metodi per passare all’interfaccia classica per la sessione corrente:

* **Collegamenti di navigazione**

   >[!CAUTION]
   >
   >Questa opzione per passare all’interfaccia utente classica non è immediatamente disponibile e deve essere configurata in modo specifico per l’istanza.
   >
   >
   >See [Enabling Access to Classic UI](/help/sites-administering/enable-classic-ui.md) for more information.

   Se questa funzione è abilitata, ogni volta che passi il mouse su una console applicabile viene visualizzata un’icona (simbolo di un monitor); tocca o fai clic su tale icona per aprire la sezione corrispondente nell’interfaccia classica.

   Ad esempio, i collegamenti da **Sites** permettono di passare all’**amministrazione del sito**:

   ![syui-01](assets/syui-01.png)

* **URL**

   The classic UI can be accessed using the URL for the welcome screen at `welcome.html`. For example:

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >L’interfaccia touch è accessibile tramite `sites.html`. Esempio:
   >
   >
   >`https://localhost:4502/sites.html`

### Passaggio all’interfaccia classica durante la modifica di una pagina {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Questa opzione per passare all’interfaccia utente classica non è immediatamente disponibile e deve essere configurata in modo specifico per l’istanza.
>
>See [Enabling Access to Classic UI](/help/sites-administering/enable-classic-ui.md) for more information.

Se abilitata, la voce **Apri interfaccia utente classica** è disponibile nella finestra di dialogo **Informazioni pagina**:

![syui-02](assets/syui-02.png)

### UI Overrides for the Editor {#ui-overrides-for-the-editor}

Per l’authoring delle pagine, le impostazioni definite da un utente o amministratore di sistema possono essere ignorate e sostituite dal sistema.

* Durante la creazione di pagine:

   * Use of the classic editor is forced when accessing the page using `cf#` in the URL. Esempio:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Use of the touch-enabled editor is forced when using `/editor.html` in the URL or when using a touch device. Esempio:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Tale comportamento forzato è temporaneo e valido solo per la sessione del browser.

   * A cookie set will be set dependent on whether touch-enabled ( `editor.html`) or classic ( `cf#`) is used.

* Quando si aprono pagine tramite `siteadmin`, viene verificato se i seguenti elementi sono presenti:

   * il cookie
   * una preferenza utente
   * Se non vengono trovati, verranno utilizzate le definizioni impostate nella [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **servizio WCM per la modalità dell’interfaccia di authoring** (`AuthoringUIMode`).

>[!NOTE]
>
>Se [un utente ha già definito una preferenza per l’authoring delle pagine](#settingthedefaultauthoringuiforyouraccount), questa non viene esclusa se si modifica la proprietà OSGi.

>[!CAUTION]
>
>A causa dell’utilizzo dei cookie, come descritto qui sopra, si consiglia di:
>
>* NON modificare manualmente l’URL; un URL non standard potrebbe dare luogo a una situazione sconosciuta e alla perdita di funzionalità;
>* NON tenere entrambi gli editor aperti allo stesso tempo, ad esempio in due diverse finestre.

