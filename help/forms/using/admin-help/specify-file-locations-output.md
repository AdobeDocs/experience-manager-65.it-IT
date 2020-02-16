---
title: Specificare i percorsi dei file per Output
seo-title: Specificare i percorsi dei file per Output
description: Scoprite come specificare i percorsi dei file per Output.
seo-description: Scoprite come specificare i percorsi dei file per Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Specificare i percorsi dei file per Output {#specify-file-locations-for-output}

È possibile specificare le posizioni in cui Output cerca determinati tipi di file richiesti.

1. Nella console di amministrazione, fate clic su Servizi > output.
1. In Posizioni specificare le opzioni appropriate.
1. Fate clic su Salva.

## Impostazioni posizioni {#locations-settings}

**** URI radice contenuto: URI o posizione assoluta della directory archivio da cui vengono recuperati i moduli. Questo valore è combinato con il parametro sForm, specificato tramite l&#39;API, per costruire il percorso assoluto del modulo recuperato. Questo valore può fare riferimento a una directory o a una posizione Web accessibile tramite HTTP.

Il valore predefinito è una stringa vuota.

**** File di configurazione XCI: Posizione relativa o assoluta del file di configurazione XCI utilizzato dal servizio Output per il rendering. Per un valore relativo, si presume che il file XCI risieda nei moduli AEM distribuibili EAR.

Il valore predefinito è `com/adobe/formServer/PA/pa_output.xci`.

**** Posizione cache: Specifica il percorso della cache del disco di output. Quando modificate questa impostazione, tutte le informazioni cache esistenti provenienti dalla posizione corrente vengono reimpostate e viene creata una nuova cache nella nuova posizione. Selezionare una delle seguenti opzioni:

**** Posizione predefinita: Questa è la selezione predefinita. Quando questa opzione è selezionata, la cache viene creata in una posizione che dipende dal server applicazione in uso:

* **** JBoss: `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **** WebLogic: `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **** WebSphere: `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**** Directory temporanea LC: La cache viene creata in una sottodirectory della directory temporanea dei moduli AEM, specificata nella console di amministrazione in Impostazioni > Impostazioni sistema di base > Configurazioni > Posizione della directory temporanea. La sottodirectory è denominata `adobeoutput_[servername]`.

>[!NOTE]
>
>Se si utilizza un&#39;utilità di pulizia temporanea, tenere presente che mentre si eliminano queste directory non influisce sulla funzionalità, può avere un impatto significativo sulle prestazioni per un breve periodo di tempo, fino alla creazione della nuova cache. Per evitare questo problema, non eliminate queste directory durante la cancellazione della directory temporanea dei moduli AEM.

