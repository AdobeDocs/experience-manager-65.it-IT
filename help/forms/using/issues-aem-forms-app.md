---
title: Risoluzione dei problemi  app AEM Forms
seo-title: Risoluzione dei problemi  app AEM Forms
description: Scopri i problemi comuni con  app AEM Forms e come risolverli.
seo-description: Scopri i problemi comuni con  app AEM Forms e come risolverli.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---


# Risoluzione dei problemi  app AEM Forms {#troubleshoot-aem-forms-app}

Questo articolo descrive i messaggi di errore che potrebbero essere visualizzati durante la creazione &#39;app AEM Forms e i passaggi per risolverli.

Le sezioni di questo articolo includono:

* [Perdita di allegati per gli utenti iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Le bozze dei moduli HTML5 inviate dagli utenti dell’area di lavoro non sono visibili sul portale](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Impossibile caricare i moduli HTML5 (non memorizzati nella cache) &#39;app AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [ AEM Forms non sincronizza in Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versione non supportata di Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemi di compatibilità dei plug-in Gradle e Gradle per Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perdita di allegati per gli utenti iOS {#attachment-loss-for-ios-users}

 app AEM Forms per iOS configurata per la sincronizzazione con  AEM Forms su OSGi supporta solo allegati a livello di campo. Tutti gli allegati devono avere nomi univoci. Se più allegati hanno lo stesso nome, viene mantenuto un solo allegato e tutti gli altri con lo stesso nome vanno persi. Effettuate le seguenti operazioni per evitare che gli utenti dei dispositivi iOS si trovino in una situazione di perdita di dati:

1. Nel server connesso, andate a **Adobe Experience Manager > Strumenti > Operazioni > Console Web**.
1. Trovare e fare clic su **Servizio configurazione modulo adattivo**.
1. Nella finestra di dialogo Servizio configurazione modulo adattivo, abilitare **Rendi univoci i nomi dei file**.

   Se l&#39;impostazione **Rendi univoci i nomi dei file** è disabilitata, gli utenti potrebbero perdere i dati se tentano di inviare moduli adattivi con più allegati.

1. Fai clic su **Salva**.

## Le bozze dei moduli HTML5 inviate dagli utenti dell&#39;area di lavoro non sono visibili sul portale {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Per i moduli HTML5 abilitati nell&#39;app  AEM Forms con il profilo di rendering HTML **Salva come bozza**, le bozze salvate non sono visibili agli utenti dell&#39;area di lavoro. Per visualizzare le bozze salvate dei moduli HTML5 inviate dagli utenti dell&#39;area di lavoro sul portale, effettuare le seguenti operazioni:

1. Aprite CRXDE e accedete con le credenziali di amministratore.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Nel percorso principale del CRXDE, nell&#39;elenco Controllo accesso in Controllo accesso fare clic su **+**.
1. Nella finestra di dialogo **Aggiungi nuova voce**, fare clic sul pulsante di ricerca del gruppo nel campo Principal.
1. Nel campo Nome della finestra di dialogo Seleziona entità digitare `PERM_WORKSPACE_USER` e fare clic su **Cerca**.
1. Selezionare il gruppo `PERM_WORKSPACE_USER` nella finestra di dialogo Seleziona entità e fare clic su **OK**.
1. Nella finestra di dialogo Aggiungi nuova voce, il gruppo `PERM_WORKSPACE_USER` è selezionato nel campo Principal.

   Abilitate i privilegi `jcr:read` per il gruppo di utenti.

1. Fai clic su **OK**.

## Impossibile caricare i moduli HTML5 (non memorizzati nella cache) &#39;app AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando &#39;app AEM Forms è connessa a una versione precedente del server AEM Forms, i moduli HTML5 non memorizzati nella cache non vengono caricati &#39;app AEM Forms.

Per risolvere il problema, effettuate le seguenti operazioni:

1. Nell&#39;istanza di authoring, passare a **Adobe Experience Manager > Strumenti > Configura servizio offline app Workspace > Configura ora**.
1. Nella pagina **Servizio offline app Workspace** fare clic su **Cache risorse manuale**.

   URL: https://&lt;server>:&lt;porta>/libs/fd/workspace-offline/content/config.html

1. Nella scheda **Cache delle risorse manuali**, fare clic sul pulsante **+** per aggiungere un percorso CRX.
1. Nel campo **Aggiungi una nuova risorsa** digitare: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e fare clic su **Aggiungi**.
1. Fai clic su **Salva**.

##  AEM Forms non sincronizza in Windows {#aem-forms-do-not-sync-on-windows}

Nell&#39;app AEM Forms  su Windows, un modulo non si sincronizza con il server connesso se il percorso del modulo o una delle relative risorse contiene più o meno 256 caratteri.

Modificare il percorso del modulo e le relative risorse per ridurre il numero di caratteri a meno di 256 caratteri.

## Versione non supportata di Gradle {#unsupported-version-of-gradle}

**Messaggio di errore:** il progetto utilizza una versione non supportata di Gradle.

Il messaggio di errore viene visualizzato quando create  app AEM Forms in Android Studio. Il problema si verifica a causa di una versione non supportata di Gradle supportata nel sistema.

**Risoluzione:** fate clic su  **Correggi wrapper sfumatura e reimportate il** progetto per risolvere il problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemi di compatibilità dei plug-in Gradle e Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Messaggio di errore:** Le versioni del plug-in Gradle Android e Gradle non sono compatibili.

Il messaggio di errore viene visualizzato quando si seleziona l&#39;opzione **Crea APK** dal menu **Genera** nell&#39;interfaccia utente di Android Studio.

![gradle_plugin_compatible](assets/gradle_plugin_compatibility.png)

**Risoluzione:** Open  **Gradle Scripts** >  **gradle-wrapper.** properties file e modificare la  **** distributionUrlproperty.

Ad esempio, la console di Android Studio consiglia di ridurre la versione Gradle a 3.5. Modificate la versione in **distributionUrl** di **gradle-wrapper.properties** file.

Selezionare di nuovo **Build** > **Crea APK** per risolvere l&#39;errore e generare il file .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

