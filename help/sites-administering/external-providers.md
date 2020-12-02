---
title: Analisi con fornitori esterni
seo-title: Analisi con fornitori esterni
description: Ulteriori informazioni su Analytics con provider esterni.
seo-description: Ulteriori informazioni su Analytics con provider esterni.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---


# Analytics con provider esterni {#analytics-with-external-providers}

Analytics può fornire informazioni importanti e interessanti su come viene utilizzato il sito Web.

Sono disponibili diverse configurazioni pronte all&#39;uso per l&#39;integrazione con il servizio appropriato, ad esempio:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Puoi anche configurare la tua istanza di **Snippet di analisi generici** per definire una nuova configurazione del servizio.

Le informazioni vengono quindi raccolte tramite piccoli frammenti di codice aggiunti alle pagine Web. Esempio:

>[!CAUTION]
>
>Gli script non devono essere racchiusi tra tag `script`.

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

Tali snippet consentono la raccolta dei dati e la generazione di rapporti. I dati effettivi raccolti dipendono dal provider e dallo snippet di codice effettivamente utilizzato. Le statistiche di esempio includono:

* quanti visitatori nel tempo
* quante pagine sono state visitate
* termini di ricerca utilizzati
* pagine di destinazione

>[!CAUTION]
>
>Il sito dimostrativo Geometrixx-esterno è configurato in modo che gli attributi forniti in Proprietà pagina vengano aggiunti al codice sorgente HTML (appena sopra il tag `</html>`) nello script `js` corrispondente.
>
>Se il proprio `/apps` non eredita dal componente di pagina predefinito ( `/libs/foundation/components/page`), è necessario assicurarsi che gli script `js` corrispondenti siano inclusi, ad esempio includendo `cq/cloudserviceconfigs/components/servicescomponents` o utilizzando un meccanismo simile.
>
>Senza questo, nessuno dei servizi (Generico, Analytics, Target, ecc.) funzionerà.

## Creazione di un nuovo servizio con un snippet generico {#creating-a-new-service-with-a-generic-snippet}

Per la configurazione di base:

1. Aprire la console **Strumenti**.
1. Dal riquadro a sinistra espandere **Configurazioni Cloud Services**.
1. Fate doppio clic su **Snippet di analisi generica** per aprire la pagina:

   ![](assets/analytics_genericoverview.png)

1. Fate clic sul simbolo + per aggiungere una nuova configurazione utilizzando la finestra di dialogo; assegnate almeno un nome, ad esempio Google Analytics:

   ![](assets/analytics_addconfig.png)

1. Fare clic su **Crea**, la finestra di dialogo degli snippet si aprirà immediatamente e incollare lo snippet javascript appropriato nel campo:

   ![](assets/analytics_snippet.png)

1. Fate clic su **OK** per salvare. 

## Utilizzo del nuovo servizio nelle pagine {#using-your-new-service-on-pages}

Dopo aver creato la configurazione del servizio è ora necessario configurare le pagine necessarie per utilizzarla:

1. Passate alla pagina.
1. Aprite la scheda **Proprietà pagina** dalla barra laterale, quindi la scheda **Cloud Services**.
1. Fare clic su **Aggiungi servizio**, quindi selezionare il servizio richiesto; ad esempio, il **Snippet di analisi generico**:

   ![](assets/analytics_selectservice.png)

1. Fate clic su **OK** per salvare. 
1. Verrà nuovamente visualizzata la scheda **Cloud Services**. Il **snippet di analisi generico** è ora elencato con il messaggio `Configuration reference missing`. Utilizzate l&#39;elenco a discesa per selezionare la vostra istanza di servizio specifica; ad esempio google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. Fate clic su **OK** per salvare. 

   Lo snippet può ora essere visualizzato se visualizzate l&#39;origine pagina per la pagina.

   Una volta trascorso un periodo di tempo adeguato, sarà possibile visualizzare le statistiche raccolte.

   >[!NOTE]
   >
   >Se la configurazione è associata a una pagina con pagine figlie, il servizio viene ereditato anche da tali pagine.
