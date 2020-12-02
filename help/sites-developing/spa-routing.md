---
title: Routing modello SPA
seo-title: Routing modello SPA
description: Per le applicazioni a pagina singola in AEM, l'app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.
seo-description: Per le applicazioni a pagina singola in AEM, l'app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# SPA ciclo del modello{#spa-model-routing}

Per le applicazioni a pagina singola in AEM, l&#39;app è responsabile del routing. Questo documento descrive il meccanismo di routing, il contratto e le opzioni disponibili.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Routing del progetto {#project-routing}

L&#39;app è proprietaria del routing e viene quindi implementata dagli sviluppatori front-end del progetto. Questo documento descrive il ciclo specifico per il modello restituito dal server AEM. La struttura dati del modello di pagina espone l&#39;URL della risorsa sottostante. Il progetto front-end può utilizzare qualsiasi libreria personalizzata o di terze parti che fornisce funzionalità di routing. Una volta che una route prevede un frammento di modello, è possibile effettuare una chiamata alla funzione `PageModelManager.getData()`. Quando un ciclo di lavorazione del modello ha modificato un evento deve essere attivato per avvertire le librerie di ascolto come Editor pagina.

## Architettura {#architecture}

Per una descrizione dettagliata, fare riferimento alla sezione [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) del documento SPA Blueprint.

## ModelRouter {#modelrouter}

La `ModelRouter` - se attivata - racchiude le funzioni API HTML5 History `pushState` e `replaceState` per garantire che un dato frammento di modello sia preacquisito e accessibile. Quindi, notifica al componente front-end registrato che il modello è stato modificato.

## Routing manuale e automatico modelli {#manual-vs-automatic-model-routing}

`ModelRouter` automatizza il recupero dei frammenti del modello. Ma come ogni attrezzo automatizzato è dotato di limitazioni. Se necessario, è possibile disabilitare o configurare la `ModelRouter` per ignorare i percorsi utilizzando le proprietà meta (vedere la sezione Meta Properties del documento [SPA Page Component](/help/sites-developing/spa-page-component.md)). Gli sviluppatori front-end possono quindi implementare un proprio livello di routing del modello richiedendo a `PageModelManager` di caricare qualsiasi frammento del modello utilizzando la funzione `getData()`.

>[!NOTE]
>
>Attualmente il progetto React di esempio We.Retail Journal illustra l&#39;approccio automatico, mentre il progetto Angular illustra quello manuale. Un approccio semi-automatizzato sarebbe anche un caso d’uso valido.

>[!CAUTION]
>
>La versione corrente di `ModelRouter` supporta solo l&#39;uso di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’uso di URL personalizzati o alias.

## Contratto di routing {#routing-contract}

L&#39;implementazione corrente si basa sul presupposto che il progetto SPA utilizzi l&#39;API HTML5 History per il routing alle diverse pagine dell&#39;applicazione.

### Configurazione {#configuration}

Il `ModelRouter` supporta il concetto di routing del modello in quanto ascolta le chiamate `pushState` e `replaceState` ai frammenti del modello di preacquisizione. Internamente, attiva la `PageModelManager` per caricare il modello che corrisponde a un determinato URL e attiva un evento `cq-pagemodel-route-changed` che altri moduli possono ascoltare.

Per impostazione predefinita, questo comportamento è attivato automaticamente. Per disattivarlo, il SPA deve eseguire il rendering della seguente proprietà meta:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Tenere presente che ogni route del SPA deve corrispondere a una risorsa accessibile in AEM (ad esempio, &quot; `/content/mysite/mypage"`), poiché `PageModelManager` cercherà automaticamente di caricare il modello di pagina corrispondente dopo che la route è stata selezionata. Anche se, se necessario, il SPA può anche definire un &quot;elenco Bloccati &quot; di route che devono essere ignorate dalla `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
