---
title: Specificare i percorsi dei file per l'output
description: Scopri come specificare i percorsi dei file di output per alcuni tipi di file, ad esempio URI radice contenuto, File di configurazione XCI, Cache e Default.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: e2a3470784beb04c2179958ac6cb98861acfaa71
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Specificare i percorsi dei file per l&#39;output {#specify-file-locations-for-output}

È possibile specificare i percorsi in cui Output cerca determinati tipi di file necessari.

1. Nella console di amministrazione, fai clic su Servizi > output.
1. In Posizioni (Locations), specificate le opzioni appropriate.
1. Fai clic su Salva.

## Impostazioni posizioni {#locations-settings}

**URI radice contenuto:** URI o posizione assoluta dell&#39;archivio da cui vengono recuperati i moduli. Questo valore è combinato con il parametro sForm, specificato tramite l’API, per costruire il percorso assoluto del modulo che viene recuperato. Questo valore può fare riferimento a una directory o a un percorso web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**File di configurazione XCI:** Posizione relativa o assoluta del file di configurazione XCI utilizzato dal servizio di output per il rendering. Per un valore relativo, si presume che il file XCI risieda nel file EAR distribuibile dei moduli AEM.

Il valore predefinito è `com/adobe/formServer/PA/pa_output.xci`.

**Percorso cache:** Specifica la posizione della cache del disco di output. Quando si modifica questa impostazione, tutte le informazioni della cache esistenti dalla posizione corrente vengono reimpostate e viene creata una nuova cache nella nuova posizione. Selezionare una delle opzioni seguenti:

**Posizione predefinita:** Questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione dipendente dal server applicazioni in uso:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Directory temporanea LC:** La cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella console di amministrazione in Impostazioni > Impostazioni sistema core > Configurazioni > Posizione della directory temporanea. La sottodirectory è denominata `adobeoutput_[servername]`.

>[!NOTE]
>
>Se si utilizza un&#39;utilità di pulizia temporanea, anche se l&#39;eliminazione di queste directory non influisce sulla funzionalità, può avere un impatto significativo sulle prestazioni per un breve periodo di tempo, fino alla creazione della nuova cache. Per evitare questo problema, non eliminare queste directory mentre si cancella la directory temporanea dei moduli AEM.
