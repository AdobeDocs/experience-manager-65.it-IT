---
title: Struttura di un'app
seo-title: Struttura di un'app
description: Segui questa pagina per scoprire come creare la struttura di un'app. Questa pagina descrive come strutturare modelli e componenti insieme a informazioni sulle librerie JavaScript e CSS.
seo-description: Segui questa pagina per scoprire come creare la struttura di un'app. Questa pagina descrive come strutturare modelli e componenti insieme a informazioni sulle librerie JavaScript e CSS.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---


# Struttura di un&#39;app{#structure-an-app}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Un progetto AEM Mobile  include un insieme di tipi di contenuto diversi, tra cui pagine, librerie client JavaScript e CSS, componenti AEM riutilizzabili, configurazioni di sincronizzazione dei contenuti e contenuto della shell dell&#39;app PhoneGap. Basare la nuova app AEM Mobile  sul [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) è un buon modo per inserire tutti i diversi tipi di contenuto nella struttura consigliata, al fine di semplificare la portabilità e la manutenzione a lungo termine.

## Contenuto pagina {#page-content}

Le pagine dell&#39;applicazione devono essere tutte posizionate sotto /content/mobileapps per essere riconosciute dalla console AEM Mobile .

![chlimage_1-52](assets/chlimage_1-52.png)

Per AEM convenzione, la prima pagina dell&#39;app deve essere un reindirizzamento a uno dei suoi elementi figlio, che funge da lingua predefinita dell&#39;app (in entrambi i casi, Geometrixx e Starter Kit). La pagina delle impostazioni internazionali di livello superiore in genere eredita dal componente &#39;splash-page&#39; di base (/libs/mobileapps/components/splash-page) che si occupa dell&#39;inizializzazione necessaria per supportare l&#39;installazione degli aggiornamenti di sincronizzazione dei contenuti in modalità &quot;over-the-air&quot; (il codice contentInit si trova all&#39;indirizzo /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modelli e componenti {#templates-and-components}

Il modello e il codice del componente per l&#39;app devono trovarsi in /apps/&lt;brand name>/&lt;app name>. In conformità con la convenzione, devi inserire il codice del modello e del componente in /apps/&lt;brand name>/&lt;app name>. Questo pattern deve essere familiare agli sviluppatori che hanno già lavorato con Site in AEM. In genere viene seguita quando /apps/ viene bloccato l&#39;accesso anonimo per impostazione predefinita sulle istanze di pubblicazione. Di conseguenza, il codice JSP non elaborato è tenuto in considerazione dai potenziali attacchi.

I modelli specifici per le app possono essere configurati solo per essere presentati utilizzando il nodo di proprietà `allowedPaths` nel modello stesso e impostando il relativo valore su &#39;/content/mobileapps(/.&amp;ast;)?&quot; - o qualcosa di più specifico se il modello deve essere utilizzabile solo per una singola app. Le proprietà `allowedParents` e `allowedChildren` possono essere sfruttate anche per un controllo granulato molto preciso su quali modelli saranno disponibili per un autore in base alla posizione in cui viene creata la nuova pagina.

Quando create un nuovo componente di pagina dell&#39;app da zero, si consiglia di impostare la proprietà `sling:resourceSuperType` su &#39;mobileapps/components/angular/ng-page&#39;. Questa opzione consente di impostare la pagina sia per l’authoring che per il rendering come app a pagina singola e di sovrapporre eventuali file .jsp che il componente potrebbe dover modificare. Poiché ng-page non include alcun framework di interfaccia utente, uno sviluppatore generalmente finisce per sovrapporre (almeno) &#39;template.jsp&#39; (con sovrapposizione da /libs/mobileapps/components/angular/ng-page/template.jsp).

I componenti di pagina modificabili, che desiderano sfruttare AngularJS, hanno un componente `sling:resourceSuperType` equivalente ubicato in /libs/mobileapps/components/angular/ng-component che può essere sovrapposto e personalizzato allo stesso modo.

## Clientlibs JavaScript e CSS {#javascript-and-css-clientlibs}

Per quanto riguarda le librerie client, lo sviluppatore può scegliere dove inserirle nella directory archivio. Il seguente modello è offerto per la guida, ma non è un requisito difficile.

Se il codice clientside può restare indipendente e non si riferisce a un componente specifico dell&#39;applicazione, ovvero può essere riutilizzato in altre applicazioni, è consigliabile memorizzarlo in /etc/clientlibs/&lt;brand name>/&lt;lib name>. D&#39;altro canto, se clientlib è specifica per una singola app, puoi nidificarla come figlio del nodo di progettazione dell&#39;app; /etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs. La categoria clientlib non deve essere utilizzata da altre libs e dovrebbe essere utilizzata per incorporare altre libs, se necessario. In questo modo lo sviluppatore non deve più aggiungere nuove configurazioni di Content Sync ogni volta che una libreria client viene aggiunta all&#39;app, ma semplicemente aggiornare la proprietà &#39;embeds&#39; della clientlib di progettazione dell&#39;app. Ad esempio, date un&#39;occhiata al nodo di configurazione clientlibs-all Content Sync in /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all.

Se il codice lato client è strettamente associato a un componente specifico, inseritelo in una libreria client nidificata sotto la posizione del componente in /apps/, e incorporate la sua categoria nella clientlib &#39;design&#39; dell&#39;app.

## Configurazione PhoneGap {#phonegap-configuration}

Ogni app AEM Mobile  contiene una directory che ospita i file di configurazione utilizzati dall&#39;interfaccia della riga di comando PhoneGap [a1/> e [PhoneGap build](https://build.phonegap.com/) per trasformare il contenuto Web in un&#39;applicazione eseguibile. ](https://github.com/phonegap/phonegap-cli) Nell’Geometrixx di esempio, questa directory (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) si trova come parte della Shell; una decisione di progettazione presa a causa del fatto che contiene solo contenuto che non può essere aggiornato in modalità &quot;over-the-air&quot;, come i plug-in che si occupano delle API del dispositivo e della configurazione dell&#39;app stessa.

In questa directory troverete anche una serie di [ganci Cordova](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) che possono essere utilizzati per installare i plug-in, inserire i file di risorse nelle loro posizioni specifiche della piattaforma, e altre azioni che dovrebbero essere eseguite come parte della build. Nota: come alternativa al download di ciascun plug-in come parte della build, è possibile seguire il modello dell&#39;app Kitchen Sink e [includere codice sorgente plug-in](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) con il resto del progetto dell&#39;app.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso la struttura dell&#39;app, vedi [Creazione e modifica delle app tramite la console dell&#39;app](/help/mobile/phonegap-apps-console.md).
