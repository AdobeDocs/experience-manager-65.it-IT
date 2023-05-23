---
title: Authoring
seo-title: Authoring
description: Concetti relativi all’authoring in AEM
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 25%

---

# Authoring  {#authoring}

## Concetto di authoring (e pubblicazione) {#concept-of-authoring-and-publishing}

L’AEM offre due ambienti:

* Autore
* Pubblicazione

Questi interagiscono tra di loro e consentono di rendere i contenuti disponibili sul sito web, in modo che i visitatori possano leggerli.

L’ambiente di authoring fornisce i meccanismi per creare, aggiornare e rivedere questo contenuto prima di pubblicarlo:

* Un autore crea e rivede il contenuto (che può essere di diversi tipi; ad esempio pagine, risorse, pubblicazioni, ecc.)
* che, a un certo punto, sarà pubblicato sul tuo sito web.

![chlimage_1-132](assets/chlimage_1-132.png)

Nell’ambiente di authoring le funzionalità dell’AEM sono rese disponibili tramite due interfacce utente. Nell’ambiente di pubblicazione vengono invece progettati l’aspetto e il comportamento dell’interfaccia presentata agli utenti.

### Ambiente di authoring {#author-environment}

L’autore utilizza il cosiddetto **ambiente di authoring**, che fornisce un’interfaccia, grafica o normale, di facile utilizzo per la creazione dei contenuti. In genere si trova dietro il firewall di un’azienda che fornisce protezione completa e richiede all’autore di effettuare l’accesso, utilizzando un account a cui sono stati assegnati i diritti di accesso appropriati.

>[!NOTE]
>
>Il tuo account necessita dei diritti di accesso appropriati per creare, modificare o pubblicare contenuti.

A seconda della configurazione dell’istanza e dei diritti di accesso personali, puoi eseguire molte attività sul contenuto, tra cui:

* generare nuovo contenuto o modificare contenuto esistente in una pagina
* utilizzare modelli predefiniti per creare nuove pagine di contenuto
* creare, modificare e gestire risorse e raccolte
* creare, modificare e gestire le pubblicazioni
* sviluppare le campagne e le risorse correlate
* sviluppare e gestire siti community
* spostare, copiare o eliminare pagine di contenuti, risorse e così via
* pubblicare (o annullare la pubblicazione) pagine, risorse, ecc.

Sono inoltre disponibili attività amministrative per la gestione dei contenuti:

* flussi di lavoro che controllano la modalità di gestione delle modifiche, ad esempio. imposizione di una revisione prima della pubblicazione
* progetti che coordinano singole attività

>[!NOTE]
>
>L&#39;AEM è anche [somministrato](/help/sites-administering/home.md) (per la maggior parte delle attività) dall’ambiente di authoring.

#### Ambiente di pubblicazione {#publish-environment}

Quando è pronto, il contenuto del sito AEM viene pubblicato in **ambiente di pubblicazione**. Qui le pagine del sito web vengono rese disponibili al pubblico di destinazione in base all’aspetto dell’interfaccia progettata.

Di solito, l&#39;ambiente di pubblicazione si trova all&#39;interno della zona demilitarizzata; in altre parole, disponibile a Internet, ma non più sotto la piena protezione della rete interna.

Quando il sito AEM è [sito community](/help/communities/overview.md), o include [Componenti community](/help/communities/author-communities.md), i visitatori del sito connessi (membri) possono interagire con le funzioni di Communities. Ad esempio, possono pubblicare in un forum, pubblicare un commento o seguire altri membri. Ai membri può essere concessa l&#39;autorizzazione per eseguire attività normalmente limitate all&#39;ambiente di authoring, ad esempio creare nuove pagine (gruppi della community), articoli di blog e moderare i post di altri membri.

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
   >  Questi sono i termini tecnici utilizzati per indicare lo spostamento di dati (ad esempio contenuto di una pagina, file, codice e commenti degli utenti) da un ambiente all’altro, ad esempio durante la pubblicazione o la replica inversa di commenti degli utenti.
>


#### Dispatcher {#dispatcher}

Per ottimizzare le prestazioni dal punto di vista dei visitatori del sito web, vengono usati **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) che implementano funzioni di bilanciamento del carico e memorizzazione in cache.**
