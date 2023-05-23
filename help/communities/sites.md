---
title: Modelli per siti
seo-title: Site Templates
description: Come accedere alla console Modelli di sito
seo-description: How to access the Site Templates console
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 4%

---

# Modelli per siti {#site-templates}

La console Modelli di sito è molto simile alla [Modelli per gruppi](tools-groups.md) , che si concentra su funzioni di interesse per i gruppi comunitari.

>[!NOTE]
>
>Le console per la creazione di [siti community](sites-console.md), [modelli per sito community](sites.md), [modelli per gruppi community](tools-groups.md) e [funzioni community](functions.md) devono essere utilizzati solo nell’ambiente di authoring.

## Console modelli sito {#site-templates-console}

Nell’ambiente di authoring, per raggiungere la console dei siti della community:

* Dalla navigazione globale: **[!UICONTROL Strumenti > Community > Modelli del sito]**

In questa console vengono visualizzati i modelli da cui [sito community](sites-console.md) può essere creato e consente di creare nuovi modelli di sito.

![site-template](assets/site-template.png)

## Crea modello sito {#create-site-template}

Per iniziare a creare un nuovo modello di sito, seleziona `Create`.

Viene visualizzato il pannello Editor sito, che contiene 3 pannelli secondari:

### Informazioni di base {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

Nel pannello Informazioni di base, vengono configurati un nome, una descrizione e se il modello è abilitato o disabilitato:

* **[!UICONTROL Nome modello per sito community]**

   ID del nome del modello.

* **[!UICONTROL Descrizione modello per sito community]**

   Descrizione del modello.

* **[!UICONTROL Disabilitato/abilitato]**

   Un interruttore che controlla se il modello è referenziabile.

### Miniatura  {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Facoltativo) Seleziona l&#39;icona Carica immagine per mostrare una miniatura insieme al nome e alla descrizione ai creatori dei siti della community.

### Struttura {#structure}

![site-structure](assets/site-structure.png)

Per aggiungere funzioni di community, trascinare il puntatore del mouse dal lato destro a quello sinistro nell&#39;ordine in cui devono essere visualizzati i collegamenti del menu del sito. Gli stili verranno applicati al modello durante la creazione del sito.

Ad esempio, se desideri una home page, trascina la funzione Page dalla libreria e rilasciala nel generatore di modelli. Questo determina l’apertura della finestra di dialogo per la configurazione della pagina. Consulta la [console funzioni](functions.md) per informazioni sulle finestre di dialogo di configurazione.

Continuare a trascinare le altre funzioni community desiderate per un sito community basato su questo modello.

La funzione page fornisce una pagina vuota. La funzione gruppi consente di creare un sito di gruppo (sottocommunity) all’interno del sito community.

>[!CAUTION]
>
>La funzione dei gruppi deve *non* essere *primo e unico* nella struttura del sito.
>
>Qualsiasi altra funzione, ad esempio [funzione page](functions.md#page-function), deve essere incluso ed elencato per primo.

![site-editor](assets/site-editor.png)

### Modelli per gruppi per funzione Gruppi {#group-templates-for-groups-function}

Quando si include una funzione di gruppo nel modello di sito, la configurazione richiede la specifica delle scelte del modello di gruppo consentite quando viene creato un nuovo gruppo nell’ambiente di pubblicazione.

>[!CAUTION]
>
>La funzione Groups deve *non* essere *primo e unico* nella struttura del sito.

![site-functions](assets/site-functions.png)

Selezionando due o più modelli per gruppi community, l&#39;amministratore del gruppo può scegliere quando creare effettivamente un nuovo gruppo nella community.

![funzione-sito](assets/site-functions1.png)

## Modifica modello sito {#edit-site-template}

Quando si visualizzano i modelli di sito nel [Console Modelli del sito](#site-templates-console), è possibile selezionare un modello di sito esistente da modificare.

Questo processo fornisce gli stessi pannelli [creazione di un modello di sito](#create-site-template).
