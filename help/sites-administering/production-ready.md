---
title: Esecuzione di AEM in modalità pronta per la produzione
seo-title: Esecuzione di AEM in modalità pronta per la produzione
description: Scopri come eseguire AEM in modalità pronta per la produzione.
seo-description: Scopri come eseguire AEM in modalità pronta per la produzione.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Esecuzione di AEM in modalità pronta per la produzione{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe introduce la nuova `"nosamplecontent"` modalità di esecuzione che automatizza i passaggi necessari per preparare un’istanza di AEM da distribuire in un ambiente di produzione.

La nuova modalità di esecuzione non solo configurerà automaticamente l&#39;istanza per aderire alle best practice di protezione descritte nella lista di controllo di sicurezza, ma rimuoverà anche tutte le applicazioni e le configurazioni geometrixx campione nel processo.

>[!NOTE]
>
>Poiché, per motivi pratici, la modalità AEM Production Ready copre solo la maggior parte delle attività necessarie per proteggere un&#39;istanza, si consiglia vivamente di consultare la [lista](/help/sites-administering/security-checklist.md) di controllo prima di iniziare a utilizzare l&#39;ambiente di produzione.
>
>Inoltre, l&#39;esecuzione di AEM in modalità pronta per la produzione comporterà la disattivazione dell&#39;accesso a CRXDE Lite. Se necessario per il debug, consultate [Abilitazione di CRXDE Lite in AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Per eseguire AEM in modalità pronta per la produzione, è sufficiente aggiungere lo switch `nosamplecontent` in modalità `-r` di esecuzione agli argomenti di avvio esistenti:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Ad esempio, potete utilizzare la produzione pronta per avviare un&#39;istanza di creazione con la persistenza MongoDB come segue:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte della modalità Produzione pronta {#changes-part-of-the-production-ready-mode}

Più precisamente, le seguenti modifiche alla configurazione verranno eseguite quando AEM viene eseguito in modalità pronta per la produzione:

1. Il pacchetto **CRXDE Support** ( `com.adobe.granite.crxde-support`) è disabilitato per impostazione predefinita in modalità pronta per la produzione. Può essere installato in qualsiasi momento dal repository di Adobe public Maven. Per AEM 6.1 è richiesta la versione 3.0.0.

1. Il pacchetto **Apache Sling Simple WebDAV Access to repository** ( `org.apache.sling.jcr.webdav`) sarà disponibile solo sulle istanze **dell&#39;autore** .

1. Gli utenti appena creati dovranno cambiare la password al primo login. Ciò non vale per l&#39;utente amministratore.
1. **La generazione di informazioni** di debug è disabilitata per il gestore **di script Java** Apache.

1. **Il contenuto** mappato e **le informazioni** di debug generate sono disabilitate per il gestore **di script JSP** Apache Sling.

1. Il filtro **** Day CQ WCM è impostato su `edit` per l’ **autore** e `disabled` sulle istanze **pubblicate** .

1. **Adobe Granite HTML Library Manager** è configurato con le seguenti impostazioni:

   1. **** Riduci: `enabled`
   1. **** Debug: `disabled`
   1. **** Gzip: `enabled`
   1. **** Tempo: `disabled`

1. Il Servlet **** Apache Sling GET è impostato per supportare le configurazioni sicure per impostazione predefinita, come segue:

| **Configurazione** | **Authoring** | **Pubblicazione** |
|---|---|---|
| Rendering TXT | disattivato | disattivato |
| Rendering HTML | disattivato | disattivato |
| Rendering JSON | abilitato | abilitato |
| Rendering XML | disattivato | disattivato |
| json.maximumresult | 1000 | 100 |
| Indice automatico | disattivato | disattivato |

