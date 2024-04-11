---
title: Authoring
description: Concetti di authoring e pubblicazione in Adobe Experience Manager 6.5.
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 28%

---

# Authoring{#authoring}

## Concetto di authoring (e pubblicazione) {#concept-of-authoring-and-publishing}

L’AEM offre due ambienti:

* Autore
* Pubblicazione

Questi interagiscono tra di loro e consentono di rendere i contenuti disponibili sul sito web, in modo che i visitatori possano leggerli.

L’ambiente di authoring fornisce le funzioni necessarie per creare, aggiornare e rivedere i contenuti prima che vengano pubblicati:

* Un autore crea e rivede il contenuto (che può essere di diversi tipi: pagine, risorse, pubblicazioni e così via)
* che, a un certo punto, sarà pubblicato sul tuo sito web.

![Panoramica degli ambienti](assets/chlimage_1-132.png)

Nell’ambiente di authoring, le funzionalità dell’AEM sono rese disponibili tramite due interfacce utente. Nell’ambiente di pubblicazione vengono invece progettati l’aspetto e il comportamento dell’interfaccia presentata agli utenti.

### Ambiente di authoring {#author-environment}

L’autore lavora in ciò che è noto come **ambiente di authoring**. Questo fornisce un’interfaccia di facile utilizzo (interfaccia grafica utente (GUI o UI)) per la creazione dei contenuti. Si trova dietro un firewall aziendale che fornisce protezione completa e richiede all’autore di accedere, utilizzando un account a cui sono stati assegnati i diritti di accesso appropriati.

>[!NOTE]
>
>Per creare, modificare o pubblicare contenuti, il tuo account deve disporre dei diritti di accesso appropriati.

A seconda della configurazione dell’istanza e dei diritti di accesso personali, puoi eseguire molte attività sul contenuto, tra cui (tra le altre):

* generare nuovo contenuto o modificare contenuto esistente in una pagina
* utilizzare modelli predefiniti per creare nuove pagine di contenuto
* creare, modificare e gestire risorse e raccolte
* creare, modificare e gestire le pubblicazioni
* sviluppare le campagne e le risorse correlate
* sviluppare e gestire siti community
* spostare, copiare o eliminare pagine di contenuto, risorse e così via
* pubblicare (o annullare la pubblicazione) pagine, risorse e così via

Sono anche disponibili attività amministrative per la gestione dei contenuti:

* flussi di lavoro che controllano il modo in cui vengono gestite le modifiche; ad esempio, imporre una revisione prima della pubblicazione
* progetti che coordinano singole attività

>[!NOTE]
>
>L&#39;AEM è anche [somministrato](/help/sites-administering/home.md) (per la maggior parte delle attività) dall’ambiente di authoring.

#### Ambiente di pubblicazione {#publish-environment}

Quando è pronto, il contenuto del sito AEM viene pubblicato in **ambiente di pubblicazione**. Qui le pagine del sito web vengono rese disponibili al pubblico di destinazione in base all’aspetto dell’interfaccia progettata.

Di solito, l&#39;ambiente di pubblicazione si trova all&#39;interno della zona demilitarizzata; in altre parole, disponibile a Internet, ma non più sotto la piena protezione della rete interna.

Quando il sito AEM è [sito community](/help/communities/overview.md), o include [Componenti community](/help/communities/author-communities.md), i visitatori del sito connessi (membri) possono interagire con le funzioni di Communities. Ad esempio, possono pubblicare in un forum, pubblicare un commento o seguire altri membri. Ai membri può essere concessa l&#39;autorizzazione ad eseguire attività normalmente limitate all&#39;ambiente di authoring, come creare nuove pagine (gruppi della community), articoli di blog e moderare i post di altri membri.

>[!NOTE]
>
>Sfortunatamente a volte c&#39;è una sovrapposizione nella terminologia utilizzata. Ciò può accadere con:
>
>* **Pubblicare/Annullare la pubblicazione**
>  Termini principali per le azioni che consentono di rendere o meno i contenuti disponibili al pubblico nell’ambiente di pubblicazione.
>
>* **Attivare/Disattivare**
>  Sinonimi di pubblicare/annullare la pubblicazione.
>
>* **Replicare/Replica**
>  Questi sono i termini tecnici utilizzati per indicare lo spostamento di dati (ad esempio contenuto di una pagina, file, codice e commenti degli utenti) da un ambiente all’altro, ovvero durante la pubblicazione o la replica inversa di commenti degli utenti.
>

#### Dispatcher {#dispatcher}

Per ottimizzare le prestazioni per i visitatori del sito Web, il **[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it)** implementa il bilanciamento del carico e il caching.
