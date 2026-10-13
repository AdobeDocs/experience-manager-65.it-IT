---
title: La tua app ibrida è pronta per AEM Mobile?
description: Scopri le app ibride. Un’app in Experience Manager è solitamente divisa in due parti. La "shell" e il "contenuto" e questa pagina forniscono ulteriori informazioni su insight su questi argomenti.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%
---
# La tua app ibrida è pronta per Adobe Experience Manager Mobili?{#is-your-hybrid-app-ready-for-aem-mobile}

{{ue-over-mobile}}

Quindi hai importato la tua app Hybrid PhoneGap o Cordova in AEM, e ora? È probabile che tu voglia aggiungere contenuto creabile all’app. Per eseguire questa attività, è necessario avere una conoscenza generale della struttura di un’app AEM. Un’app in AEM è solitamente divisa in due parti. La &quot;shell&quot; e il &quot;contenuto&quot;. La &quot;shell&quot; comprende le parti statiche dell’app, ad esempio i file di configurazione PhoneGap, il framework dell’app e i controlli di navigazione. Il contenuto dell&#39;archivio importato viene memorizzato come parte della shell. Nel contesto di questo documento, la shell è tutto il contenuto non creato da AEM dell&#39;app Hybrid PhoneGap creata dallo sviluppatore dell&#39;app.

Il contenuto si riferisce ai componenti, ai modelli e alle pagine create in AEM e create da AEM Developer. Il contenuto è classificato come contenuto per sviluppatori o come contenuto creato. Componenti, progettazioni e modelli di pagina sono considerati contenuti per lo sviluppo in quanto sono generati da uno sviluppatore. I contenuti dell’autore sono pagine che sono state create utilizzando i componenti e i modelli. Queste pagine vengono in genere eseguite da un Designer o da un addetto al marketing.

L’aggiunta di pagine AEM create all’app ibrida richiede il coordinamento tra lo sviluppatore dell’app e lo sviluppatore AEM. In qualsiasi punto dell’app in cui desideri aggiungere contenuti creati, lo sviluppatore dell’app deve organizzare queste pagine in una struttura che possa essere sovrapposta in Experience Manager. Lo sviluppatore di app deve essere in grado di fornire allo sviluppatore di Experience Manager i percorsi in cui viene aggiunto il contenuto creato da Experience Manager. Quindi, fornisci una pagina segnaposto nell’app ibrida che viene sostituita dopo che lo sviluppatore Experience Manager ha creato il contenuto della pagina.

Per rendere la spiegazione più facile da seguire, viene utilizzato AEM Experience Cloud: AEM Mobile Hybrid Reference per spiegare i concetti. L’app Hybrid Reference è costituita da una pagina di benvenuto con un menu laterale.

![chlimage_1-76](assets/chlimage_1-76.png)

In questo esempio verrà creata la pagina di benvenuto dell’applicazione. Visualizzazione dell&#39;origine [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Lo sviluppatore dell’app ha definito una pagina di benvenuto e fornito un modello per la pagina di cui viene eseguito il rendering dall’app. Lo sviluppatore di app e lo sviluppatore di AEM devono coordinarsi in questa pagina. Il percorso del modello della pagina di benvenuto nell’app di riferimento ibrida è definito come &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;. Questo percorso è importante perché lo sviluppatore AEM creerà la pagina di benvenuto nell’archivio AEM utilizzando lo stesso percorso.

![chlimage_1-77](assets/chlimage_1-77.png)

È importante che l’app ibrida e i contenuti creati con AEM utilizzino lo stesso percorso, perché per aggiungere nuove pagine all’app ibrida si basa sulla possibilità di sovrapporre i contenuti utilizzando Sincronizzazione contenuti. Quando l’app ibrida viene importata in AEM, come parte del processo di importazione, vengono impostate le configurazioni di sincronizzazione dei contenuti.

![chlimage_1-78](assets/chlimage_1-78.png)

Quando &quot;Scarica Source&quot; dal dashboard dell’app, questi script ContentSync vengono eseguiti per assemblare un archivio dell’app ibrida.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync prima richiama la &quot;shell&quot; dell’app, dove vengono memorizzati tutti i contenuti sviluppati dall’app ibrida. Quindi, estrae il &quot;contenuto&quot; dell’app. Ora, se ci sono pagine nella &quot;shell&quot; che hanno lo stesso percorso di &quot;content&quot;, le pagine sotto &quot;shell&quot; sono (sostituite) dalle pagine sotto &quot;content&quot;. Nell’esempio dell’app di riferimento ibrida, se viene creata in AEM una pagina con lo stesso percorso di &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;, quando viene eseguito ContentSync, questa si sovrappone alla pagina che faceva parte dell’app di riferimento ibrido. Si sovrappone a qualsiasi cosa si trovi in AEM in quella posizione. La sovrapposizione è gestita da ContentSync, quindi per chi utilizza l’app, gli aggiornamenti all’app con i contenuti creati da AEM sono facili da interpretare e non richiedono la ricostruzione dell’app. Di conseguenza, quando esegui l’app, la pagina di benvenuto viene visualizzata come segue:

![chlimage_1-80](assets/chlimage_1-80.png)
