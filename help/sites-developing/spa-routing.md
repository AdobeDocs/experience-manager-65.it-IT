---
title: Routing modello SPA
description: Per le applicazioni a pagina singola in AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di instradamento, il contratto e le opzioni disponibili.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Routing modello SPA{#spa-model-routing}

Per le applicazioni a pagina singola in AEM, l’app è responsabile del routing. Questo documento descrive il meccanismo di instradamento, il contratto e le opzioni disponibili.

{{ue-over-spa}}

## Indirizzamento progetto {#project-routing}

L’app è proprietaria del routing e viene quindi implementata dagli sviluppatori front-end del progetto. Questo documento descrive il routing specifico per il modello restituito dal server AEM. La struttura dati del modello di pagina espone l’URL della risorsa sottostante. Il progetto front-end può utilizzare qualsiasi libreria personalizzata o di terze parti che fornisce funzionalità di indirizzamento. Quando una route prevede un frammento di modello, è possibile effettuare una chiamata alla funzione `PageModelManager.getData()`. Quando viene modificata una route di modello, deve essere attivato un evento per avvisare le librerie in ascolto, come l’Editor pagina.

## Architettura {#architecture}

Per una descrizione dettagliata, vedi la sezione [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) del documento Blueprint SPA.

## ModelRouter {#modelrouter}

`ModelRouter` - se abilitato - incapsula le funzioni API della cronologia di HTML5 `pushState` e `replaceState` per garantire che un determinato frammento di modello sia preacquisito e accessibile. Notifica quindi al componente front-end registrato che il modello è stato modificato.

## Routing modello manuale e automatico {#manual-vs-automatic-model-routing}

`ModelRouter` automatizza il recupero dei frammenti del modello. Ma come qualsiasi strumento automatizzato è dotato di limitazioni. Se necessario, è possibile disabilitare o configurare `ModelRouter` per ignorare i percorsi che utilizzano le metaproprietà (vedere la sezione Meta Properties del documento [Componente pagina SPA](/help/sites-developing/spa-page-component.md)). Gli sviluppatori front-end possono quindi implementare il proprio livello di routing del modello richiedendo a `PageModelManager` di caricare un determinato frammento di modello utilizzando la funzione `getData()`.

>[!NOTE]
>
>Il progetto di esempio [We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) React illustra l&#39;approccio automatizzato, mentre il progetto Angular illustra quello manuale. Anche un approccio semi-automatizzato sarebbe un caso d’uso valido.

>[!CAUTION]
>
>La versione corrente di `ModelRouter` supporta solo l&#39;utilizzo di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’utilizzo di URL personalizzati o alias.

## Contratto ciclo {#routing-contract}

L’implementazione corrente si basa sul presupposto che il progetto SPA utilizzi l’API della cronologia di HTML5 per il routing alle diverse pagine dell’applicazione.

### Configurazione {#configuration}

`ModelRouter` supporta il concetto di routing del modello in quanto ascolta le chiamate `pushState` e `replaceState` per la preacquisizione dei frammenti del modello. Internamente, attiva `PageModelManager` per caricare il modello corrispondente a un determinato URL e genera un evento `cq-pagemodel-route-changed` a cui altri moduli possono fare da listener.

Per impostazione predefinita, questo comportamento viene attivato automaticamente. Per disattivarla, l’applicazione a pagina singola deve eseguire il rendering della seguente proprietà meta:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Si noti che ogni route dell&#39;applicazione a pagina singola deve corrispondere a una risorsa accessibile in AEM (ad esempio, &quot; `/content/mysite/mypage"`) poiché `PageModelManager` tenterà automaticamente di caricare il modello di pagina corrispondente una volta selezionata la route. Tuttavia, se necessario, l&#39;applicazione a pagina singola può anche definire un &quot;elenco Bloccati&quot; di route che devono essere ignorate da `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
