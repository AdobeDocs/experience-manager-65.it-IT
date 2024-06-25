---
title: Come abilitare i componenti core Adaptive Forms su AEM 6.5 Forms?
description: Guida dettagliata per abilitare i componenti core Adaptive Forms in un ambiente Forms AEM 6.5.
keywords: Abilitare i componenti core, i componenti core Forms adattivo, i componenti core su 6.5, i componenti core Forms adattivo su AEM 6.5, i componenti core AF su AEM 6.5, i componenti core AEM 6.5 di Forms
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 3%

---

# Abilitare i componenti core Adaptive Forms sul Forms AEM 6.5 {#enable-adaptive-forms-core-components}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=it) |
| AEM 6.5 | Questo articolo |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

L’abilitazione dei componenti core adattivi di Forms consente di iniziare a creare, pubblicare e distribuire [Forms adattivo basato su componenti core](create-an-adaptive-form-core-components.md) e [Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) dall’ambiente Forms AEM 6.5.

Per abilitare i componenti core Adaptive Forms nell’ambiente Forms AEM 6.5, imposta e implementa [AEM Archetipo 41 o versione successiva](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) progetto basato (con le opzioni forms abilitate) su tutte le istanze Author e Publish.

Questo articolo fornisce istruzioni dettagliate per configurare e distribuire un progetto basato su Archetipo AEM 41 o versione successiva nell’ambiente Forms AEM 6.5 per abilitare i componenti core di Forms adattivi. Consulta l’elenco di seguito per **AEM 6.5** versioni compatibili per l’abilitazione dei componenti core di Forms:

## Prerequisiti {#prerequisites}

Prima di abilitare i componenti core Forms adattivi in un ambiente Forms AEM 6.5:

* [Aggiornamento a AEM 6.5 Forms Service Pack 16 (6.5.16.0) o versione successiva](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* Installa la versione più recente di [Apache Maven](https://maven.apache.org/download.cgi).

* Installa un editor di testo normale. Microsoft Visual Studio Code.

## Crea e implementa il progetto più recente basato su Archetipo AEM

Per creare un Archetipo AEM 41 o [più tardi](https://github.com/adobe/aem-project-archetype) basato su e implementalo in tutte le istanze Author e Publish:

1. Accedi al tuo computer, ospitando ed eseguendo l’istanza Forms AEM 6.5, come amministratore.
1. Apri il prompt dei comandi o il terminale ed esegui il seguente comando per creare un progetto Archetipo AEM (con le opzioni Forms abilitate):

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux o Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Quando esegui il comando di cui sopra, considera i seguenti punti:

   * Non modificare il valore di `aemVersion` proprietà da `6.5.15.0` a qualsiasi altra cosa.

   * Imposta il `archetypeVersion` proprietà a `41` o più tardi. Per la versione più recente, consulta la sezione sui requisiti di sistema in [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) documentazione.

   * Aggiorna il comando per riflettere i valori specifici per l&#39;ambiente, incluso `appTitle`, `appId`, e `groupId`. Inoltre, imposta il valore di  `includeFormsenrollment` proprietà a `y`. Se si utilizza Forms Portal, impostare `includeExamples=y` per includere nel progetto i componenti core di Forms Portal.


1. (Solo per progetti basati su Archetipo versione 41) Dopo la creazione del progetto Archetipo AEM, abilita i temi per Forms adattivo basato su Componenti core. Per abilitare i temi:

   1. Apri [Cartella progetto Archetipo AEM]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html per la modifica:

   1. Aggiungere il seguente codice alla riga 21:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Aggiungere il codice sopra indicato alla riga 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Salva e chiudi il file.

1. Aggiorna il progetto per includere la versione più recente dei Componenti core di Forms:

   1. Apri [Cartella progetto Archetipo AEM]/pom.xml per la modifica.
   1. Imposta versione di `core.forms.components.version` e `core.forms.components.af.version` al [Componenti core Forms più recenti](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history) e accertarsi che entrambi abbiano la stessa versione di **Componenti core Forms** indicato nella tabella e impostare la versione di `core.wcm.components.version` come indicato nella [Componenti core WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html).

      >[!WARNING]
      >
      >* Quando si crea un progetto Archetipo con versione 45, il `[AEM Archetype Project Folder]/pom.xml` inizialmente imposta la versione dei componenti core forms su 1.1.28. Prima di creare o distribuire il progetto Archetipo, aggiorna la versione dei componenti core forms al 1.1.26. La versione più recente è disponibile nel [Cronologia delle versioni di Forms di AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history).

      >[!NOTE]
      >
      >* Se imposti un’altra topologia, accertati di aggiungere l’URL di invio, di precompilazione e di altro tipo al inserisco nell&#39;elenco Consentiti di Dispatcher a livello di Dispatcher.

   1. Salva e chiudi il file.


1. Dopo aver creato correttamente il progetto dell’Archetipo AEM, crea il pacchetto di distribuzione per il tuo ambiente. Per generare il pacchetto:

   1. Passa alla directory principale del progetto Archetipo AEM.

   1. Esegui il seguente comando per creare il progetto Archetipo AEM per il tuo ambiente:

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   Una volta creato correttamente il progetto dell’Archetipo AEM, viene generato un pacchetto AEM. Puoi trovare il pacchetto all’indirizzo [Cartella progetto Archetipo AEM]\all\target\[appid].all-[version].zip

1. Utilizza il [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) per implementare [Cartella progetto Archetipo AEM]\all\target\[appid].all-[version].zip su tutte le istanze Author e Publish.

>[!NOTE]
>
>
>
> * Nel caso in cui si verifichino difficoltà di accesso alla finestra di dialogo di accesso in un’istanza di pubblicazione, per installare il pacchetto tramite Gestione pacchetti, prova a utilizzare l’URL: `http://[Publish Server URL]:[PORT]/system/console` per accedere. Questo consente di accedere alla pagina di accesso di un’istanza di Publish, per procedere con il processo di installazione.
> * Non eliminare o eliminare il progetto Archetipo dopo averlo distribuito nell’ambiente. Il progetto Archetipo è necessario per aggiungere all’ambiente temi personalizzati e nuovi Componenti core Forms adattivi.

I Componenti core sono abilitati per il tuo ambiente. Nell’ambiente vengono distribuiti un modello modulo adattivo basato su Componenti core vuoto e un tema Canvas 3.0, che consente di: [creazione di componenti core basati su Adaptive Forms](create-an-adaptive-form-core-components.md).

## Domande frequenti

### Cosa sono i Componenti core?

Il [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un set di componenti WCM (Web Content Management) standardizzati per l’AEM che consentono di velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti web.

### Quali sono tutte le funzionalità aggiunte all’abilitazione dei componenti core?


Quando i componenti core Adaptive Forms sono abilitati per il tuo ambiente, all’ambiente vengono aggiunti un modello di modulo adattivo basato su Componenti core vuoto e un tema Canvas 3.0. Dopo aver abilitato i componenti core Forms adattivi per il tuo ambiente, puoi:

* Creazione di componenti core basati su Adaptive Forms.
* Creare modelli di moduli adattivi basati su Componenti core.
* Crea temi personalizzati per i modelli di moduli adattivi basati su Componenti core.
* Distribuisci le rappresentazioni JSON del modulo adattivo basato su componenti core a canali quali dispositivi mobili, web, app native e servizi che richiedono la rappresentazione headless di un modulo.

## Passaggio successivo

* [Creare componenti core basati sul modulo adattivo](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Creare o aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Creazione di temi per Forms adattivo basato su Componenti core](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Creazione di un modello per Forms adattivo basato su Componenti core](template-editor.md)
