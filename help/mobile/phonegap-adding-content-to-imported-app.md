---
title: La tua app ibrida è pronta per  AEM Mobile?
seo-title: La tua app ibrida è pronta per  AEM Mobile?
description: Segui questa pagina per saperne di più sulle app ibride. Un'app in AEM è comunemente divisa in due parti. I contenuti 'shell' e 'content' e questa pagina forniscono ulteriori informazioni su questi argomenti.
seo-description: Segui questa pagina per saperne di più sulle app ibride. Un'app in AEM è comunemente divisa in due parti. I contenuti 'shell' e 'content' e questa pagina forniscono ulteriori informazioni su questi argomenti.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---


# L&#39;app ibrida è pronta per  AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Quindi hai importato la tua app Hybrid PhoneGap o Cordova in AEM, ora cosa? È probabile che desideriate aggiungere all&#39;app contenuto modificabile. Per eseguire questa attività, è necessario conoscere in modo generale la struttura di un&#39;app AEM. Un&#39;app in AEM è comunemente divisa in due parti. &#39;shell&#39; e &#39;content&#39;. La &#39;shell&#39; comprende le parti statiche dell&#39;app; come i file di configurazione PhoneGap, il framework dell&#39;app e i controlli di navigazione. I contenuti dell&#39;archivio importato vengono memorizzati come parte della shell. Nel contesto di questo documento, la shell è tutto il contenuto non AEM creato dell&#39;app PhoneGap ibrida creata dallo sviluppatore di app.

Per &quot;contenuto&quot; si intendono i componenti, i modelli e le pagine create AEM dallo sviluppatore AEM. Il contenuto è classificato come contenuto sviluppatore o come contenuto creato. I componenti, le progettazioni e i modelli di pagina sono considerati come contenuti da sviluppo, poiché sono creati da uno sviluppatore. author-content sono pagine create utilizzando i componenti e i modelli. Generalmente, sono eseguite da un designer o un esperto di marketing.

L&#39;aggiunta di pagine AEM create all&#39;app ibrida richiede il coordinamento tra lo sviluppatore di app e lo sviluppatore di AEM. In qualsiasi punto dell&#39;app in cui desiderate aggiungere contenuto creato, lo sviluppatore di app deve organizzare queste pagine in una struttura che può essere sovrapposta in AEM. Lo sviluppatore di app deve essere in grado di fornire allo sviluppatore di AEM i percorsi in cui aggiungere il contenuto creato AEM e quindi fornire una pagina segnaposto nell&#39;app ibrida che verrà sostituita dopo che lo sviluppatore AEM avrà creato il contenuto della pagina.

Per semplificare la spiegazione, utilizzeremo il Marketing Cloud AEM:  AEM Mobile Hybrid Reference per spiegare i concetti. L&#39;app Riferimento ibrido è costituita da una pagina di benvenuto con un menu laterale.

![chlimage_1-76](assets/chlimage_1-76.png)

In questo esempio verrà creata la pagina di benvenuto dell&#39;applicazione. Date un&#39;occhiata alla fonte [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Lo sviluppatore di app ha definito una pagina di benvenuto e fornito un modello per la pagina di cui l&#39;app esegue il rendering. Qui è dove lo sviluppatore di app e AEM sviluppatore devono coordinarsi. Il percorso del modello di pagina di benvenuto nell&#39;app di riferimento ibrida è definito come &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39;. Questo percorso è estremamente importante perché lo sviluppatore AEM creerà la propria pagina di benvenuto nell&#39;archivio AEM utilizzando lo stesso percorso.

![chlimage_1-77](assets/chlimage_1-77.png)

È importante che l’app ibrida e il contenuto AEM creato utilizzino lo stesso percorso perché ci affidiamo alla possibilità di sovrapporre il contenuto tramite Content Sync per aggiungere nuove pagine all’app ibrida. Quando l&#39;app ibrida viene importata in AEM come parte del processo di importazione, vengono configurate le configurazioni di sincronizzazione dei contenuti.

![chlimage_1-78](assets/chlimage_1-78.png)

Quando &quot;Scarica origine&quot; dal dashboard dell&#39;app, questi script ContentSync vengono eseguiti per assemblare un archivio dell&#39;app ibrida.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync richiama innanzitutto &#39;shell&#39; dell&#39;app, dove viene memorizzato tutto il contenuto sviluppato dall&#39;app ibrida, e quindi richiama &#39;content&#39; dell&#39;app. Ora, se nella shell sono presenti pagine con lo stesso percorso di &quot;contenuto&quot;, le pagine sotto &quot;shell&quot; saranno (sostituite) dalle pagine sotto &quot;contenuto&quot;. In altre parole, nell’esempio dell’app di riferimento ibrida, se creiamo una pagina in AEM con lo stesso percorso di &#39;&#39;content/mobileapps/hybrid-reference-app/en/welcome.template.html&#39;&#39; durante l’esecuzione di ContentSync, essa sovrapporrà alla pagina che faceva parte dell’app di riferimento ibrido qualsiasi cosa si trovi in AEM in quella posizione. La sovrapposizione viene gestita da ContentSync in modo che per gli utenti che utilizzano l&#39;app gli aggiornamenti all&#39;app con AEM contenuto creato siano perfetti e non richiedano una nuova build dell&#39;app. Di conseguenza, quando eseguite l&#39;app, la pagina di benvenuto verrà visualizzata come segue:

![chlimage_1-80](assets/chlimage_1-80.png)
