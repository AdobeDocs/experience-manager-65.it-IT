---
title: Specificare le posizioni dei file per l'output
seo-title: Specify file locations for Output
description: Scopri come specificare le posizioni dei file per Output.
seo-description: Learn how to specify file locations for Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# Specificare le posizioni dei file per l&#39;output {#specify-file-locations-for-output}

È possibile specificare le posizioni in cui Output cerca determinati tipi di file necessari.

1. Nella console di amministrazione, fai clic su Servizi > output.
1. In Posizioni specificare le opzioni appropriate.
1. Fai clic su Salva.

## Impostazioni delle posizioni {#locations-settings}

**URI radice contenuto:** URI o posizione assoluta dell’archivio da cui vengono recuperati i moduli. Questo valore viene combinato con il parametro sForm, specificato tramite l&#39;API, per creare il percorso assoluto del modulo recuperato. Questo valore può fare riferimento a una directory o a una posizione Web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**File di configurazione XCI:** Posizione relativa o assoluta del file di configurazione XCI utilizzato dal servizio Output per il rendering. Per un valore relativo, si presume che il file XCI risieda nel file EAR dei moduli AEM distribuibili.

Il valore predefinito è `com/adobe/formServer/PA/pa_output.xci`.

**Posizione cache:** Specifica il percorso della cache del disco di output. Quando modifichi questa impostazione, tutte le informazioni esistenti sulla cache dalla posizione corrente vengono reimpostate e viene creata una nuova cache nella nuova posizione. Selezionare una delle seguenti opzioni:

**Posizione predefinita:** Questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione che dipende dal server dell&#39;applicazione in uso:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Directory temporanea LC:** La cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella console di amministrazione in Impostazioni > Impostazioni sistema di base > Configurazioni > Posizione della directory temporanea. La sottodirectory viene denominata `adobeoutput_[servername]`.

>[!NOTE]
>
>Se si utilizza un&#39;utilità di pulizia temporanea, tenere presente che mentre l&#39;eliminazione di queste directory non influisce sulla funzionalità, può avere un impatto significativo sulle prestazioni per un breve periodo di tempo, fino alla creazione della nuova cache. Per evitare questo problema, non eliminare queste directory quando si cancella la directory temporanea dei moduli AEM.
