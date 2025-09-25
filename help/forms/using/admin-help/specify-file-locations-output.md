---
title: Specificare i percorsi dei file per l’output
description: Scopri come specificare i percorsi dei file nell’output per determinati tipi di file, ad esempio file URI principale del contenuto, file di configurazione XCI, file di cache e file predefiniti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '339'
ht-degree: 100%

---

# Specificare i percorsi dei file per l’output {#specify-file-locations-for-output}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi specificare i percorsi in cui l’output cerca determinati tipi di file necessari.

1. Nella Console di amministrazione, fai clic su Servizi > Output.
1. In Posizioni specifica le opzioni appropriate.
1. Fai clic su Salva.

## Impostazioni di Posizioni {#locations-settings}

**URI principale contenuto:** URI o posizione assoluta dell’archivio da cui vengono recuperati i moduli. Questo valore è combinato con il parametro sForm, specificato tramite l’API, per creare il percorso assoluto del modulo che viene recuperato. Il valore può fare riferimento a una directory o a un percorso web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**File di configurazione XCI:** posizione relativa o assoluta del file di configurazione XCI utilizzato dal servizio di output per il rendering. Per un valore relativo, si presume che il file XCI si trovi nel file EAR distribuibile di AEM forms.

Il valore predefinito è `com/adobe/formServer/PA/pa_output.xci`.

**Percorso della cache:** specifica la posizione della cache su disco per l’output. Quando modifichi questa impostazione, tutti i dati della cache esistenti per la posizione corrente vengono reimpostati e viene creata una nuova cache nella nuova posizione. Seleziona una delle opzioni seguenti:

**Percorso predefinito:** questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione che dipende dal server applicazioni in uso:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Directory temporanea LC:** la cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella Console di amministrazione in Impostazioni > Impostazioni sistema core > Configurazioni > Percorso directory temporanea. Il nome della sottodirectory è `adobeoutput_[servername]`.

>[!NOTE]
>
>Se esegui un’utilità di pulizia dei file temporanei, l’eliminazione di queste directory non influisce sulla funzionalità, ma può avere un impatto significativo sulle prestazioni per un periodo di tempo limitato, fino alla creazione della nuova cache. Per evitare il problema, non eliminare queste directory quando cancelli la directory temporanea di AEM Forms.
