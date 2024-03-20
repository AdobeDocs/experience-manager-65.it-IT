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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Mappatura delle risorse{#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per Adobe Experience Manager (AEM).

Ad esempio, puoi utilizzare queste mappature per:

* Aggiungi il prefisso a tutte le richieste `/content` in modo che la struttura interna sia nascosta ai visitatori del sito web.
* Definisci un reindirizzamento in modo che tutte le richieste a `/content/en/gateway` pagina del sito web vengono reindirizzati a `https://gbiv.com/`.

Un possibile prefisso di mappatura HTTP per tutte le richieste a `localhost:4503` con `/content`. Una mappatura come questa può essere utilizzata per nascondere la struttura interna dai visitatori al sito web in quanto consente:

`localhost:4503/content/we-retail/en/products.html`

Da accedere tramite:

`localhost:4503/we-retail/en/products.html`

Poiché la mappatura aggiunge automaticamente il prefisso `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Gli URL personalizzati non supportano i pattern regex.

>[!NOTE]
>
>Consulta la documentazione di Sling e [Mappature per la risoluzione delle risorse](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) e [Risorse](https://sling.apache.org/documentation/the-sling-engine/resources.html) per ulteriori informazioni.

## Visualizzazione delle definizioni di mappatura {#viewing-mapping-definitions}

Le mappature formano due elenchi che JCR Resource Resolver valuta (dall’alto verso il basso) per trovare una corrispondenza.

Questi elenchi possono essere visualizzati (insieme alle informazioni di configurazione) nella sezione **ResourceResolver JCR** della console Felix; ad esempio, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configurazione Mostra la configurazione corrente (come definita per [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Test di configurazione Consente di immettere un URL o un percorso di risorsa. Clic **Risolvi** o **Mappa** per confermare la modalità di trasformazione della voce.

* **Voci mappa del resolver**
Elenco di voci utilizzate dai metodi ResourceResolver.resolve per mappare gli URL alle risorse.

* **Mappatura delle voci di mappa**
Elenco di voci utilizzate dai metodi ResourceResolver.map per mappare i percorsi delle risorse agli URL.

I due elenchi mostrano varie voci, comprese quelle definite come predefinite dalle applicazioni. Queste servono spesso a semplificare gli URL dell’utente.

La coppia di elenchi a **Pattern**, un’espressione regolare associata alla richiesta, con un **Sostituto** che definisce il reindirizzamento da imporre.

Ad esempio:

**Pattern** `^[^/]+/[^/]+/welcome$`

Attiva:

**Sostituto** `/libs/cq/core/content/welcome.html`.

Per reindirizzare una richiesta:

`https://localhost:4503/welcome` &quot;

A:

`https://localhost:4503/libs/cq/core/content/welcome.html`

All’interno dell’archivio vengono create nuove definizioni di mappatura.

>[!NOTE]
>
>Sono disponibili molte risorse che spiegano come definire le espressioni regolari. Ad esempio: [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creazione di definizioni di mappatura in AEM {#creating-mapping-definitions-in-aem}

In un’installazione standard di AEM puoi trovare la cartella:

`/etc/map/http`

Struttura utilizzata per definire le mappature per il protocollo HTTP. Altre cartelle ( `sling:Folder`) può essere creato in `/etc/map` per qualsiasi altro protocollo che desideri mappare.

#### Configurazione di un reindirizzamento interno a /content {#configuring-an-internal-redirect-to-content}

Per creare il mapping che aggiunge il prefisso a qualsiasi richiesta a https://localhost:4503/ `/content`:

1. Utilizzo di CRXDE passa a `/etc/map/http`.

1. Crea un nodo:

   * **Tipo** `sling:Mapping`
Questo tipo di nodo è destinato a tali mappature, anche se il suo utilizzo non è obbligatorio.

   * **Nome** `localhost_any`

1. Clic **Salva tutto**.
1. **Aggiungi** le seguenti proprietà di questo nodo:

   * **Nome** `sling:match`

      * **Tipo** `String`

      * **Valore** `localhost.4503/`

   * **Nome** `sling:internalRedirect`

      * **Tipo** `String[]`

      * **Valore** `/content/`

1. Clic **Salva tutto**.

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
>È possibile utilizzare `/etc/map.publish` per mantenere le configurazioni dell’ambiente di pubblicazione. Questi devono essere replicati e la nuova posizione ( `/etc/map.publish`) configurato per **Posizione mappatura** del [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) dell’ambiente di pubblicazione.
