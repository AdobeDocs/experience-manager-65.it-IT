---
title: Diagnostica ContextHub
seo-title: ContextHub Diagnostics
description: ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub
seo-description: ContextHub provides a diagnostics page where you can see an overview of the ContextHub framework
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Diagnostica ContextHub {#contexthub-diagnostics}

ContextHub fornisce una pagina di diagnostica in cui puoi visualizzare una panoramica del framework ContextHub. Per aprire la pagina, vai al `contexthub.diagnostics.html` pagina dell’istanza dell’autore AEM, ad esempio:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

La pagina Diagnostica ContextHub fornisce informazioni sugli archivi e i moduli di interfaccia utente creati, sulle cartelle della libreria client caricate e sui collegamenti a pagine utili.

>[!NOTE]
>
>Per restituire le informazioni di diagnostica, è necessario attivare la modalità di debug. In caso contrario, la pagina di diagnostica sarà vuota. Consulta [questo documento](ch-configuring.md#debugging-contexthub) per informazioni dettagliate su come abilitare la modalità di debug.

>[!NOTE]
>
>Per le configurazioni ContextHub ancora presenti nei percorsi legacy, la posizione della pagina di diagnostica è `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Negozi {#stores}

La sezione Archivi elenca tutti gli store ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** Il [tipo di archivio](/help/sites-developing/ch-samplestores.md) su cui si basa il negozio.
* **percorso:** Percorso del nodo dell’archivio che contiene la configurazione.
* **resourceType:** Percorso del nodo dell’archivio in cui è definito il tipo di archivio.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di archivio.

## Moduli {#modules}

La sezione Moduli elenca tutti i moduli dell’interfaccia utente ContextHub configurati. Ogni voce dell&#39;elenco è costituita dalle seguenti informazioni:

* **Titolo:** Il [Tipo di modulo interfaccia utente](/help/sites-developing/ch-samplemodules.md) su cui si basa il modulo dell’interfaccia utente.
* **percorso:** Percorso del nodo dell’archivio che contiene la configurazione.
* **resourceType:** Percorso del nodo dell’archivio in cui è definito il tipo di modulo dell’interfaccia utente.
* **clientlibs:** Le categorie delle librerie client caricate che implementano il tipo di modulo dell’interfaccia utente.

## Clientlibs {#clientlibs}

La sezione Clientlibs elenca tutte le cartelle della libreria client caricate da ContextHub. Le librerie client sono suddivise in categorie:

* **kernel.js:** Librerie client che implementano il framework ContextHub, il motore di segmenti e i tipi di archivio.
* **ui.js:** Librerie client che implementano i tipi di moduli UI e interfaccia utente di ContextHub.
* **style.css:** File CSS caricati dalle librerie client.

## URL {#urls}

La sezione URL contiene collegamenti alle funzioni di ContextHub:

* **Editor configurazione:** Apre il [Pagina Configurazione ContextHub](ch-configuring.md) dove è possibile configurare store, modalità di interfaccia utente e moduli di interfaccia utente.

* **Configurazione dei moduli ContextHub:** Apre il file /etc/cloudsettings/default/contexthub.config.kernel.js, che contiene la rappresentazione dell’oggetto JavaScript delle configurazioni dell’archivio ContextHub.
* **Configurazione dell’interfaccia utente di ContextHub:** Apre il file /etc/cloudsettings/default/contexthub.config.ui.js, che contiene la rappresentazione dell’oggetto JavaScript delle configurazioni della modalità di interfaccia utente di ContextHub.
* **kernel.js:** Apre il file /etc/cloudsettings/default/contexthub.kernel.js, che contiene il codice sorgente delle librerie client che implementano il framework ContextHub, il motore dei segmenti e i tipi di archivio.
* **ui.js:** Apre il file /etc/cloudsettings/default/contexthub.ui.js, che contiene il codice sorgente delle librerie client che implementano i tipi di moduli UI e interfaccia utente di ContextHub.
* **style.css:** Apre il file /etc/cloudsettings/default/contexthub.styles.css, che contiene gli stili CSS per i moduli interfaccia utente e ContextHub.
