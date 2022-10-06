---
title: Struttura di un'app
seo-title: Structure an App
description: Segui questa pagina per scoprire come creare la struttura di un’app. Questa pagina descrive come strutturare modelli e componenti insieme a informazioni sulle librerie client JavaScript e CSS.
seo-description: Follow this page to learn about how to create structure of an app. This page describes how to structure templates and components along with information on JavaScript and CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# Struttura di un&#39;app{#structure-an-app}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Un progetto AEM Mobile include un set diversificato di tipi di contenuto, tra cui pagine, librerie client JavaScript e CSS, componenti AEM riutilizzabili, configurazioni di sincronizzazione dei contenuti e contenuto della shell dell’app PhoneGap. Basare la nuova app AEM Mobile su [Kit iniziale](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) è un buon modo per inserire tutti i diversi tipi di contenuto nella struttura consigliata per facilitare sia la portabilità che la manutenzione a lungo termine.

## Contenuto della pagina {#page-content}

Le pagine dell’applicazione devono essere tutte situate sotto /content/mobileapps per essere riconosciute dalla console AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Per convenzione, la prima pagina dell’app deve essere un reindirizzamento a uno dei suoi elementi figlio, che funge da lingua predefinita dell’app (&quot;en&quot; nei casi Geometrixx e Starter Kit). La pagina locale di primo livello eredita tipicamente dal componente &#39;splash-page&#39; di base (/libs/mobileapps/components/splash-page) che si occupa dell&#39;inizializzazione necessaria per supportare l&#39;installazione degli aggiornamenti di sincronizzazione dei contenuti offline (il codice contentInit può essere trovato all&#39;indirizzo /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modelli e componenti {#templates-and-components}

Il modello e il codice del componente per l&#39;app devono trovarsi in /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. In conformità alla convenzione, dovresti inserire il modello e il codice componente in /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. Questo modello deve essere familiare agli sviluppatori che hanno già lavorato con Site in AEM. Viene generalmente seguito come /apps/ viene bloccato per impostazione predefinita all’accesso anonimo nelle istanze di pubblicazione. Di conseguenza, il codice JSP non elaborato è nascosto a potenziali aggressori.

È possibile configurare modelli specifici per le app in modo che siano presentati solo utilizzando il `allowedPaths` nodo di proprietà sul modello stesso e impostazione del relativo valore su &#39;/content/mobileapps(/.&amp;ast;)?&quot; - o qualcosa di più specifico se il modello deve essere utilizzabile solo per una singola app. La `allowedParents` e `allowedChildren` è inoltre possibile sfruttare le proprietà per un controllo a grana molto fine sui modelli disponibili per un autore in base alla posizione in cui viene creata la nuova pagina.

Quando crei un nuovo componente per la pagina dell’app da zero, si consiglia di impostarlo come `sling:resourceSuperType` su &#39;mobileapps/components/angular/ng-page&#39;. Questo consente di impostare la pagina sia per l’authoring che per il rendering come app a pagina singola e di sovrapporre eventuali file .jsp che il componente potrebbe dover modificare. Poiché ng-page non include alcun framework di interfaccia utente, uno sviluppatore generalmente finisce per sovrapporre (almeno) &#39;template.jsp&#39; (sovrapposto da /libs/mobileapps/components/angular/ng-page/template.jsp).

I componenti di pagina autorizzati che desiderano sfruttare AngularJS hanno un equivalente `sling:resourceSuperType` componente situato in /libs/mobileapps/components/angular/ng-component che può essere sovrapposto e personalizzato nello stesso modo.

## Clientlibs JavaScript e CSS {#javascript-and-css-clientlibs}

Per quanto riguarda le librerie client, lo sviluppatore può scegliere dove inserirle nell’archivio. Il seguente modello è offerto per la guida, ma non è un requisito difficile.

Se il tuo codice clientside può stare da solo e non si riferisce a un componente specifico della tua applicazione - ovvero può essere riutilizzato in altre applicazioni - si consiglia di memorizzarlo in /etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. D’altro canto, se la clientlib è specifica per una singola app, puoi nidificarla come elemento secondario del nodo di progettazione dell’app; /etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs. La categoria di clientlib non deve essere utilizzata da altre librerie e deve essere utilizzata per incorporare altre librerie come necessario. Seguendo questi pattern, lo sviluppatore non deve aggiungere nuove configurazioni di sincronizzazione dei contenuti ogni volta che una libreria client viene aggiunta all’app, ma semplicemente aggiornare la proprietà &quot;embeds&quot; della clientlib di progettazione dell’app. Ad esempio, dai un&#39;occhiata al nodo di configurazione clientlibs-all Content Sync in /content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all.

Se il codice lato client è strettamente associato a un componente specifico, inseriscilo in una libreria client nidificata sotto la posizione del componente in /apps/ e incorporalo nella clientlib &#39;design&#39; dell&#39;app.

## Configurazione di PhoneGap {#phonegap-configuration}

Ogni app AEM Mobile contiene una directory che ospita i file di configurazione utilizzati da PhoneGap [interfaccia a riga di comando](https://github.com/phonegap/phonegap-cli) e [PhoneGap build](https://build.phonegap.com/) per trasformare il contenuto web in un’applicazione eseguibile. Nell’esempio di Geometrixx, ad esempio, questa directory (/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content) si trova come parte della Shell; una decisione di progettazione presa a causa del fatto che contiene solo contenuti che non possono essere aggiornati nell’aria, come plug-in che si occupano delle API dei dispositivi e della configurazione dell’app stessa.

In questa directory troverete anche una serie di [Hook Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) che può essere utilizzato per installare i plug-in, inserire i file di risorse nelle rispettive posizioni specifiche della piattaforma e altre azioni che devono essere eseguite come parte della build. Nota: come alternativa al download di ogni plug-in come parte della build, è possibile seguire il modello dell&#39;app Kitchen Sink e [include il codice sorgente del plug-in](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) con il resto del progetto dell&#39;app.

## Passaggi successivi {#the-next-steps}

Una volta appresa la struttura dell’app, consulta [Creazione e modifica delle app tramite la console App](/help/mobile/phonegap-apps-console.md).
