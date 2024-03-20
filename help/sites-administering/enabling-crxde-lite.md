---
title: Abilitazione di CRXDE Liti nell’AEM
description: Scopri come abilitare CRXDE Liti in Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Abilitazione di CRXDE Liti nell’AEM{#enabling-crxde-lite-in-aem}

Per garantire la massima sicurezza possibile delle installazioni AEM, gli elenchi di controllo per la sicurezza raccomandano [disattivazione di WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) negli ambienti di produzione.

Tuttavia, CRXDE Liti dipende dalla `org.apache.sling.jcr.davex` per funzionare correttamente, in modo che la disattivazione di WebDAV disabiliti efficacemente anche CRXDE Liti.

In questo caso, cerca in `https://serveraddress:4502/crx/de/index.jsp` mostrerà un nodo principale vuoto e tutte le richieste HTTP alle risorse CRXDE Liti avranno esito negativo:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Anche se questo consiglio ha lo scopo di ridurre il più possibile le superfici di attacco, gli amministratori di sistema a volte potrebbero aver bisogno dell’accesso a CRXDE Liti per sfogliare il contenuto o eseguire il debug dei problemi sulle istanze di produzione.

È possibile abilitare CRXDE Liti con [Impostazioni OSGi](#enabling-crxde-lite-osgi) o con un [comando cURL](#enabling-crxde-lite-curl).

>[!WARNING]
>
>A causa di lievi differenze nel funzionamento di questi metodi, è necessario utilizzare ***o*** OSGI ***o*** cURL.
>
>I due metodi sono ***non*** intercambiabile.

## Abilitazione di CRXDE Liti con OSGI {#enabling-crxde-lite-osgi}

Se è disattivato, puoi attivare CRXDE Liti seguendo la procedura seguente:

1. Vai alla console Componenti OSGi all’indirizzo `http://localhost:4502/system/console/components`
1. Cerca il seguente componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Fai clic sull’icona a forma di chiave inglese accanto ad essa per visualizzarne le opzioni di configurazione:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Crea la seguente configurazione:

   * **Percorso directory principale:** `/crx/server`
   * Seleziona la casella sotto **Usa URI assoluti**.

1. Al termine dell&#39;utilizzo di CRXDE Liti, assicurarsi di disabilitare nuovamente WebDAV.

## Abilitazione di CRXDE Liti con cURL {#enabling-crxde-lite-curl}

Puoi anche abilitare CRXDE Liti tramite cURL, eseguendo questo comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Altre risorse {#other-resources}

Per ulteriori informazioni sulle funzioni di sicurezza dell’AEM 6, consulta le pagine seguenti:

* [Elenco di controllo della sicurezza AEM](/help/sites-administering/security-checklist.md)
* [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md)
