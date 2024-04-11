---
title: Domande frequenti su AEM
description: Utilizza queste domande frequenti per comprendere, configurare e risolvere i problemi relativi ai flussi di lavoro o ai problemi più comuni in AEM.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# Domande frequenti su AEM {#aem-faqs}

Scopri le risposte ad alcuni problemi di configurazione e risoluzione dei problemi AEM.

## Sites {#sites}

### Come si configura la distribuzione senza binario? {#how-do-i-configure-binary-less-distribution}

La distribuzione senza binario è supportata per le distribuzioni in un archivio dati condiviso e coinvolge agenti che utilizzano l’utilità di esportazione pacchetti di distribuzione basata su Vault (PID di fabbrica: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) Generatore di pacchetti.

Con la modalità senza binari abilitata, i pacchetti di contenuti distribuiti contengono riferimenti ai binari anziché ai binari effettivi.

#### Come si abilita la distribuzione senza binario? {#how-do-i-enable-binary-less-distribution}

Per abilitare la distribuzione senza binari, distribuisci con un archivio BLOB condiviso.
Controlla la `useBinaryReferences` nella configurazione OSGI con il PID di fabbrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* che il tuo agente sta utilizzando.

#### Come abilitare le autorizzazioni durante la creazione di una copia in lingua per gli autori di contenuti in AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Per creare la funzione di copia in lingua, gli autori dei contenuti devono disporre delle autorizzazioni all’indirizzo `/content/projects` posizione.

Se uno richiede che anche gli autori gestiscano i progetti, la soluzione consiste nell’aggiungere l’autore a `projects-administrators` gruppo.

#### Come si modifica il formato durante la creazione della copia in lingua per un progetto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Crea una directory principale della lingua e una copia per lingua all’interno della directory principale, prima di creare un progetto di traduzione.

Ad esempio, crea una directory principale della lingua in `/content/geometrixx` con nome come `fr_LU` (e titolo in francese (Lussemburgo)). Successivamente, crea una copia in lingua della pagina dal pannello Riferimenti e passa a `Create structure only` opzione in `Create & Translate`. Infine, crea un progetto di traduzione e quindi aggiungi la copia per lingua al processo di traduzione.

Per informazioni dettagliate, consulta le risorse aggiuntive di seguito:

* [Preparazione del contenuto per la traduzione](/help/sites-administering/tc-prep.md)
* [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md)

#### Come si controllano le funzionalità AEM come, i tentativi di accesso e ACL o le modifiche delle autorizzazioni? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

L&#39;AEM ha introdotto la possibilità di registrare le modifiche amministrative per una migliore risoluzione dei problemi e un migliore controllo. Per impostazione predefinita, le informazioni sono registrate in `error.log` file. Per semplificare il monitoraggio, si consiglia di reindirizzarli a un file di registro separato.
Per reindirizzare l&#39;output a un file di registro separato, vedere [Come controllare le operazioni di gestione degli utenti in AEM](/help/sites-administering/audit-user-management-operations.md).

#### Come si abilita SSL per impostazione predefinita? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 viene fornito con la procedura guidata SSL e offre un’interfaccia utente per configurare il supporto SSL di Jetty e Granite Jetty.

Per abilitare SSL per impostazione predefinita, consulta [SSL per impostazione predefinita](/help/sites-administering/ssl-by-default.md).

#### Qual è l’architettura consigliata quando si utilizza AEM Content Services da un’app mobile, idealmente React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

I servizi di contenuto sono basati sui modelli Sling e gli sviluppatori AEM devono fornire un pojo del modello Sling per ogni componente esportato.

Per informazioni su come utilizzare i servizi di contenuti AEM da un’applicazione React, consulta [Introduzione a AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) esercitazione.

