---
title: Come abilitare i componenti core Adaptive Forms su AEM 6.5 Forms?
description: Guida dettagliata per abilitare i componenti core Adaptive Forms in un ambiente AEM 6.5 Forms.
keywords: Abilitare i componenti core, i componenti core Forms adattivo, i componenti core su 6.5, i componenti core Forms adattivo su AEM 6.5, i componenti core AF su AEM 6.5, i componenti core Forms di AEM 6.5
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: c75cd7a0cbd0c19fd10cc7512bbfa14fae1e4f92
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---

# Abilitare i componenti core Adaptive Forms su AEM 6.5 Forms {#enable-adaptive-forms-core-components}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=it) |
| AEM 6.5 | Questo articolo |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

L&#39;abilitazione dei componenti core adattivi di Forms consente di iniziare a creare, pubblicare e distribuire [componenti core basati su Forms adattivo](create-an-adaptive-form-core-components.md) e [Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) dall&#39;ambiente Forms di AEM 6.5.

Per abilitare i componenti core Adaptive Forms nell&#39;ambiente AEM 6.5 Forms, imposta e distribuisci un progetto basato su [AEM Archetype 41 o versione successiva](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) (con le opzioni Forms abilitate) in tutte le istanze Author e Publish.

Questo articolo fornisce istruzioni dettagliate per configurare e distribuire un progetto basato su Archetipo 41 o versioni successive di AEM nell’ambiente Forms AEM 6.5 per abilitare i componenti core di Forms adattivi. Per **versioni compatibili con AEM 6.5** per l&#39;abilitazione dei componenti core Forms, fare riferimento all&#39;elenco seguente:

## Prerequisiti {#prerequisites}

Prima di abilitare i componenti core Adaptive Forms in un ambiente AEM 6.5 Forms:

* [Eseguire l&#39;aggiornamento ad AEM 6.5 Forms Service Pack 16 (6.5.16.0) o versione successiva](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* Installa la versione più recente di [Apache Maven](https://maven.apache.org/download.cgi).

* Installa un editor di testo normale. Microsoft Visual Studio Code.

## Crea e implementa il progetto più recente basato su Archetipo AEM

Per creare un progetto basato su Archetipo AEM 41 o [versione successiva](https://github.com/adobe/aem-project-archetype) e distribuirlo a tutte le istanze di authoring e pubblicazione:

1. Accedi al computer, hosting ed esecuzione dell’istanza Forms di AEM 6.5, come amministratore.
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
      -D aemVersion="6.5.23" 
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
      -D aemVersion="6.5.23" 
   ```

   Quando esegui il comando di cui sopra, considera i seguenti punti:

   * Impostare la proprietà `archetypeVersion` su `41` o versione successiva. Per la versione più recente, consulta la sezione sui requisiti di sistema nella documentazione di [AEM Project Archetype](https://github.com/adobe/aem-project-archetype).

   * Aggiornare il comando in modo che rifletta i valori specifici dell&#39;ambiente, inclusi `appTitle`, `appId` e `groupId`. Impostare inoltre il valore della proprietà `includeFormsenrollment` su `y`. Se si utilizza Forms Portal, impostare l&#39;opzione `includeExamples=y` per includere nel progetto i componenti core di Forms Portal.


1. (Solo per progetti basati su Archetipo versione 41) Dopo la creazione del progetto Archetipo AEM, abilita i temi per Forms adattivo basato su Componenti core. Per abilitare i temi:

   1. Apri la [cartella dei progetti Archetipo AEM]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html per modificare:

   1. Aggiungere il seguente codice alla riga 21:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Aggiungi il codice sopra menzionato alla riga 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Salva e chiudi il file.

1. Aggiorna il progetto per includere la versione più recente dei Componenti core di Forms:

   1. Apri la [cartella dei progetti Archetipo AEM]/pom.xml per la modifica.
   1. Impostare la versione di `core.forms.components.version` e `core.forms.components.af.version` sulla [versione più recente dei Componenti core di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history) e assicurarsi che entrambi abbiano la stessa versione dei **Componenti core di Forms** menzionati nella tabella e impostare la versione di `core.wcm.components.version` come specificato in [Componenti core di WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html).

      >[!WARNING]
      >
      >* Durante la creazione di un progetto Archetipo con versione 45, `[AEM Archetype Project Folder]/pom.xml` imposta inizialmente la versione dei Componenti core forms su 1.1.28. Prima di creare o distribuire il progetto Archetipo, aggiorna la versione dei componenti core forms al 1.1.26. La versione più recente è disponibile nella [cronologia delle versioni di AEM 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history).

      >[!NOTE]
      >
      >* Se configuri un’altra topologia, accertati di aggiungere l’URL di invio, precompilazione e altro al inserisco nell&#39;elenco Consentiti a livello di Dispatcher.

   1. Salva e chiudi il file.


1. Dopo aver creato correttamente il progetto Archetipo AEM, crea il pacchetto di distribuzione per il tuo ambiente. Per generare il pacchetto:

   1. Passa alla directory principale del progetto Archetipo AEM.

   1. Esegui il seguente comando per generare il progetto Archetipo AEM per il tuo ambiente:

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   Una volta generato correttamente il progetto Archetipo AEM, viene generato un pacchetto AEM. Puoi trovare il pacchetto nella [cartella dei progetti Archetipo AEM]\all\target\[appid].all-[versione].zip

1. Utilizza [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) per distribuire il pacchetto [Cartella di progetto Archetipo AEM]\all\target\[appid].all-[versione].zip in tutte le istanze di authoring e pubblicazione.

>[!NOTE]
>
>
>
> * Se si verificano problemi durante l&#39;accesso alla finestra di dialogo di accesso in un&#39;istanza di pubblicazione, per installare il pacchetto tramite Gestione pacchetti provare a utilizzare l&#39;URL `http://[Publish Server URL]:[PORT]/system/console` per l&#39;accesso. Questo consente di accedere alla pagina di accesso di un’istanza Publish, per procedere con il processo di installazione.
> * Non eliminare o eliminare il progetto Archetipo dopo averlo distribuito nell’ambiente. Il progetto Archetipo è necessario per aggiungere all’ambiente temi personalizzati e nuovi Componenti core Forms adattivi.

I Componenti core sono abilitati per il tuo ambiente. Nell&#39;ambiente vengono distribuiti un modello modulo adattivo basato su Componenti core vuoti e un tema Canvas 3.0, che consente di [creare componenti core basati su Forms adattivo](create-an-adaptive-form-core-components.md).

## Domande frequenti

### Cosa sono i Componenti core?

I [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un insieme di componenti WCM (Web Content Management) standardizzati di AEM che consentono di velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti Web.

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
