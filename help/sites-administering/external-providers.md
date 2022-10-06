---
title: Analytics con fornitori esterni
seo-title: Analytics with External Providers
description: Scopri di più su Analytics con fornitori esterni.
seo-description: Learn about Analytics with External Providers.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 4%

---

# Analytics con fornitori esterni {#analytics-with-external-providers}

Analytics può fornire informazioni importanti e interessanti sull’utilizzo del sito web.

Sono disponibili diverse configurazioni predefinite per l’integrazione con il servizio appropriato, ad esempio:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Puoi anche configurare la tua istanza di **Frammenti generici di Analytics** per definire una nuova configurazione del servizio.

Le informazioni vengono quindi raccolte tramite piccoli frammenti di codice che vengono aggiunti alle pagine web. Esempio:

>[!CAUTION]
>
>Gli script non devono essere racchiusi in `script` tag.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

Tali snippet consentono la raccolta dei dati e la generazione di rapporti. I dati effettivi raccolti dipendono dal provider e dallo snippet di codice effettivo utilizzato. Le statistiche di esempio includono:

* quanti visitatori nel tempo
* quante pagine sono state visitate
* termini di ricerca utilizzati
* pagine di destinazione

>[!CAUTION]
>
>Il sito demo Geometrixx-Outdoors è configurato in modo che gli attributi forniti nelle Proprietà pagina vengano aggiunti al codice sorgente html (appena sopra il `</html>` endtag) nel corrispondente `js` script.
>
>Se il tuo `/apps` non ereditano dal componente pagina predefinito ( `/libs/foundation/components/page`) devi assicurarti (o i tuoi sviluppatori) che il `js` gli script sono inclusi, ad esempio, includendo `cq/cloudserviceconfigs/components/servicescomponents`o utilizzando un meccanismo simile.
>
>In caso contrario, nessuno dei servizi (Generico, Analytics, Target, ecc.) funzionerà.

## Creazione di un nuovo servizio con un frammento generico {#creating-a-new-service-with-a-generic-snippet}

Per la configurazione di base:

1. Apri **Strumenti** console.
1. Espandi il riquadro a sinistra **Configurazioni Cloud Services**.
1. Fai doppio clic su **Frammento di analisi generico** per aprire la pagina:

   ![](assets/analytics_genericoverview.png)

1. Fai clic sul segno + per aggiungere una nuova configurazione utilizzando la finestra di dialogo; almeno assegna un nome, ad esempio google analytics:

   ![](assets/analytics_addconfig.png)

1. Fai clic su **Crea**, la finestra di dialogo snippet si aprirà immediatamente - incolla lo snippet javascript appropriato nel campo :

   ![](assets/analytics_snippet.png)

1. Fate clic su **OK** per salvare. 

## Utilizzo del nuovo servizio nelle pagine {#using-your-new-service-on-pages}

Dopo aver creato la configurazione del servizio è ora necessario configurare le pagine necessarie per utilizzarla:

1. Passa alla pagina .
1. Apri **Proprietà pagina** dalla barra laterale, quindi il **Cloud Services** scheda .
1. Fai clic su **Aggiungi servizio**, quindi seleziona il servizio richiesto; ad esempio **Frammento di analisi generico**:

   ![](assets/analytics_selectservice.png)

1. Fate clic su **OK** per salvare. 
1. Verrà restituito al **Cloud Services** scheda . La **Frammento di analisi generico** è ora elencato con il messaggio `Configuration reference missing`. Utilizza l’elenco a discesa per selezionare la tua istanza di servizio specifica; per esempio google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. Fate clic su **OK** per salvare. 

   Lo snippet può ora essere visualizzato se visualizzi l’origine pagina per la pagina.

   Una volta trascorso un adeguato periodo di tempo, potrai visualizzare le statistiche raccolte.

   >[!NOTE]
   >
   >Se la configurazione è associata a una pagina con pagine figlie, anche il servizio viene ereditato da tali pagine.
