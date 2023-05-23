---
title: Strutturare un’app
seo-title: Structure an App
description: Segui questa pagina per scoprire come creare la struttura di un’app. Questa pagina descrive come strutturare modelli e componenti con informazioni su JavaScript e CSS Clientlibs.
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

# Strutturare un’app{#structure-an-app}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Un progetto AEM Mobile coinvolge un diverso set di tipi di contenuto, tra cui pagine, librerie client JavaScript e CSS, componenti AEM riutilizzabili, configurazioni di sincronizzazione dei contenuti e contenuti shell dell’app PhoneGap. Basare la nuova app AEM Mobile su [Kit di avvio](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) è un buon modo per inserire tutti i diversi tipi di contenuti nella struttura consigliata, per facilitarne sia la portabilità che la manutenzione nel lungo periodo.

## Contenuto pagina {#page-content}

Le pagine dell’applicazione devono trovarsi tutte sotto /content/mobileapps per essere riconosciute dalla console di AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Per convenzione AEM, la prima pagina dell’app deve essere reindirizzata a uno dei suoi figli, che funge da lingua predefinita dell’app (&quot;en&quot; in entrambi i casi Geometrixx e Starter Kit). La pagina internazionale di primo livello in genere eredita dal componente di base &quot;splash-page&quot; (/libs/mobileapps/components/splash-page) che si occupa dell’inizializzazione necessaria per supportare l’installazione degli aggiornamenti over-the-air di Content Sync (il codice contentInit è disponibile all’indirizzo /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modelli e componenti {#templates-and-components}

Il codice modello e componente per l&#39;app deve trovarsi in /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. In conformità alla convenzione, inserisci il modello e il codice del componente in /apps/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. Questo modello deve essere familiare agli sviluppatori che hanno già lavorato con Site in AEM. Per impostazione predefinita, questa opzione è seguita dal blocco di /apps/ per l’accesso anonimo nelle istanze di pubblicazione. Di conseguenza, il tuo codice JSP non elaborato è nascosto da potenziali aggressori.

I modelli specifici dell’app possono essere configurati per essere presentati solo utilizzando `allowedPaths` sul modello stesso e impostandone il valore su &#39;/content/mobileapps(/.&amp;ast;)?&#39; - o anche qualcosa di più specifico se il modello dovrebbe essere utilizzabile solo per una singola app. Il `allowedParents` e `allowedChildren` Le proprietà possono essere utilizzate anche per un controllo molto dettagliato dei modelli che saranno disponibili per un autore in base a dove viene creata la nuova pagina.

Quando crei un nuovo componente pagina app da zero, si consiglia di impostarlo `sling:resourceSuperType` su &quot;mobileapps/components/angular/ng-page&quot;. In questo modo la pagina verrà impostata per l’authoring e il rendering come app a pagina singola e potrai sovrapporre eventuali file .jsp che il componente potrebbe dover modificare. Poiché ng-page non include alcun framework dell’interfaccia utente, in genere uno sviluppatore finisce per sovrapporsi (almeno) a &quot;template.jsp&quot; (sovrapposto da /libs/mobileapps/components/angular/ng-page/template.jsp).

I componenti di pagina autorizzabili, che desiderano sfruttare AngularJS, hanno un equivalente `sling:resourceSuperType` si trova in /libs/mobileapps/components/angular/ng-component che può essere sovrapposto e personalizzato allo stesso modo.

## Clientlibs JavaScript e CSS {#javascript-and-css-clientlibs}

Per quanto riguarda le librerie client, sono disponibili alcune opzioni per lo sviluppatore di dove inserirle nell’archivio. Il seguente modello è offerto a titolo indicativo, ma non è un requisito difficile.

Se il codice lato client può essere mantenuto da solo e non è correlato a un componente specifico dell’applicazione, ovvero può essere riutilizzato in altre applicazioni, si consiglia di memorizzarlo in /etc/clientlibs/&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. D’altra parte, se la libreria client è specifica per una singola app, puoi nidificarla come elemento secondario del nodo di progettazione dell’app; /etc/designs/phonegap/&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs. Questa categoria di clientlib non deve essere utilizzata da altre librerie e deve essere utilizzata per incorporare altre librerie, a seconda delle necessità. Seguendo questo modello, lo sviluppatore evita di dover aggiungere nuove configurazioni di sincronizzazione dei contenuti ogni volta che una libreria client viene aggiunta all’app, semplicemente aggiornando la proprietà &quot;embeds&quot; della libreria client di progettazione dell’app. Osserva ad esempio il nodo di configurazione Geometrixx clientlibs-all Content Sync in /content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all.

Se il codice lato client è strettamente associato a un componente specifico, inseriscilo in una libreria client nidificata sotto la posizione del componente in /apps/ e incorporane la categoria nella libreria client &quot;progettazione&quot; dell’app.

## Configurazione PhoneGap {#phonegap-configuration}

Ogni app AEM Mobile contiene una directory che ospita i file di configurazione utilizzati da PhoneGap [interfaccia della riga di comando](https://github.com/phonegap/phonegap-cli) e [PhoneGap Build](https://build.phonegap.com/) per trasformare il contenuto web in un’applicazione eseguibile. Nell’esempio di Geometrixx, ad esempio, questa directory (/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content) si trova come parte della shell; una decisione di progettazione è stata presa perché contiene solo contenuti che non possono essere aggiornati over-the-air, come i plug-in che si occupano delle API dei dispositivi e la configurazione dell’app stessa.

In questa directory troverai anche un certo numero di [Hook Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) che possono essere utilizzati per installare i plug-in, inserire i file di risorse nelle posizioni specifiche della piattaforma e altre azioni che devono essere eseguite come parte della build. Nota: in alternativa al download di ciascun plug-in come parte della build, puoi seguire il pattern dell’app Kitchen Sink e [includi codice sorgente del plug-in](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) con il resto del progetto dell&#39;app.

## Passaggi successivi {#the-next-steps}

Una volta appresa la struttura dell’app, consulta [Creazione e modifica delle app tramite la console delle app](/help/mobile/phonegap-apps-console.md).
