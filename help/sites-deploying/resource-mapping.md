---
title: Mapping delle risorse
seo-title: Mapping delle risorse
description: Scoprite come definire reindirizzamenti, URL personalizzati e host virtuali per AEM utilizzando la mappatura delle risorse.
seo-description: Scoprite come definire reindirizzamenti, URL personalizzati e host virtuali per AEM utilizzando la mappatura delle risorse.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---


# Mapping risorse{#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per AEM.

Ad esempio, è possibile utilizzare queste mappature per:

* Aggiungi un prefisso a tutte le richieste con `/content` in modo che la struttura interna sia nascosta ai visitatori del sito Web.
* Definite un reindirizzamento in modo che tutte le richieste alla pagina `/content/en/gateway` del sito Web vengano reindirizzate a `https://gbiv.com/`.

Una possibile mappatura HTTP prefissa tutte le richieste a `localhost:4503` con `/content`. Una mappatura di questo tipo potrebbe essere utilizzata per nascondere la struttura interna dai visitatori al sito Web, così come consente:

`localhost:4503/content/we-retail/en/products.html`

per l’accesso tramite:

`localhost:4503/we-retail/en/products.html`

poiché la mappatura aggiunge automaticamente il prefisso `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Gli URL personalizzati non supportano i pattern regolari.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione Sling e [Mappature per la risoluzione delle risorse](https://sling.apache.org/site/resources.html) e [Risorse](https://sling.apache.org/site/mappings-for-resource-resolution.html).

## Visualizzazione delle definizioni di mapping {#viewing-mapping-definitions}

Le mappature sono due elenchi che il Risolutore risorse JCR valuta (dall&#39;alto verso il basso) per trovare una corrispondenza.

Questi elenchi possono essere visualizzati (insieme alle informazioni di configurazione) nell&#39;opzione **JCR ResourceResolver** della console Felix; ad esempio, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configurazione
Mostra la configurazione corrente (come definito per il [Risolutore risorse Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Test di configurazione
Consente di inserire un URL o un percorso di risorsa. Fare clic su **Resolve** o **Map** per confermare come il sistema trasformerà la voce.

* **Risolutore**
Voci mappaElenco di voci utilizzate dai metodi ResourceResolver.resolve per mappare gli URL sulle risorse.

* **Mappatura**
voci mappaElenco di voci utilizzate dai metodi ResourceResolver.map per mappare i percorsi delle risorse agli URL.

I due elenchi mostrano varie voci, comprese quelle definite come predefinite dalle applicazioni. Spesso con lo scopo di semplificare gli URL per l’utente.

Gli elenchi associano un **Pattern**, un&#39;espressione regolare associata alla richiesta, con un **Sostituzione** che definisce il reindirizzamento da imporre.

Ad esempio:

**Pattern** `^[^/]+/[^/]+/welcome$`

attiverà:

**Sostituzione** `/libs/cq/core/content/welcome.html`.

per reindirizzare una richiesta:

`https://localhost:4503/welcome` ``

a:

`https://localhost:4503/libs/cq/core/content/welcome.html`

All&#39;interno dell&#39;archivio vengono create nuove definizioni di mapping.

>[!NOTE]
>
>Sono disponibili numerose risorse che spiegano come definire le espressioni regolari; ad esempio [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creazione di definizioni di mapping in AEM {#creating-mapping-definitions-in-aem}

In un’installazione standard di AEM potete trovare la cartella:

`/etc/map/http`

Questa è la struttura utilizzata per definire le mappature per il protocollo HTTP. È possibile creare altre cartelle ( `sling:Folder`) in `/etc/map` per qualsiasi altro protocollo da mappare.

#### Configurazione di un reindirizzamento interno a /content {#configuring-an-internal-redirect-to-content}

Per creare la mappatura che prefissa qualsiasi richiesta a https://localhost:4503/ con `/content`:

1. Utilizzando CRXDE, passare a `/etc/map/http`.

1. Crea un nuovo nodo:

   * **** `sling:Mapping`
Tipo: questo tipo di nodo è destinato a tali mappature, anche se il suo utilizzo non è obbligatorio.

   * **Nome** `localhost_any`

1. Fare clic su **Salva tutto**.
1. **A questo nodo** sono state aggiunte le seguenti proprietà:

   * **Nome** `sling:match`

      * **Tipo** `String`

      * **Valore** `localhost.4503/`
   * **Nome** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valore** `/content/`


1. Fare clic su **Salva tutto**.

Questo gestirà una richiesta come:
`localhost:4503/geometrixx/en/products.html`
come se:
`localhost:4503/content/geometrixx/en/products.html`
era stato richiesto.

>[!NOTE]
>
>Per ulteriori informazioni sulle proprietà di sling disponibili e su come configurarle, vedere [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) nella documentazione Sling.

>[!NOTE]
>
>Potete utilizzare `/etc/map.publish` per mantenere le configurazioni dell&#39;ambiente di pubblicazione. Devono quindi essere replicati e la nuova posizione ( `/etc/map.publish`) configurata per la **posizione di mappatura** di [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) dell&#39;ambiente di pubblicazione.

