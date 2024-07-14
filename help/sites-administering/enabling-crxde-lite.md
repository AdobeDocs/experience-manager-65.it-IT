---
title: Abilitazione di CRXDE Lite nell’AEM
description: Scopri come abilitare CRXDE Lite in Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Abilitazione di CRXDE Lite nell’AEM{#enabling-crxde-lite-in-aem}

Per garantire la massima protezione possibile delle installazioni AEM, l&#39;elenco di controllo della sicurezza consiglia di [disabilitare WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) negli ambienti di produzione.

Tuttavia, CRXDE Lite dipende dal funzionamento corretto del bundle `org.apache.sling.jcr.davex`, pertanto la disabilitazione di WebDAV disabiliterà effettivamente anche CRXDE Lite.

In questo caso, l&#39;esplorazione di `https://serveraddress:4502/crx/de/index.jsp` determinerà la visualizzazione di un nodo principale vuoto e tutte le richieste HTTP alle risorse CRXDE Lite avranno esito negativo:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Anche se questo consiglio ha lo scopo di ridurre il più possibile le superfici di attacco, gli amministratori di sistema a volte potrebbero aver bisogno dell’accesso a CRXDE Lite per sfogliare il contenuto o eseguire il debug dei problemi sulle istanze di produzione.

È possibile abilitare CRXDE Lite con [impostazioni OSGi](#enabling-crxde-lite-osgi) o con un comando [cURL](#enabling-crxde-lite-curl).

>[!WARNING]
>
>A causa di lievi differenze nel funzionamento di questi metodi, è necessario utilizzare ***o*** cURL OSGI ***o***.
>
>I due metodi sono ***non*** intercambiabili.

## Abilitazione di CRXDE Lite con OSGI {#enabling-crxde-lite-osgi}

Se è disattivato, puoi attivare CRXDE Lite seguendo la procedura seguente:

1. Passa alla console dei componenti OSGi in `http://localhost:4502/system/console/components`
1. Cerca il seguente componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Fai clic sull’icona a forma di chiave inglese accanto ad essa per visualizzarne le opzioni di configurazione:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Crea la seguente configurazione:

   * **Percorso principale:** `/crx/server`
   * Selezionare la casella in **Usa URI assoluti**.

1. Al termine dell&#39;utilizzo di CRXDE Lite, assicurarsi di disabilitare nuovamente WebDAV.

## Abilitazione di CRXDE Lite con cURL {#enabling-crxde-lite-curl}

Puoi anche abilitare CRXDE Lite tramite cURL, eseguendo questo comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Altre risorse {#other-resources}

Per ulteriori informazioni sulle funzioni di sicurezza dell’AEM 6, consulta le pagine seguenti:

* [Elenco di controllo della sicurezza AEM](/help/sites-administering/security-checklist.md)
* [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md)
