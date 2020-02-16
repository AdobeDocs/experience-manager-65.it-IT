---
title: Risoluzione dei problemi relativi all'app AEM Forms
seo-title: Risoluzione dei problemi relativi all'app AEM Forms
description: Scopri i problemi più comuni con l’app AEM Forms e come risolverli.
seo-description: Scopri i problemi più comuni con l’app AEM Forms e come risolverli.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Risoluzione dei problemi relativi all&#39;app AEM Forms {#troubleshoot-aem-forms-app}

Questo articolo descrive i messaggi di errore che potrebbero essere visualizzati durante la creazione dell&#39;app AEM Forms e i passaggi per risolverli.

Le sezioni di questo articolo includono:

* [Perdita di allegati per gli utenti iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Le bozze dei moduli HTML5 inviate dagli utenti dell’area di lavoro non sono visibili sul portale](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Impossibile caricare i moduli HTML5 (non memorizzati nella cache) nell&#39;app AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [I moduli AEM non vengono sincronizzati in Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versione non supportata di Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemi di compatibilità dei plug-in Gradle e Gradle per Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perdita di allegati per gli utenti iOS {#attachment-loss-for-ios-users}

L’app AEM Forms per iOS configurata per la sincronizzazione con AEM Forms su OSGi supporta solo gli allegati a livello di campo. Tutti gli allegati devono avere nomi univoci. Se più allegati hanno lo stesso nome, viene mantenuto un solo allegato e tutti gli altri con lo stesso nome vanno persi. Effettuate le seguenti operazioni per evitare che gli utenti dei dispositivi iOS si trovino in una situazione di perdita di dati:

1. Nel server connesso, passa a **Adobe Experience Manager > Strumenti > Operazioni > Console** Web.
1. Individuare e fare clic su Servizio **di configurazione del modulo** adattivo.
1. Nella finestra di dialogo Servizio configurazione modulo adattivo, abilitare **Rendi univoci** i nomi dei file.

   Se l&#39;impostazione **Rendi univoci** i nomi dei file è disabilitata, gli utenti potrebbero perdere i dati se tentano di inviare moduli adattivi con più allegati.

1. Fai clic su **Salva**.

## Le bozze dei moduli HTML5 inviate dagli utenti dell’area di lavoro non sono visibili sul portale {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Per i moduli HTML5 abilitati nell’app AEM Forms con **Salva come profilo di rendering HTML bozza** , le bozze salvate non sono visibili agli utenti dell’area di lavoro. Per visualizzare le bozze salvate dei moduli HTML5 inviate dagli utenti dell&#39;area di lavoro sul portale, effettuare le seguenti operazioni:

1. Aprite CRXDE e accedete con le credenziali di amministratore.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Nel percorso principale del CRXDE, nell&#39;elenco Controllo accesso in Controllo accesso fare clic su **+**.
1. Nella finestra di dialogo **Aggiungi nuovo elemento** , fate clic sul pulsante di ricerca del gruppo nel campo Principal.
1. Nel campo Nome della finestra di dialogo Seleziona entità digitare `PERM_WORKSPACE_USER` e fare clic su **Cerca**.
1. Selezionate `PERM_WORKSPACE_USER` il gruppo nella finestra di dialogo Seleziona entità e fate clic su **OK**.
1. Nella finestra di dialogo Aggiungi nuovo elemento, `PERM_WORKSPACE_USER` il gruppo è selezionato nel campo Principal.

   Abilitate `jcr:read` i privilegi per il gruppo di utenti.

1. Fai clic su **OK**. 

## Impossibile caricare i moduli HTML5 (non memorizzati nella cache) nell&#39;app AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando l’app AEM Forms è connessa a una versione precedente del server AEM Forms, i moduli HTML5 non memorizzati nella cache non vengono caricati nell’app AEM Forms.

Per risolvere il problema, effettuate le seguenti operazioni:

1. Nell’istanza di creazione, accedi ad **Adobe Experience Manager > Strumenti > Configura servizio offline app Workspace > Configura ora**.
1. Nella pagina Servizio **offline app** Workspace, fai clic su Cache **risorse** manuale.

   URL: https://&lt;server>:&lt;porta>/libs/fd/workspace-offline/content/config.html

1. Nella scheda Cache **risorse** manuale fare clic sul pulsante **+** per aggiungere un percorso CRX.
1. Nel campo **Aggiungi nuova risorsa** digitare: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e fate clic su **Aggiungi**.
1. Fai clic su **Salva**.

## I moduli AEM non vengono sincronizzati in Windows {#aem-forms-do-not-sync-on-windows}

Nell&#39;app AEM Forms in Windows, un modulo non si sincronizza con il server connesso se il percorso del modulo o una delle sue risorse contiene più o meno 256 caratteri.

Modificare il percorso del modulo e le relative risorse per ridurre il numero di caratteri a meno di 256 caratteri.

## Versione non supportata di Gradle {#unsupported-version-of-gradle}

**** Messaggio di errore: Il progetto utilizza una versione non supportata di Gradle.

Il messaggio di errore viene visualizzato quando si crea l&#39;app AEM Forms in Android Studio. Il problema si verifica a causa di una versione non supportata di Gradle supportata nel sistema.

**** Risoluzione: Per risolvere il problema, fate clic su **Correggi il wrapper della sfumatura e reimportate il progetto** .

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemi di compatibilità dei plug-in Gradle e Gradle per Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**** Messaggio di errore: Le versioni del plug-in Gradle Android e Gradle non sono compatibili.

Il messaggio di errore viene visualizzato quando selezionate l&#39;opzione **Genera APK** dal menu **Genera** dell&#39;interfaccia utente di Android Studio.

![gradle_plugin_compatible](assets/gradle_plugin_compatibility.png)

**** Risoluzione: Aprite il file **Gradle Scripts** > **gradle-wrapper.properties** e modificate la proprietà **distributionUrl** .

Ad esempio, la console di Android Studio consiglia di ridurre la versione Gradle a 3.5. Modificate la versione in **distributionUrl** del **file gradle-wrapper.properties** .

Selezionate di nuovo **Genera** > **Crea APK** per risolvere l&#39;errore e generare il file .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

