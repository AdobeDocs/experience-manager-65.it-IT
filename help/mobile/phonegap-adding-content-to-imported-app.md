---
title: La tua app ibrida è pronta per AEM Mobile?
seo-title: Is your hybrid app ready for AEM Mobile?
description: Segui questa pagina per scoprire di più sulle app ibride. Un’app nell’AEM è comunemente divisa in due parti. La "shell" e il "contenuto" e questa pagina forniscono ulteriori informazioni su questi argomenti.
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# La tua app ibrida è pronta per AEM Mobile?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Quindi hai importato la tua app Hybrid PhoneGap o Cordova nell&#39;AEM, e ora? Probabilmente vorrai aggiungere all’app contenuti che possano essere creati dall’autore. Per eseguire questa attività è necessaria una comprensione generale della struttura di un’app AEM. Un’app nell’AEM è comunemente divisa in due parti. La &quot;shell&quot; e il &quot;contenuto&quot;. La &quot;shell&quot; comprende le parti statiche dell’app, ad esempio i file di configurazione PhoneGap, il framework dell’app e i controlli di navigazione. Il contenuto dell&#39;archivio importato viene memorizzato come parte della shell. Nel contesto di questo documento, la shell è tutto il contenuto creato non dall’AEM dell’app Hybrid PhoneGap creata dallo sviluppatore dell’app.

Il contenuto si riferisce ai componenti, ai modelli e alle pagine create da AEM e create da AEM Developer. Il contenuto è classificato come contenuto per sviluppatori o come contenuto creato. I componenti, le progettazioni e i modelli di pagina sono considerati contenuti per lo sviluppo, in quanto sono generati da uno sviluppatore. i contenuti dell’autore sono pagine che sono state create utilizzando i componenti e i modelli. Queste operazioni vengono in genere eseguite da un designer o da un addetto marketing.

L’aggiunta di pagine AEM create all’app ibrida richiede il coordinamento tra lo sviluppatore dell’app e lo sviluppatore dell’AEM. In qualsiasi punto dell’app in cui desideri aggiungere contenuti creati, lo sviluppatore dell’app deve organizzare queste pagine in una struttura che possa essere sovrapposta nell’AEM. Lo sviluppatore dell’app deve essere in grado di fornire allo sviluppatore dell’AEM i percorsi in cui deve essere aggiunto il contenuto creato dall’AEM e quindi fornire nell’app ibrida una pagina segnaposto che verrà sostituita dopo che lo sviluppatore dell’AEM avrà creato il contenuto della pagina.

Per rendere la spiegazione più facile da seguire, per spiegare i concetti utilizzeremo il Marketing Cloud AEM: AEM Mobile Hybrid Reference. L’app Hybrid Reference è costituita da una pagina di benvenuto con un menu laterale.

![chlimage_1-76](assets/chlimage_1-76.png)

In questo esempio verrà creata la pagina di benvenuto dell’applicazione. Dai un’occhiata alla sorgente [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Vediamo che lo sviluppatore di app ha definito una pagina di benvenuto e ha fornito un modello per la pagina di cui viene eseguito il rendering dall’app. È qui che lo sviluppatore di app e lo sviluppatore di AEM devono coordinarsi. Il percorso del modello della pagina di benvenuto nell’app di riferimento ibrida è definito come &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;. Questo percorso è estremamente importante perché lo sviluppatore AEM creerà la pagina di benvenuto nell’archivio AEM utilizzando lo stesso percorso.

![chlimage_1-77](assets/chlimage_1-77.png)

È importante che l’app ibrida e i contenuti creati dall’AEM utilizzino lo stesso percorso, perché per aggiungere nuove pagine all’app ibrida ci affidiamo alla possibilità di sovrapporre i contenuti utilizzando Sincronizzazione contenuti. Quando l’app ibrida viene importata in AEM come parte del processo di importazione, vengono impostate le configurazioni di Sincronizzazione contenuto.

![chlimage_1-78](assets/chlimage_1-78.png)

Quando &quot;Scarica origine&quot; dal dashboard dell’app, questi script ContentSync vengono eseguiti per assemblare un archivio dell’app ibrida.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync prima richiama la &quot;shell&quot; dell’app, dove vengono memorizzati tutti i contenuti sviluppati dall’app ibrida, e poi richiama il &quot;contenuto&quot; dell’app. Ora, se ci sono pagine nella &quot;shell&quot; che hanno lo stesso percorso di &quot;content&quot;, le pagine nella &quot;shell&quot; saranno (sostituite) dalle pagine in &quot;content&quot;. In altre parole, nell’esempio dell’app di riferimento ibrida se creiamo in AEM una pagina con lo stesso percorso di &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot; quando viene eseguito ContentSync, questa si sovrapporrà alla pagina che faceva parte dell’app di riferimento ibrido con tutto ciò che si trova nell’AEM in quella posizione. La sovrapposizione è gestita da ContentSync in modo che per qualcuno che sta utilizzando l&#39;app gli aggiornamenti all&#39;app con contenuti creati da AEM saranno senza soluzione di continuità e non richiederanno una ricostruzione dell&#39;app. Di conseguenza, quando esegui l’app, la pagina di benvenuto viene visualizzata come segue:

![chlimage_1-80](assets/chlimage_1-80.png)
