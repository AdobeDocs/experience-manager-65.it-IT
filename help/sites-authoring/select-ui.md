---
title: Selezione dell’interfaccia utente in AEM
description: Configurare l’interfaccia utilizzata per lavorare in Adobe Experience Manager 6.5.
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# Selezione dell’interfaccia utente{#selecting-your-ui}

L’interfaccia utente touch di Adobe Experience Manager (AEM) è ora l’interfaccia utente standard e la parità di funzioni è stata quasi raggiunta con l’amministrazione e la modifica dei siti. Tuttavia, in alcuni casi l’utente desidera passare al [interfaccia classica](/help/sites-classic-ui-authoring/classicui.md). Sono disponibili diverse opzioni per eseguire questa operazione.

>[!NOTE]
>
>Per informazioni dettagliate sullo stato della parità delle funzioni con l’interfaccia classica, vedi [Parità delle funzioni dell’interfaccia touch](/help/release-notes/touch-ui-features-status.md) documento.

Puoi definire l’interfaccia utente da utilizzare in diverse posizioni:

* [Configurazione dell’interfaccia utente predefinita per l’istanza](#configuring-the-default-ui-for-your-instance)
Imposta l&#39;interfaccia utente predefinita da mostrare all&#39;accesso dell&#39;utente. L’utente potrebbe ignorare questa impostazione e selezionare un’interfaccia utente diversa per il proprio account o per la sessione corrente.

* [Impostazione dell’authoring dell’interfaccia classica per l’account](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Questa impostazione imposta l’interfaccia utente predefinita per la modifica delle pagine, anche se l’utente può ignorarla e selezionare un’interfaccia diversa per il proprio account o per la sessione corrente.

* [Passare all’interfaccia classica per la sessione corrente](#switching-to-classic-ui-for-the-current-session)
Passa all&#39;interfaccia classica per la sessione corrente.

* Nel caso di [nell’authoring delle pagine, il sistema effettua alcune sostituzioni in relazione all’interfaccia utente](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Le varie opzioni per passare all’interfaccia utente classica non sono immediatamente disponibili come predefinite, ma devono essere configurate per la tua istanza.
>
>Consulta [Abilitazione dell’accesso all’interfaccia classica](/help/sites-administering/enable-classic-ui.md) per ulteriori informazioni.

>[!NOTE]
>
>Le istanze aggiornate da una versione precedente mantengono l’interfaccia utente classica per l’authoring delle pagine.
>
>Dopo l’aggiornamento, l’authoring delle pagine non passa automaticamente all’interfaccia touch, ma puoi configurarlo utilizzando [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio). Consulta [Sostituzioni dell’interfaccia utente per l’editor](#ui-overrides-for-the-editor).

## Configurazione dell’interfaccia utente predefinita per l’istanza {#configuring-the-default-ui-for-your-instance}

Un amministratore di sistema può configurare l’interfaccia utente visualizzata all’avvio e all’accesso utilizzando [Mappatura radice](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Questo può essere ignorato dai valori predefiniti dell&#39;utente o dalle impostazioni di sessione.

## Impostazione dell’authoring dell’interfaccia classica per l’account {#setting-classic-ui-authoring-for-your-account}

Ogni utente può accedere ai propri [preferenze utente](/help/sites-authoring/user-properties.md#userpreferences) per definire se si desidera utilizzare l’interfaccia classica per la creazione delle pagine, anziché quella predefinita.

Questo può essere ignorato dalle impostazioni di sessione.

## Passaggio all’interfaccia classica per la sessione corrente {#switching-to-classic-ui-for-the-current-session}

Quando si utilizza l’interfaccia touch, gli utenti desktop potrebbero voler ripristinare l’interfaccia classica (solo desktop). Esistono diversi metodi per passare all’interfaccia utente classica per la sessione corrente:

* **Collegamenti di navigazione**

  >[!CAUTION]
  >
  >Questa opzione per passare all’interfaccia classica non è immediatamente disponibile come strumento predefinito, ma deve essere configurata per la tua istanza.
  >
  >
  >Consulta [Abilitazione dell’accesso all’interfaccia classica](/help/sites-administering/enable-classic-ui.md) per ulteriori informazioni.

  Se questa opzione è attivata, ogni volta che si passa il mouse su una console applicabile, viene visualizzata un&#39;icona (un simbolo di monitor). Toccando/facendo clic su questo pulsante si apre la posizione appropriata nell’interfaccia classica.

  Ad esempio, i collegamenti da **Sites** a **siteadmin**:

  ![syui-01](assets/syui-01.png)

* **URL**

  È possibile accedere all’interfaccia classica utilizzando l’URL per la schermata di benvenuto all’indirizzo `welcome.html`. Ad esempio:

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >L’interfaccia touch è accessibile tramite `sites.html`. Ad esempio:
  >
  >
  >`https://localhost:4502/sites.html`

### Passare all’interfaccia classica durante la modifica di una pagina {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Questa opzione per passare all’interfaccia classica non è immediatamente disponibile come strumento predefinito, ma deve essere configurata per la tua istanza.
>
>Consulta [Abilitazione dell’accesso all’interfaccia classica](/help/sites-administering/enable-classic-ui.md) per ulteriori informazioni.

Se attivato, **Aprire l’interfaccia classica** è disponibile da **Informazioni pagina** finestra di dialogo:

![syui-02](assets/syui-02.png)

### Sostituzioni dell’interfaccia utente per l’editor {#ui-overrides-for-the-editor}

Le impostazioni definite da un utente o da un amministratore di sistema possono essere ignorate dal sistema in caso di authoring delle pagine.

* Durante l’authoring delle pagine:

   * L’utilizzo dell’editor classico viene forzato quando si accede alla pagina utilizzando `cf#` nell’URL. Ad esempio:
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * L’utilizzo dell’editor touch viene forzato quando si utilizza `/editor.html` nell’URL o quando si utilizza un dispositivo touch. Ad esempio:
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Qualsiasi forzatura è temporanea e valida solo per la sessione del browser

   * Un set di cookie viene impostato a seconda che sia abilitato al tocco ( `editor.html`) o classico ( `cf#`).

* Quando si aprono le pagine tramite `siteadmin`, viene verificata l&#39;esistenza dei seguenti elementi:

   * Il cookie
   * Preferenza utente
   * Se non esiste, per impostazione predefinita vengono impostate le definizioni [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) del **Servizio modalità interfaccia utente di authoring WCM** ( `AuthoringUIMode` servizio).

>[!NOTE]
>
>Se [un utente ha già definito una preferenza per l’authoring delle pagine](#settingthedefaultauthoringuiforyouraccount), che non viene ignorato modificando la proprietà OSGi.

>[!CAUTION]
>
>A causa dell’utilizzo di cookie, come già descritto, non è consigliabile:
>
>* Modifica manualmente l’URL: un URL non standard potrebbe causare una situazione sconosciuta e la mancanza di funzionalità.
>* Avere entrambi gli editor aperti contemporaneamente, ad esempio in finestre separate.
