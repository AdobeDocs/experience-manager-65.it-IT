---
title: Risoluzione dei problemi e domande frequenti relativi a MSM
description: Scopri come risolvere i problemi più comuni relativi a MSM e ottieni le risposte alle domande più comuni.
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 59%

---

# Risoluzione dei problemi e domande frequenti relativi a MSM {#troubleshooting-msm}

## Risoluzione dei problemi - Primi passi {#first-steps}

Se stai riscontrando un comportamento errato o un errore in MSM, prima di iniziare e risolvere in modo dettagliato i problemi assicurati:

* Controlla le [Domande frequenti su MSM](#faq) poiché alcuni problemi o domande potrebbero già essere stati affrontati lì.
* Controlla la [Articolo sulle best practice MSM](msm-best-practices.md) poiché vi sono diversi suggerimenti e chiarimenti su alcuni malintesi.

## Ricerca di informazioni avanzate sullo stato della blueprint e della Live Copy {#advanced-info}

MSM registra diversi servlet che possono essere richiesti con i selettori sugli URL delle risorse. Questi vengono utilizzati dall’interfaccia utente, ma possono anche essere richiesti direttamente per visualizzare stati MSM avanzati e direttamente aggiuntivi per le tue pagine:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Utilizza questo su una pagina blueprint per recuperare l’elenco di tutte le Live Copy ad essa collegate, con informazioni sullo stato di Live Copy aggiuntive.
   * ad esempio:
     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Utilizza questo nelle pagine Live Copy per recuperare informazioni avanzate sulla loro connessione con le loro pagine blueprint. Se la pagina non è una Live Copy, non viene restituito nulla.
   * ad esempio:
     `http://localhost:4502/content/wknd/ca/en.msm.json`

Questi servlet generano messaggi del registro DEBUG attraverso il logger `com.day.cq.wcm.msm` che può anche essere utile.

## Verifica delle informazioni specifiche di MSM nell’archivio {#checking-repo}

I servlet precedenti restituivano informazioni calcolate in base ai nodi e ai mixin specifici di MSM. Le informazioni vengono memorizzate nell’archivio nel modo seguente.

* Tipo mixin `cq:LiveSync`
   * È impostato sui nodi `jcr:content` e definisce le pagine Live Copy principali.
   * Tali pagine hanno un `cq:LiveSyncConfig` nodo figlio di tipo `cq:LiveCopy` che contengono informazioni di base e obbligatorie sulla Live Copy tramite le seguenti proprietà:
      * `cq:master` punta alla pagina blueprint della Live Copy.
      * `cq:rolloutConfigs` indica le configurazioni di rollout attive applicate alla Live Copy.
      * `cq:isDeep` è true se le pagine figlie di questa pagina Live Copy principale sono incluse nella Live Copy.
* Tipo mixin `cq:LiveRelationship`
   * Qualsiasi pagina Live Copy ha questo tipo mixin sul suo nodo `jcr:content`.
   * In caso contrario, la pagina a un certo punto è stata scollegata o creata manualmente tramite l’interfaccia di authoring al di fuori di un’azione Live Copy (creazione o rollout).
* Tipo mixin `cq:LiveSyncCancelled`
   * Aggiunto ai nodi `jcr:content` di pagine Live Copy sospese.
   * Se la sospensione è efficace anche per le pagine figlie, una proprietà `cq:isCancelledForChildren` è impostata su true sullo stesso nodo.

Le informazioni presenti in queste proprietà devono essere riportare nell’interfaccia utente, tuttavia durante la risoluzione dei problemi può essere utile osservare il comportamento di MSM direttamente nell’archivio mentre si verificano le azioni MSM.

Conoscere queste proprietà può essere utile anche per eseguire query sull’archivio e individuare set di pagine che si trovano in determinati stati. Esempio:

* `select * from cq:LiveSync` restituisce tutte le pagine principali di Live Copy.

## Domande frequenti {#faq}

Ecco alcune domande frequenti relative a MSM e Live Copy.

### Perché alcune proprietà (ad esempio titolo, annotazioni) non vengono aggiornate durante un rollout di MSM? {#missing-properties}

Le azioni di sincronizzazione MSM sono altamente configurabili. Quali proprietà o componenti vengono modificati durante il rollout dipendono direttamente dalle proprietà di tali configurazioni.

Per ulteriori informazioni su questo argomento, consulta [questo articolo](msm-best-practices.md).

### Come posso rimuovere le autorizzazioni di rollout per un gruppo di autori? {#remove-rollout-permissions}

Non esiste alcun privilegio di **rollout** che può essere impostato o rimosso per le entità principali di AEM (utenti o gruppi).

In alternativa, puoi effettuare le seguenti operazioni:

* Personalizzare l’interfaccia utente del prodotto per nascondere le azioni di Rollout per una determinata entità principale.
* Rimuovi i privilegi di scrittura dalla struttura Live Copy per gli autori che non sono autorizzati a eseguire il rollout.

### Perché vedo le pagine Live Copy con il suffisso “_msm_moved“? {#moved-pages}

Se viene eseguito il rollout di una pagina blueprint, la pagina Live Copy viene aggiornata oppure viene creata una nuova pagina Live Copy, se non esiste ancora. Ad esempio, quando viene eseguito il rollout per la prima volta o la pagina Live Copy è stata eliminata manualmente.

In quest’ultimo caso, tuttavia, se una pagina senza un `cq:LiveRelationship` esiste con lo stesso nome; questa pagina viene rinominata prima che venga creata la pagina Live Copy.

Per impostazione predefinita, il rollout prevede una pagina Live Copy collegata, alla quale vengono distribuiti gli aggiornamenti dei blueprint. Oppure, quando viene creata una pagina Live Copy, non prevede assolutamente alcuna pagina.

Se viene trovata una pagina “indipendente“, MSM sceglie di rinominare questa pagina e di creare una pagina Live Copy separata collegata.

Una pagina indipendente di questo tipo in una sottostruttura Live Copy è in genere il risultato di una **Stacca** oppure la pagina Live Copy precedente è stata eliminata manualmente da un autore e quindi ricreata con lo stesso nome.

Per evitare questo, utilizza la Live Copy **Sospendi** funzione invece di **Stacca**. Maggiori dettagli sulla **Stacca** azione disponibile in [questo articolo.](msm-livecopy.md)
