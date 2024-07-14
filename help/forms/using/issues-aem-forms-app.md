---
title: Risolvere i problemi relativi all’app AEM Forms
description: Scopri i problemi comuni dell’app AEM Forms e come risolverli.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Risolvere i problemi relativi all’app AEM Forms {#troubleshoot-aem-forms-app}

Questo articolo descrive i messaggi di errore che potrebbero essere visualizzati durante la creazione dell’app AEM Forms e i passaggi per risolverli.

Le sezioni in questo articolo includono:

* [Perdita di allegati per utenti iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Le bozze dei moduli di HTML5 inviate dagli utenti dell’area di lavoro non sono visibili nel portale](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Impossibile caricare i moduli HTML5 (non memorizzati in cache) nell’app AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms do not sync on Windows (Non sincronizzare su Windows)](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versione di Gradle non supportata](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemi di compatibilità del plug-in Gradle e Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perdita di allegati per utenti iOS {#attachment-loss-for-ios-users}

L’app AEM Forms per iOS configurata per la sincronizzazione con AEM Forms su OSGi supporta solo allegati a livello di campo. Tutti gli allegati devono avere nomi univoci. Se più allegati hanno lo stesso nome, viene conservato un solo allegato e tutti gli altri con lo stesso nome vengono persi. Per evitare che gli utenti dei dispositivi iOS subiscano una perdita di dati, effettua le seguenti operazioni:

1. Nel server connesso passare a **Adobe Experience Manager > Strumenti > Operazioni > Console Web**.
1. Trova e fai clic su **[!UICONTROL Configurazione canale web per modulo adattivo e comunicazione interattiva]**.
1. Nella finestra di dialogo [!UICONTROL Configurazione canale Web modulo adattivo e comunicazione interattiva], abilita **Nomi file univoci**.

   Se l&#39;impostazione **Rendi nomi file univoci** è disabilitata, gli utenti perderanno dati se tenteranno di inviare moduli adattivi con più allegati.

1. Fai clic su **Salva**.

## Le bozze dei moduli di HTML5 inviate dagli utenti dell’area di lavoro non sono visibili nel portale {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Per i moduli HTML5 abilitati nell&#39;app AEM Forms con **Salva come bozza** profilo di rendering HTML, le bozze salvate non sono visibili agli utenti dell&#39;area di lavoro. Per visualizzare le bozze salvate dei moduli HTML5 inviati dagli utenti del workspace sul portale, effettuare le seguenti operazioni:

1. Apri CRXDE e accedi con le credenziali di amministratore.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Nel percorso radice di CRXDE, nell&#39;elenco di controllo di accesso in Controllo di accesso, fare clic su **+**.
1. Nella finestra di dialogo **Aggiungi nuova voce**, fai clic sul pulsante di ricerca del gruppo nel campo Principal.
1. Nel campo Nome della finestra di dialogo Seleziona entità, digitare `PERM_WORKSPACE_USER` e fare clic su **Cerca**.
1. Selezionare il gruppo `PERM_WORKSPACE_USER` nella finestra di dialogo Seleziona entità e fare clic su **OK**.
1. Nella finestra di dialogo Aggiungi nuova voce, il gruppo `PERM_WORKSPACE_USER` è selezionato nel campo Principal.

   Abilita i privilegi `jcr:read` per il gruppo di utenti.

1. Fai clic su **OK**.

## Impossibile caricare i moduli HTML5 (non memorizzati in cache) nell’app AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando l’app AEM Forms è connessa a una versione precedente del server AEM Forms, i moduli HTML5 non memorizzati nella cache non vengono caricati nell’app AEM Forms.

Per risolvere il problema, effettua le seguenti operazioni:

1. Nell&#39;istanza di authoring, passa a **Adobe Experience Manager > Strumenti > Configura servizio offline app Workspace > Configura ora**.
1. Nella pagina **Servizio offline app Workspace**, fare clic su **Cache risorse manuale**.

   URL: https://&lt;server>:&lt;porta>/libs/fd/workspace-offline/content/config.html

1. Nella scheda **Cache risorse manuale**, fare clic sul pulsante **+** per aggiungere un percorso CRX.
1. Nel campo **Aggiungi nuova risorsa** digitare: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e fare clic su **Aggiungi**.
1. Fai clic su **Salva**.

## AEM Forms do not sync on Windows (Non sincronizzare su Windows) {#aem-forms-do-not-sync-on-windows}

Nell’app AEM Forms su Windows, un modulo non viene sincronizzato con il server connesso se il percorso del modulo o una delle relative risorse contiene più di 256 caratteri o meno.

Modifica il percorso del modulo e delle relative risorse in modo da ridurre il numero di caratteri a meno di 256 caratteri.

## Versione di Gradle non supportata {#unsupported-version-of-gradle}

**Messaggio di errore:** Il progetto utilizza una versione non supportata di Gradle.

Il messaggio di errore viene visualizzato quando si crea l’app AEM Forms in Android Studio. Il problema si verifica a causa di una versione non supportata di Gradle nel sistema.

**Risoluzione:** Fai clic su **Correggi il wrapper Gradle e reimporta il progetto** per risolvere il problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemi di compatibilità del plug-in Gradle e Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Messaggio di errore:** Le versioni del plug-in e del Gradle di Android non sono compatibili.

Il messaggio di errore viene visualizzato quando si seleziona l&#39;opzione **Genera APK** dal menu **Genera** nell&#39;interfaccia utente di Android Studio.

![compatibilità_plug_gradle](assets/gradle_plugin_compatibility.png)

**Risoluzione:** Aprire il file **Gradle Scripts** > **gradle-wrapper.properties** e modificare la proprietà **distributionUrl**.

Ad esempio, la console Android Studio consiglia di effettuare il downgrade della versione Gradle alla versione 3.5. Modifica la versione nel file **distributionUrl** of **gradle-wrapper.properties**.

Seleziona di nuovo **Build** > **Build APK** per risolvere l&#39;errore e generare il file .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
