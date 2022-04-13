---
title: Risoluzione dei problemi e domande frequenti relativi a MSM
description: Scopri come risolvere i problemi più comuni relativi a MSM e ottieni le risposte alle domande più comuni relative a MSM.
feature: Multi Site Manager
role: Admin
source-git-commit: d4fa331ad048e1d8bd57e0944c8bc5b67be1d203
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Risoluzione dei problemi e domande frequenti relativi a MSM {#troubleshooting-msm}

## Risoluzione dei problemi - Primi passi {#first-steps}

Se stai riscontrando un comportamento errato o un errore in MSM, prima di iniziare e risolvere in modo dettagliato i problemi assicurati:

* Controlla la [Domande frequenti su MSM](#faq) poiché i vostri problemi o domande possono già essere affrontati lì.
* Controlla la [Articolo sulle best practice MSM](msm-best-practices.md) come una serie di suggerimenti sono offerti là insieme a chiarimenti di una serie di malintesi.

## Ricerca di informazioni avanzate sullo stato della blueprint e della Live Copy {#advanced-info}

MSM registra diversi servlet che possono essere richiesti con i selettori sugli URL delle risorse. Questi vengono utilizzati dall’interfaccia utente, ma possono anche essere richiesti direttamente per visualizzare stati MSM avanzati e direttamente aggiuntivi per le tue pagine:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Utilizza questo su una pagina blueprint per recuperare l’elenco di tutte le Live Copy ad essa collegate, con informazioni sullo stato di Live Copy aggiuntive.
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Utilizza questo nelle pagine Live Copy per recuperare informazioni avanzate sulla loro connessione con le loro pagine blueprint. Se la pagina non è una Live Copy, non viene restituito nulla.

Questi servlet generano messaggi di log DEBUG attraverso `com.day.cq.wcm.msm` logger che può anche essere utile.

## Verifica delle informazioni specifiche di MSM nell&#39;archivio {#checking-repo}

I servlet precedenti restituivano informazioni calcolate in base ai nodi e ai mixin specifici di MSM. Le informazioni vengono memorizzate nell’archivio nel modo seguente.

* `cq:LiveSync` tipo mixin
   * È impostato su `jcr:content` e definire le pagine Live Copy principali.
   * Le pagine avranno un `cq:LiveSyncConfig` nodo figlio di tipo `cq:LiveCopy` che conterrà informazioni di base e obbligatorie sulla Live Copy attraverso le seguenti proprietà:
      * `cq:master` punta alla pagina blueprint della Live Copy.
      * `cq:rolloutConfigs` indica le configurazioni di rollout attive applicate alla Live Copy.
      * `cq:isDeep` è true se le pagine figlie di questa pagina Live Copy principale sono incluse nella Live Copy.
* `cq:LiveRelationship` tipo mixin
   * Qualsiasi pagina Live Copy ha un tale tipo mixin sul suo `jcr:content` nodo.
   * In caso contrario, la pagina a un certo punto è stata staccata o creata manualmente tramite l’interfaccia di authoring al di fuori di un’azione Live Copy (creazione o rollout).
* `cq:LiveSyncCancelled` tipo mixin
   * Aggiunto a `jcr:content` nodi di pagine Live Copy sospese.
   * Se la sospensione è efficace anche per le pagine figlie, un `cq:isCancelledForChildren` su true sullo stesso nodo.

Le informazioni presenti in queste proprietà dovrebbero riflettersi nell’interfaccia utente, tuttavia quando si risolve il problema può essere utile osservare il comportamento di MSM direttamente nell’archivio mentre si verificano le azioni MSM.

Conoscere queste proprietà può essere utile anche per eseguire query sull’archivio e trovare set di pagine che si trovano in determinati stati. Ad esempio:

* `select * from cq:LiveSync` restituisce tutte le pagine principali di Live Copy.

## Domande frequenti {#faq}

Ecco alcune domande frequenti relative a MSM e Live Copy.

### Perché alcune proprietà (ad esempio titolo, annotazioni) non vengono aggiornate durante un rollout di MSM? {#missing-properties}

Le azioni di sincronizzazione MSM sono altamente configurabili. Le proprietà o i componenti modificati durante il rollout dipendono direttamente dalle proprietà di tali configurazioni.

Vedi [articolo](msm-best-practices.md) per ulteriori informazioni su questo argomento.

### Come posso rimuovere le autorizzazioni di rollout per un gruppo di autori? {#remove-rollout-permissions}

Non esiste **rollout** privilegio che può essere impostato o rimosso per AEM entità (utenti o gruppi).

In alternativa, puoi effettuare le seguenti operazioni:

* Personalizzazione dell’interfaccia utente del prodotto per nascondere le azioni di Rollout per una determinata entità principale.
* Rimuovi i privilegi di scrittura dalla struttura Live Copy per gli autori che non possono eseguire il rollout.

### Perché vedo le pagine Live Copy con il suffisso &quot;_msm_move&quot;? {#moved-pages}

Se viene implementata una pagina blueprint, la pagina Live Copy verrà aggiornata o creata una nuova pagina Live Copy, se non esiste ancora (ad esempio, quando viene lanciata per la prima volta o la pagina Live Copy è stata eliminata manualmente).

In quest&#39;ultimo caso, tuttavia, se una pagina senza un `cq:LiveRelationship` La proprietà esiste con lo stesso nome, la pagina verrà rinominata di conseguenza prima che venga creata la pagina Live Copy.

Per impostazione predefinita, il rollout prevede una pagina Live Copy collegata, alla quale verranno implementati gli aggiornamenti dei progetti, o nessuna pagina al momento della creazione di una pagina Live Copy.

Se viene trovata una pagina &quot;standalone&quot;, MSM sceglie di rinominare questa pagina e di creare una pagina Live Copy separata collegata.

Una pagina autonoma come questa in un sottoalbero Live Copy è in genere il risultato di un **Stacca** oppure la pagina Live Copy precedente è stata eliminata manualmente da un autore e quindi ricreata con lo stesso nome.

Per evitare questo, utilizza la Live Copy **Sospendi** anziché **Stacca**. Maggiori dettagli sul **Stacca** in azione [questo articolo.](msm-livecopy.md)
