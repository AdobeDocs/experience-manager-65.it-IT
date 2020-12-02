---
title: Configurazione di Annulla per la modifica della pagina
seo-title: Configurazione di Annulla per la modifica della pagina
description: Scoprite come configurare il supporto Annulla per la modifica delle pagine in AEM.
seo-description: Scoprite come configurare il supporto Annulla per la modifica delle pagine in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---


# Configurazione dell&#39;annullamento per la modifica delle pagine{#configuring-undo-for-page-editing}

Il [servizio OSGi](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM Undo Configuration** ( `com.day.cq.wcm.undo.UndoConfigService`) espone diverse proprietà che controllano il comportamento dei comandi Annulla e Ripristina per la modifica delle pagine.

## Configurazione predefinita {#default-configuration}

In un&#39;installazione standard, le impostazioni predefinite sono definite come proprietà sul nodo `sling:OsgiConfig`:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Questo nodo contiene le proprietà `cq.wcm.undo.whitelist` e `cq.wcm.undo.blacklist`, per le altre proprietà vengono utilizzate le impostazioni predefinite.

>[!CAUTION]
>
>***non è necessario*** modificare nulla nel percorso `/libs`.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).

## Configurazione di Annulla e Ripristina {#configuring-undo-and-redo}

Potete configurare queste proprietà del servizio OSGi per la vostra istanza.

>[!NOTE]
>
>Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Di seguito sono elencate le proprietà visualizzate nella console Web, seguite dal nome del parametro OSGi corrispondente, insieme a una descrizione e al valore predefinito (se appropriato):

* **Abilita**
( 
`cq.wcm.undo.enabled`)

   * **Descrizione**: Determina se gli autori delle pagine possono annullare e ripristinare le modifiche.
   * **Predefinito**:  `Selected`
   * **Tipo**: `Boolean`

* **Percorso**
( 
`cq.wcm.undo.path`)

   * **Descrizione**: Percorso dell&#39;archivio per i dati di annullamento binari persistenti. Quando gli autori modificano dati binari, ad esempio immagini, la versione originale dei dati viene mantenuta in questa posizione. Quando le modifiche ai dati binari vengono annullate, i dati di annullamento binari vengono ripristinati nella pagina.
   * **Predefinito**:  `/var/undo`
   * **Tipo**: `String`

   >[!NOTE]
   >
   >Per impostazione predefinita, solo gli amministratori possono accedere al nodo `/var/undo`. Gli autori possono eseguire operazioni di annullamento e ripristino su contenuto binario solo dopo che gli sono state assegnate le autorizzazioni per accedere ai dati di annullamento binari.

* **Min. validation**
( 
`cq.wcm.undo.validity`)

   * **Descrizione**: Il tempo minimo di memorizzazione dei dati di annullamento binari, in ore. Dopo questo periodo di tempo, i dati binari sono disponibili per l&#39;eliminazione, per risparmiare spazio su disco.
   * **Predefinito**:  `10`
   * **Tipo**: `Integer`

* **Passaggi**
( 
`cq.wcm.undo.steps`)

   * **Descrizione**: Il numero massimo di azioni di pagina memorizzate nella cronologia di annullamento.
   * **Predefinito**:  `20`
   * **Tipo**: `Integer`

* **Persistenza**
( 
`cq.wcm.undo.persistence`)

   * **Descrizione**: Classe che persiste nella cronologia di annullamento. Sono disponibili due classi di persistenza:

      * `CQ.undo.persistence.WindowNamePersistence`: Persiste la cronologia mediante la proprietà window.name.
      * `CQ.undo.persistence.CookiePersistance`: Persiste la cronologia utilizzando i cookie.
   * **Predefinito**:  `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`


* **Modalità**
 persistenza ( 
`cq.wcm.undo.persistence.mode`)

   * **Descrizione**: Determina quando la cronologia di annullamento viene mantenuta. Selezionare questa opzione per mantenere la cronologia di annullamento dopo ogni modifica di pagina. Deselezionate questa opzione per rimanere attiva solo quando si verifica un ricaricamento di pagina (ad esempio, l’utente passa a un’altra pagina).

      La cronologia degli annullamenti persistenti utilizza le risorse del browser Web. Se il browser degli utenti reagisce lentamente alle modifiche apportate alla pagina, provate a mantenere la cronologia di annullamento sui ricarichi della pagina.

   * **Predefinito**:  `Selected`
   * **Tipo**: `Boolean`

* **Modalità**
 marker( 
`cq.wcm.undo.markermode`)

   * **Descrizione**: Specifica il segnale visivo da utilizzare per indicare quali paragrafi vengono interessati dall&#39;operazione di annullamento o ripristino. I seguenti valori sono validi:

      * flash: L&#39;indicatore di selezione dei paragrafi lampeggia temporaneamente.
      * select: Il paragrafo è selezionato.
   * **Predefinito**:  `flash`
   * **Tipo**: `String`


* **Buoni componenti**
( 
`cq.wcm.undo.whitelist`)

   * **Descrizione**: Elenco dei componenti che devono essere interessati dai comandi Annulla e Ripristina. Aggiungere i percorsi dei componenti a questo elenco quando funzionano correttamente con Annulla/Ripristina. Aggiungi un asterisco (&amp;ast;) per specificare un gruppo di componenti:

      * Il seguente valore specifica il componente di testo di base:

         `foundation/components/text`

      * Il valore seguente specifica tutti i componenti di base:

         `foundation/components/*`
   * Quando si annullano o si ripristinano operazioni su un componente che non figura in questo elenco, viene visualizzato un messaggio che indica che il comando potrebbe non essere affidabile.

   * **Predefinito**: La proprietà viene compilata con molti componenti AEM.
   * **Tipo**: `String[]`


* **Componenti**
 non validi 
`cq.wcm.undo.blacklist`)

   * **Descrizione**: Elenco di componenti e/o operazioni di componenti che non devono essere interessati dal comando Annulla. Aggiungere componenti e operazioni di componenti che non funzionano correttamente con il comando Annulla:

      * Aggiungere un percorso di componente quando non si desidera eseguire nessuna delle operazioni del componente nella cronologia di annullamento, ad esempio `collab/forum/components/post`
      * Aggiungere due punti (:) e un&#39;operazione al percorso quando si desidera che l&#39;operazione specifica venga omessa dalla cronologia degli annullamenti (altre operazioni funzionano correttamente), ad esempio `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >Quando un&#39;operazione è presente in questo elenco, viene comunque aggiunta alla cronologia di annullamento. Gli utenti non possono annullare le operazioni precedenti a un&#39;operazione **Componente non valido** nella cronologia di annullamento.

   * Di seguito sono riportati i nomi tipici delle operazioni:

      * `insertParagraph`: Il componente viene aggiunto alla pagina.
      * `removeParagraph`: Il componente viene eliminato.
      * `moveParagraph`: Il paragrafo viene spostato in una posizione diversa.
      * `updateParagraph`: Le proprietà del paragrafo vengono modificate.
   * **Predefinito**: La proprietà viene compilata con diverse operazioni dei componenti.
   * **Tipo**: `String[]`




