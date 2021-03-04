---
title: Risolvere i problemi relativi all’app AEM Forms
seo-title: Risolvere i problemi relativi all’app AEM Forms
description: Scopri i problemi comuni dell’app AEM Forms e come risolverli.
seo-description: Scopri i problemi comuni dell’app AEM Forms e come risolverli.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: 3690d2d76ce13064bd3946f4f6fea1a2759cdf37
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---


# Risolvere i problemi relativi all’app AEM Forms {#troubleshoot-aem-forms-app}

Questo articolo descrive i messaggi di errore che potrebbero essere visualizzati durante la creazione dell’app AEM Forms e i passaggi per risolverli.

Le sezioni di questo articolo includono:

* [Perdita di allegati per gli utenti iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Le bozze dei moduli HTML5 inviate dagli utenti dell’area di lavoro non sono visibili sul portale](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Impossibile caricare i moduli HTML5 (non memorizzati nella cache) nell’app AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms non si sincronizza su Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versione non supportata di Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemi di compatibilità dei plug-in Gradle e Gradle per Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perdita di allegati per gli utenti iOS {#attachment-loss-for-ios-users}

L’app AEM Forms per iOS configurata per la sincronizzazione con AEM Forms su OSGi supporta solo allegati a livello di campo. Tutti gli allegati devono avere nomi univoci. Se più allegati hanno lo stesso nome, viene conservato un solo allegato e tutti gli altri con lo stesso nome vengono persi. Esegui i seguenti passaggi per evitare che gli utenti su dispositivi iOS subiscano una perdita di dati:

1. Sul server connesso, passa a **Adobe Experience Manager > Strumenti > Operazioni > Console web**.
1. Trova e fai clic su **[!UICONTROL Configurazione canale web per moduli adattivi e comunicazioni interattive]**.
1. Nella finestra di dialogo [!UICONTROL Configurazione canale web per moduli adattivi e comunicazioni interattive], abilita **Rendi unici i nomi dei file**.

   Se l&#39;impostazione **Rendi unici i nomi dei file** è disabilitata, gli utenti subiranno una perdita di dati se tentano di inviare moduli adattivi con più allegati.

1. Fai clic su **Salva**.

## Le bozze dei moduli HTML5 inviate dagli utenti dell’area di lavoro non sono visibili sul portale {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Per i moduli HTML5 abilitati nell’app AEM Forms con il profilo di rendering HTML **Salva come bozza**, le bozze salvate non sono visibili agli utenti dell’area di lavoro. Per visualizzare le bozze salvate dei moduli HTML5 inviate dagli utenti dell’area di lavoro sul portale, esegui le seguenti operazioni:

1. Apri CRXDE e accedi con le credenziali di amministratore.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Nel percorso principale del CRXDE, nell&#39;elenco Controllo accessi in Controllo accessi fare clic su **+**.
1. Nella finestra di dialogo **Aggiungi nuova voce**, fare clic sul pulsante di ricerca del gruppo nel campo Principale.
1. Nel campo Nome della finestra di dialogo Seleziona entità digitare `PERM_WORKSPACE_USER` e fare clic su **Cerca**.
1. Seleziona il gruppo `PERM_WORKSPACE_USER` nella finestra di dialogo Seleziona principale e fai clic su **OK**.
1. Nella finestra di dialogo Aggiungi nuova voce, il gruppo `PERM_WORKSPACE_USER` viene selezionato nel campo Principale .

   Abilitare i privilegi `jcr:read` per il gruppo di utenti.

1. Fai clic su **OK**.

## Impossibile caricare i moduli HTML5 (non memorizzati nella cache) nell’app AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando l’app AEM Forms è connessa a una versione precedente del server AEM Forms, i moduli HTML5 non memorizzati nella cache non vengono caricati nell’app AEM Forms.

Esegui i seguenti passaggi per risolvere il problema:

1. Nell’istanza di authoring, passa a **Adobe Experience Manager > Strumenti > Configura il servizio offline dell’app Workspace > Configura ora**.
1. Nella pagina **Servizio offline app Workspace**, fai clic su **Cache risorse manuale**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. Nella scheda **Cache risorse manuale**, fai clic sul pulsante **+** per aggiungere un percorso CRX.
1. Nel campo **Aggiungi una nuova risorsa**, digita: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e fai clic su **Aggiungi**.
1. Fai clic su **Salva**.

## AEM Forms non viene sincronizzato su Windows {#aem-forms-do-not-sync-on-windows}

Nell’app AEM Forms su Windows, un modulo non si sincronizza con il server connesso se il percorso del modulo o di una delle relative risorse contiene più o meno 256 caratteri.

Modificare il percorso del modulo e le relative risorse per ridurre il numero di caratteri a meno di 256 caratteri.

## Versione non supportata di Gradle {#unsupported-version-of-gradle}

**Messaggio di errore:** il progetto utilizza una versione non supportata di Gradle.

Il messaggio di errore viene visualizzato quando si crea l’app AEM Forms in Android Studio. Il problema si verifica a causa di una versione non supportata di Gradle supportata sul sistema.

**Risoluzione:** Fai clic su  **Fix Gradle wrapper e reimporta il** progetto per risolvere il problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemi di compatibilità dei plug-in Gradle e Gradle per Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Messaggio di errore:** le versioni del plugin Gradle Android e Gradle non sono compatibili.

Il messaggio di errore viene visualizzato quando si seleziona l&#39;opzione **Genera APK** dal menu **Genera** nell&#39;interfaccia utente di Android Studio.

![gradle_plugin_compatibilità](assets/gradle_plugin_compatibility.png)

**Risoluzione:** Apri script  **di grammatica**  >  **gradle-wrapper.** propertiesfile e modifica la proprietà  **** distributionUrlproperty.

Ad esempio, la console Android Studio consiglia di scaricare la versione Gradle a 3.5. Modifica la versione nel file **distributionUrl** di **gradle-wrapper.properties** .

Seleziona nuovamente **Build** > **Genera APK** per risolvere l&#39;errore e generare il file .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

