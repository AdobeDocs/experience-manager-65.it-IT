---
title: Mappatura delle risorse
description: Scopri come definire reindirizzamenti, URL personalizzati e host virtuali per Adobe Experience Manager utilizzando la mappatura delle risorse.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%
---
# Mappatura delle risorse{#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per Adobe Experience Manager (AEM).

Ad esempio, puoi utilizzare queste mappature per:

* Aggiungi il prefisso `/content` a tutte le richieste in modo che la struttura interna sia nascosta ai visitatori del tuo sito Web.
* Definisci un reindirizzamento in modo che tutte le richieste alla pagina `/content/en/gateway` del sito Web vengano reindirizzate a `https://gbiv.com/`.

Un possibile prefisso di mappatura HTTP per tutte le richieste a `localhost:4503` con `/content`. Una mappatura come questa può essere utilizzata per nascondere la struttura interna dai visitatori al sito web in quanto consente:

`localhost:4503/content/we-retail/en/products.html`

Da accedere tramite:

`localhost:4503/we-retail/en/products.html`

Poiché il mapping aggiunge automaticamente il prefisso `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Gli URL personalizzati non supportano i pattern regex.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione di Sling e [Mapping per la risoluzione delle risorse](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) e [Risorse](https://sling.apache.org/documentation/the-sling-engine/resources.html).

## Visualizzazione delle definizioni di mappatura {#viewing-mapping-definitions}

Le mappature formano due elenchi che JCR Resource Resolver valuta (dall’alto verso il basso) per trovare una corrispondenza.

Questi elenchi possono essere visualizzati (insieme alle informazioni di configurazione) nell&#39;opzione **JCR ResourceResolver** della console Felix; ad esempio, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configurazione
Mostra la configurazione corrente (come definita per [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Prova di configurazione
Questo ti consente di immettere un URL o un percorso di risorsa. Fai clic su **Risolvi** o **Mappa** per confermare la modalità di trasformazione della voce da parte del sistema.

* **Voci mappa risolutore**
Elenco di voci utilizzate dai metodi ResourceResolver.resolve per mappare gli URL alle risorse.

* **Voci mapping**
Elenco di voci utilizzate dai metodi ResourceResolver.map per mappare i percorsi delle risorse agli URL.

I due elenchi mostrano varie voci, comprese quelle definite come predefinite dalle applicazioni. Queste servono spesso a semplificare gli URL dell’utente.

Gli elenchi associano un **Pattern**, un&#39;espressione regolare corrispondente alla richiesta, con un **Replacement** che definisce il reindirizzamento da imporre.

Ad esempio:

**Pattern** `^[^/]+/[^/]+/welcome$`

Attiva:

**Sostituzione** `/libs/cq/core/content/welcome.html`.

Per reindirizzare una richiesta:

`https://localhost:4503/welcome` &quot;

A:

`https://localhost:4503/libs/cq/core/content/welcome.html`

All’interno dell’archivio vengono create nuove definizioni di mappatura.

>[!NOTE]
>
>Sono disponibili molte risorse che spiegano come definire le espressioni regolari. Ad esempio, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creazione di definizioni di mappatura in AEM {#creating-mapping-definitions-in-aem}

In un’installazione standard di AEM puoi trovare la cartella:

`/etc/map/http`

Struttura utilizzata per definire le mappature per il protocollo HTTP. È possibile creare altre cartelle ( `sling:Folder`) in `/etc/map` per qualsiasi altro protocollo che si desidera mappare.

#### Configurazione di un reindirizzamento interno a /content {#configuring-an-internal-redirect-to-content}

Per creare il mapping con il prefisso `/content` per qualsiasi richiesta a https://localhost:4503/:

1. Utilizzando CRXDE passa a `/etc/map/http`.

1. Crea un nodo:

   * **Tipo** `sling:Mapping`
     Questo tipo di nodo è destinato a tali mappature, anche se il suo utilizzo non è obbligatorio.

   * **Nome** `localhost_any`

1. Fare clic su **Salva tutto**.
1. **Aggiungi** le seguenti proprietà a questo nodo:

   * **Nome** `sling:match`

     * **Tipo** `String`

     * **Valore** `localhost.4503/`

   * **Nome** `sling:internalRedirect`

     * **Tipo** `String[]`

     * **Valore** `/content/`

1. Fare clic su **Salva tutto**.

Questo gestisce una richiesta come:
`localhost:4503/geometrixx/en/products.html`
come se:
`localhost:4503/content/geometrixx/en/products.html`
è stato richiesto.

>[!NOTE]
>
>Consulta [Risorse](https://sling.apache.org/documentation/the-sling-engine/resources.html) nella documentazione di Sling per ulteriori informazioni sulle proprietà sling disponibili e su come configurarle.

>[!NOTE]
>
>È possibile utilizzare `/etc/map.publish` per mantenere le configurazioni per l&#39;ambiente di pubblicazione. Questi devono essere replicati e la nuova posizione ( `/etc/map.publish`) configurata per il **Percorso mappatura** del [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) dell&#39;ambiente di pubblicazione.
