---
title: Abilitazione di CRXDE Lite in AEM
seo-title: Abilitazione di CRXDE Lite in AEM
description: Come abilitare CRXDE Lite in AEM.
seo-description: Come abilitare CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d

---


# Abilitazione di CRXDE Lite in AEM{#enabling-crxde-lite-in-aem}

Per garantire che le installazioni di AEM siano il più sicure possibile, la lista di controllo di sicurezza consiglia di [disattivare WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) negli ambienti di produzione.

Tuttavia, CRXDE Lite dipende dal `org.apache.sling.jcr.davex` bundle per funzionare correttamente, quindi disabilitando WebDAV si disattiverà in modo efficace anche CRXDE Lite.

In questo caso, la navigazione in `https://serveraddress:4502/crx/de/index.jsp` visualizzerà un nodo principale vuoto e tutte le richieste HTTP alle risorse CRXDE Lite avranno esito negativo:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Sebbene questa raccomandazione sia intesa a ridurre il più possibile le superfici di attacco, gli amministratori di sistema potrebbero talvolta dover accedere a CRXDE Lite per cercare il contenuto o risolvere i problemi relativi alle istanze di produzione.

Se disabilitato, è possibile attivare CRXDE Lite seguendo la procedura seguente:

1. Passate alla console Componenti OSGi all’indirizzo `http://localhost:4502/system/console/components`
1. Cerca il componente seguente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Fate clic sull’icona chiave inglese accanto a essa per visualizzarne le opzioni di configurazione:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Create la configurazione seguente:

   * **Percorso directory principale:** `/crx/server`
   * Fare clic sulla casella in **Usa URI** assoluti.

1. Quando avete finito di utilizzare CRXDE Lite, accertatevi di disabilitare di nuovo WebDAV.

È inoltre possibile abilitare CRXDE Lite tramite cURL, eseguendo questo comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Altre risorse {#other-resources}

Per ulteriori informazioni sulle funzioni di sicurezza di AEM 6, consultate le pagine seguenti:

* [Elenco di controllo AEM Security](/help/sites-administering/security-checklist.md)
* [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md)

