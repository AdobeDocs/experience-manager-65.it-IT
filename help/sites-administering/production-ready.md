---
title: Esecuzione di AEM in modalità pronta per la produzione
seo-title: Running AEM in Production Ready Mode
description: Scopri come eseguire AEM in modalità Produzione pronta.
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 4%

---

# Esecuzione di AEM in modalità pronta per la produzione{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe introduce il nuovo `"nosamplecontent"` runmode mirava ad automatizzare i passaggi necessari per preparare un&#39;istanza AEM per la distribuzione in un ambiente di produzione.

La nuova modalità runmode non solo configurerà automaticamente l&#39;istanza per aderire alle best practice di sicurezza descritte nella lista di controllo della sicurezza, ma rimuoverà anche tutte le applicazioni e configurazioni geometrixx campione nel processo.

>[!NOTE]
>
>Poiché, per motivi pratici, la modalità Produzione pronta AEM copre solo la maggior parte delle attività necessarie per proteggere un&#39;istanza, si consiglia vivamente di consultare la [Lista di controllo sicurezza](/help/sites-administering/security-checklist.md) prima di iniziare a lavorare con l&#39;ambiente di produzione.
>
>Inoltre, l’esecuzione di AEM in modalità pronta per la produzione disattiverà efficacemente l’accesso ad CRXDE Lite. Se necessario a scopo di debug, consulta [Abilitazione di CRXDE Lite in AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Per eseguire AEM in modalità pronta per la produzione, è sufficiente aggiungere il comando `nosamplecontent` tramite `-r` passa alla modalità runmode per gli argomenti di avvio esistenti:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Ad esempio, puoi utilizzare la produzione pronta per avviare un&#39;istanza di authoring con persistenza MongoDB come questa:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte della modalità pronta per la produzione {#changes-part-of-the-production-ready-mode}

Più specificamente, le seguenti modifiche di configurazione verranno eseguite quando si esegue AEM in modalità pronta per la produzione:

1. La **Bundle di supporto CRXDE** ( `com.adobe.granite.crxde-support`) è disabilitata per impostazione predefinita in modalità pronta per la produzione. Può essere installato in qualsiasi momento dall’archivio Maven pubblico Adobe. La versione 3.0.0 è necessaria per AEM 6.1.

1. La **Apache Sling Simple WebDAV Accesso agli archivi** ( `org.apache.sling.jcr.webdav`) il bundle sarà disponibile solo su **autore** istanze.

1. Gli utenti appena creati dovranno modificare la password al primo accesso. Questo non si applica all&#39;utente amministratore.
1. **Genera informazioni di debug** è disattivato per **Apache Sling Java Script Handler**.

1. **Contenuto mappato** e **Genera informazioni di debug** sono disattivati per **Apache Sling JSP Script Handler**.

1. La **Filtro WCM Day CQ** è impostato su `edit` su **autore** e `disabled` su **pubblicare** istanze.

1. La **Adobe Granite HTML Library Manager** è configurato con le seguenti impostazioni:

   1. **Minimizza:** `enabled`
   1. **Debug:** `disabled`
   1. **Gzip:** `enabled`
   1. **Tempo:** `disabled`

1. La **Servlet Apache Sling GET** è impostato per supportare le configurazioni sicure per impostazione predefinita, come segue:

| **Configurazione** | **Autore** | **Pubblicazione** |
|---|---|---|
| Rendering TXT | disattivato | disattivato |
| rendering di HTML | disattivato | disattivato |
| Rendering JSON | abilitato | abilitato |
| Rendering XML | disattivato | disattivato |
| json.maximumresults | 1000 | 100 |
| Indice automatico | disattivato | disattivato |
