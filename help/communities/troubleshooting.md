---
title: Risoluzione dei problemi della community
description: Risoluzione dei problemi della community, compresi i problemi noti
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# Risoluzione dei problemi della community {#troubleshooting}

Questa sezione contiene i problemi comuni e i problemi noti durante la risoluzione dei problemi relativi alla Community.

## Problemi noti {#known-issues}

### Recupero del dispatcher non riuscito {#dispatcher-refetch-fails}

Quando si utilizza Dispatcher 4.1.5 con una versione più recente di Jetty, un refetch potrebbe risultare in &quot;Impossibile ricevere la risposta dal server remoto&quot; dopo aver aspettato il timeout della richiesta.

Questo problema verrà risolto con l’utilizzo di Dispatcher 4.1.6 o versione successiva.

### Impossibile accedere al post del forum dopo l&#39;aggiornamento da CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Se un forum è stato creato su CQ 5.4 e gli argomenti pubblicati e poi il sito è stato aggiornato a AEM 5.6.1 o versione successiva, il tentativo di visualizzare i post esistenti potrebbe causare un errore sulla pagina:

Carattere pattern non valido &#39;a&#39; Non è possibile elaborare la richiesta a `/content/demoforums/forum-test.html` su questo server e i registri contengono quanto segue:

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

Il problema è che la stringa di formato per com.day.cq.commons.date.RelativeTimeFormat è stata modificata tra 5.4 e 5.5 in modo che la &quot;a&quot; per &quot;ago&quot; non venga più accettata.

Pertanto, qualsiasi codice che utilizzi l’API RelativeTimeFormat() deve essere modificato:

* Da: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* A: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

L’errore è diverso in fase di authoring e pubblicazione. L&#39;autore non riesce in modo silenzioso e semplicemente non visualizza gli argomenti del forum. Al momento della pubblicazione, genera l’errore sulla pagina.

Consulta la sezione [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API per ulteriori informazioni.

## Preoccupazioni comuni {#common-concerns}

### Avviso nei registri: Handlebars dichiarato obsoleto {#warning-in-logs-handlebars-deprecated}

Durante l&#39;avvio (non il primo - ma ogni uno dopo) nei log può essere visualizzato il seguente avviso:

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` è stato sostituito da `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Questo avviso può essere ignorato come `jknack.handlebars.Handlebars`, utilizzato da [SCF](scf.md#handlebarsjavascripttemplatinglanguage), viene fornito con la propria utility helper i18n. All&#39;avvio, viene sostituito con un AEM specifico [Helper i18n](handlebars-helpers.md#i-n). Questo avviso viene generato dalla libreria di terze parti per confermare l&#39;override di un helper esistente.

### Avviso nei registri: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

La pubblicazione di un certo numero di argomenti del forum di Social Communities può comportare enormi quantità di log di avviso e informazioni da OakResourceListener processOsgiEventQueue.

Questi avvisi possono essere tranquillamente ignorati.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### Errore nei registri: NoClassDefFoundError per IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

L&#39;aggiornamento AEM 5.6.1 GA all&#39;ultimo cq-socialcommunities-pkg-1.4.x o a AEM 6.0 causa errori nel file di log durante l&#39;avvio per una condizione che si risolverà come evidenziato dall&#39;errore non visto al riavvio.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