Inoltre, se gli sviluppatori desiderano esportare una struttura di componenti, possono anche implementare `ComponentExporter` e `ContainerExporter` e utilizzare il `ModelFactory` per scorrere i componenti figlio e restituire la relativa rappresentazione del modello. Consulta le risorse seguenti:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: modelli Sling](https://sling.apache.org/documentation/bundles/models.html)

#### Come disattivare la finestra a comparsa per sondaggi AEM 6.4? {#how-to-disable-aem-survey-pop-up}

Puoi partecipare alla raccolta delle statistiche di utilizzo utilizzando l’interfaccia utente touch o la console web. Per istruzioni dettagliate, consulta [Accesso alla raccolta di statistiche di utilizzo aggregate](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Esiste una buona risorsa che evidenzia le caratteristiche principali per l’aggiornamento a AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Consulta [Perché aggiornare l’AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) che descrive il raggruppamento ad alto livello delle funzioni chiave per i clienti che intendono effettuare l’aggiornamento all’ultima versione di Adobe Experience Manager.

## Risorse {#assets}

### Perché il flusso di lavoro Assets si ripete durante il caricamento di file MP4 (ad esempio, utilizzando il metodo di trascinamento della selezione)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Se l’utente non dispone delle autorizzazioni di eliminazione per il caricamento dei file filmato nel nodo della risorsa, i nodi di eliminazione non riescono e il caricamento viene riavviato.

#### Quali sono le impostazioni predefinite per le configurazioni predefinite durante la creazione della copia in lingua? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Quando crei una copia per lingua tramite l’interfaccia utente touch (**Riferimenti** > **Aggiorna copia per lingua**), viene creata una nuova cartella DAM nella nuova lingua e da qui viene fatto riferimento alle risorse.

Questa è l’impostazione predefinita per le configurazioni pronte all’uso. È possibile impostare **Traduci risorse di pagina** = **Non tradurre** nelle configurazioni di traduzione.
Per AEM 6.4, **Strumenti** > **Cloud Service** > **Servizi cloud di traduzione**.

#### Come disattivare una componente AEM che causa una crescita esponenziale per il SegmentStore AEM (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Puoi disattivare la funzione di disabilitazione del componente OSGi. Per utilizzare questo servizio, consulta [Disattivazione componente OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Come soluzione alternativa, puoi anche disabilitare manualmente il componente tramite l’interfaccia utente o tramite un `curl` (esempio di seguito), dopo ogni riavvio dell’AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Come personalizzare le console di amministrazione? {#how-to-customize-admin-consoles}

AEM offre diversi meccanismi per personalizzare le console e la funzionalità di authoring delle pagine dell’istanza di authoring. Per informazioni su come creare una console personalizzata e personalizzare una vista predefinita per una console, consulta [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md).

#### Qual è la differenza tra i componenti basati su CoralUI 2 e CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Un nuovo set di componenti Sling di Granite UI Foundation viene creato per Coral3 e si trova in [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Esiste un set per i componenti basati su CoralUI 2 e uno per i componenti basati su CoralUI 3. Il nuovo set non sarà solo un copia-incolla del vecchio set, ma verrà ripulito (ad esempio, snellimento, rimozione della funzione obsoleta). Pertanto, si consiglia di utilizzare una pagina solo con set basati su CoralUI 3 o CoralUI 2.

Per ulteriori informazioni, consulta [Guida alla migrazione a CoralUI 3-based](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Come personalizzare il componente Ricerca in AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Per informazioni sull’aumento/classificazione delle ricerche e ulteriori informazioni sull’implementazione, consulta [Guida all’implementazione della ricerca semplice](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

L’implementazione di Simple Search è costituita dai materiali del laboratorio AEM Search Demystified del Summit 2017.

#### È possibile creare un plug-in per WordPress che consenta al cliente di accedere al selettore risorse di Adobe per selezionare le immagini? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sì, un cliente che utilizza WordPress può utilizzare il Selettore risorse di Adobe per selezionare immagini dal proprio server AEM Assets da aggiungere ai post sul proprio sito WordPress.

Fai riferimento a [Selettore risorse](../assets/search-assets.md#assetpicker) per ulteriori informazioni.
