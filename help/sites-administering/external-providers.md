---
title: Analytics con provider esterni
description: Scopri come configurare una tua istanza di snippet generici di Analytics per definire una nuova configurazione di servizio.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# Analytics con provider esterni {#analytics-with-external-providers}

Analytics può fornirti informazioni importanti e interessanti su come viene utilizzato il tuo sito web.

Sono disponibili diverse configurazioni pronte all’uso per l’integrazione con il servizio appropriato, ad esempio:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Puoi anche configurare una tua istanza di **Snippet generici di analisi** per definire una nuova configurazione di servizio.

Le informazioni vengono quindi raccolte da piccoli snippet di codice che vengono aggiunti alle pagine web. Ad esempio:

>[!CAUTION]
>
>Non racchiudere gli script in `script` tag.

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

Tali snippet consentono la raccolta dei dati e la generazione dei rapporti. I dati effettivi raccolti dipendono dal provider e dal frammento di codice effettivo utilizzato. Le statistiche di esempio includono:

* quanti visitatori nel tempo
* quante pagine visitate
* termini di ricerca utilizzati
* pagine di destinazione

>[!CAUTION]
>
>Il sito demo Geometrixx-Outdoors è configurato in modo che gli attributi forniti nelle Proprietà pagina vengano aggiunti al codice sorgente html (appena sopra il `</html>` tag di fine) nel `js` script.
>
>Se il tuo `/apps` non ereditare dal componente pagina predefinito ( `/libs/foundation/components/page`) tu (o i tuoi sviluppatori) devi assicurarti che il corrispondente `js` Gli script sono inclusi, ad esempio, includendo `cq/cloudserviceconfigs/components/servicescomponents`o utilizzando un meccanismo simile.
>
>In caso contrario, nessuno dei servizi (Generico, Analytics, Target e così via) funzionerà.

## Creazione di un servizio con uno snippet generico {#creating-a-new-service-with-a-generic-snippet}

Per la configurazione di base:

1. Apri **Strumenti** console.
1. Dal riquadro sinistro espandere **Configurazioni Cloud Service**.
1. Doppio clic **Snippet generico di analisi** per aprire la pagina:

   ![Snippet generico di analisi](assets/analytics_genericoverview.png)

1. Fate clic su + per aggiungere una nuova configurazione utilizzando la finestra di dialogo. Come minimo, assegna un nome, ad esempio Google Analytics:

   ![Creare la configurazione](assets/analytics_addconfig.png)

1. Clic **Crea**, la finestra di dialogo snippet si apre immediatamente - incolla lo snippet JavaScript appropriato nel campo:

   ![Modifica del componente](assets/analytics_snippet.png)

1. Clic **OK** per salvare.

## Utilizzo del nuovo servizio nelle pagine {#using-your-new-service-on-pages}

Dopo aver creato la configurazione del servizio, è ora necessario configurare le pagine richieste per utilizzarla:

1. Passa alla pagina.
1. Apri **Proprietà pagina** dalla barra laterale, quindi **Cloud Service** scheda.
1. Clic **Aggiungi servizio**, quindi seleziona il servizio richiesto. Ad esempio, il **Snippet generico di analisi**:

   ![Aggiunta di un servizio cloud](assets/analytics_selectservice.png)

1. Clic **OK** per salvare.
1. Viene visualizzata di nuovo la **Cloud Service** scheda. Il **Snippet generico di analisi** è ora elencato con il messaggio `Configuration reference missing`. Utilizza l’elenco a discesa per selezionare la tua istanza di servizio specifica. Ad esempio, google-analytics:

   ![Aggiunta della configurazione del servizio cloud](assets/analytics_selectspecificservice.png)

1. Clic **OK** per salvare.

   Lo snippet può ora essere visualizzato se si visualizza l’Origine pagina della pagina.

   Trascorso un certo periodo di tempo, puoi visualizzare le statistiche raccolte.

   >[!NOTE]
   >
   >Se la configurazione è associata a una pagina che ha pagine figlie, il servizio viene ereditato anche da queste.
