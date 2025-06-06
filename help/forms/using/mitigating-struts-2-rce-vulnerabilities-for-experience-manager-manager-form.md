---
title: Mitigazione delle vulnerabilità di Struts 2 per Experience Manager Forms su JEE
description: Mitigazione delle vulnerabilità di Struts 2 per Experience Manager Forms su JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 73b5aff2-1320-4d9a-8972-54c4fdd3a2c2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Mitigazione delle vulnerabilità Struts 2 per Experience Manager Forms {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## Problema  

Sono state segnalate vulnerabilità di sicurezza critiche per Struts 2, un framework di applicazioni web popolare e open-source per lo sviluppo di applicazioni web Java EE. Sono state analizzate le seguenti vulnerabilità:

| Vulnerabilità | Che cosa è interessato? | Cosa non è interessato? |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | Experience Manager 6.5 Forms su JEE (tutte le versioni da 6.5 GA a 6.5.19.0) | <ul><li> Experience Manager Forms Workbench (tutte le versioni)</li> <li> Experience Manager Forms su OSGi (tutte le versioni) </li> <li> Experience Manager Forms as a Cloud Service </li> <ul> |

## Risoluzione

La tabella seguente elenca la risoluzione per tutte le versioni interessate:

| Versione | Versione corrente | Azione utente |
|---|---|---|
| Experience Manager 6.5 Forms su JEE | 6.5.19.0 | [Installa il service pack più recente](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=it) |
| Experience Manager 6.5 Forms su JEE | 6.5.13.0 - 6.5.18.0 | Utilizza uno dei seguenti metodi: <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=it"> Installare il service pack più recente </a> </li> <li> <a href ="#use-manual-mitigation-steps"> Utilizzare i passaggi di mitigazione manuali </a> |
| Experience Manager 6.5 Forms su JEE | 6,5 - 6.5.12,0 | [Installa il service pack più recente](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=it) </br> </br> **NOTA:** AEM Forms supporta attualmente le versioni da 6.5.13.0 a 6.5.19.0. Se utilizzi una versione precedente, ti consigliamo di effettuare l’aggiornamento a 6.5.13.0 o a una versione successiva. Per istruzioni su come installare AEM 6.5.13.0 o versione successiva, consulta le note sulla versione. |

### Utilizzare i passaggi di mitigazione manuali {#use-manual-mitigation-steps}

È possibile utilizzare i passaggi di mitigazione manuali per risolvere il problema sul server di moduli AEM 6.5 con Service Pack 13 al server di moduli AEM 6.5 con Service Pack 18 (6.5.13.0 - 6.5.18.0):

1. Scarica [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar) in una cartella locale. Ad esempio, C:\Users\labuser\Desktop\struts2-core-2.5.33.jar.
1. Scarica lo strumento di patch manuale AEM Forms su JEE da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. Decomprimi l’archivio dello strumento di applicazione di patch manuale. Ad esempio, estrarre in `/Users/labuser/Desktop/archive-patcher-1.0.0 folder`. Vengono estratti i seguenti file:
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh

>[!BEGINTABS]

>[!TAB Windows]

1. Arresta tutte le istanze e i localizzatori del server.

1. Apri la finestra del terminale e passa alla cartella contenente lo strumento AEM Forms on JEE Manual Patching Tool (file estratti).

1. Esegui il comando seguente per cercare tutti i file con librerie Struts2 precedenti. Prima di eseguire il comando, sostituisci il percorso nel comando con il percorso del server AEM Forms:


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >Lo strumento richiede la connettività Internet in quanto scarica le dipendenze in fase di esecuzione. Quindi, prima di eseguire lo strumento, assicurarsi di essere connessi a Internet.

1. Eseguire i seguenti comandi nell&#39;ordine elencato per la sostituzione diretta ricorsiva. Prima di eseguire il comando, sostituire il percorso nel comando con il percorso del server AEM Forms e del file `struts2-core-2.5.33.jar`.



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$ -action=replace C:\Users\labuser\Desktop\struts2-core-2.5.33.jar
   ```

   I passaggi precedenti applicano la patch a tutti i file dell’orecchio con librerie struts2 precedenti.

1. Annullare la distribuzione dell&#39;EAR precedente e distribuire nel server applicazioni il file EAR con patch, disponibile nella cartella di esportazione.

1. Avvia il server AEM Forms.

>[!TAB Linux]

1. Arresta tutte le istanze e i localizzatori del server.

1. Apri la finestra del terminale e passa alla cartella contenente lo strumento AEM Forms on JEE Manual Patching Tool (file estratti).

1. Esegui il comando seguente per cercare tutti i file con librerie Struts2 precedenti. Prima di eseguire il comando, sostituisci il percorso nel comando con il percorso del server AEM Forms:


   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >Lo strumento richiede la connettività Internet in quanto scarica le dipendenze in fase di esecuzione. Quindi, prima di eseguire lo strumento, assicurarsi di essere connessi a Internet.

1. Eseguire i seguenti comandi nell&#39;ordine elencato per la sostituzione diretta ricorsiva. Prima di eseguire il comando, sostituire il percorso nel comando con il percorso del server AEM Forms e del file `struts2-core-2.5.33.jar`.



   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$ -action=replace /opt/struts2-core-2.5.33.jar
   ```

   I passaggi precedenti applicano la patch a tutti i file dell’orecchio con librerie struts2 precedenti.

1. Annullare la distribuzione dell&#39;EAR precedente e distribuire nel server applicazioni il file EAR con patch, disponibile nella cartella di esportazione.

1. Avvia il server AEM Forms.

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->
