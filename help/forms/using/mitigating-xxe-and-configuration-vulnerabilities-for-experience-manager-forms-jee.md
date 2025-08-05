---
title: Mitigazione di XXE, configurazione avanzata della modalità di sviluppo e vulnerabilità di esecuzione del codice remoto per AEM Forms su JEE
description: Mitigazione delle vulnerabilità XXE, di configurazione e di esecuzione remota del codice per AEM Forms su JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: 9be9bfc9e20a151afdb9ae2cddcc39b4d2701c1b
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 5%

---

# Mitigazione di RCE (CVE-2025-49533), configurazione Struts Dev Mode (CVE-2025-54253), XXE (CVE-2025-54254) e vulnerabilità per AEM Forms su JEE {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## Riferimento rapido

| **Livello di impatto** | **Versioni interessate** | **Azione consigliata** |
|---|---|---|
| **Critico** | AEM 6.5 Forms su JEE Service Pack 23 (6.5.23.0) | [Installa aggiornamento rapido più recente](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **Critico** | AEM 6.5 Forms su JEE Service Pack 18-22 (6.5.18.0 - 6.5.22.0) | [Installare manualmente le correzioni](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **Critico** | AEM 6.5 Forms su JEE Service Pack 17 (6.5.17.0) o versioni precedenti | Esegui l’aggiornamento a una versione del Service Pack supportata, quindi applica i passaggi di mitigazione consigliati per la nuova versione |
| **Non interessato** | AEM Forms su OSGi, Workbench, Cloud Service | Nessuna azione richiesta |

**Vulnerabilità risolte:**

- Esecuzione di codice remoto (CVE-2025-49533)
- Problemi di sicurezza della configurazione (CVE-2025-54253)
- Elaborazione XXE (XML External Entity) (CVE-2025-54254)

## Panoramica

### Che cosa è interessato

| Vulnerabilità | Impatto | Componenti interessati |
|---|---|---|
| **CVE-2025-49533**: Esecuzione codice remoto | Esecuzione di codice non autenticato in GetDocumentServlet | AEM 6.5 Forms su JEE Service Pack 23 (6.5.23.0) e versioni precedenti |
| **CVE-2025-54253**: problemi di configurazione | Avvia la modalità di sviluppo abilitata nell’interfaccia di amministrazione | AEM 6.5 Forms su JEE Service Pack 23 (6.5.23.0) e versioni precedenti |
| **CVE-2025-54254**: Elaborazione XXE | Il modulo Document Security consente l’accesso non autorizzato ai file | AEM 6.5 Forms su JEE Service Pack 23 (6.5.23.0) e versioni precedenti |


### Cosa non viene interessato

- Experience Manager Forms Workbench (tutte le versioni)
- Experience Manager Forms su OSGi (tutte le versioni)
- Experience Manager Forms as a Cloud Service

## Opzioni di risoluzione


### Prima di iniziare

Prima di apportare qualsiasi modifica, eseguire una copia di backup del file EAR o del file DSC che si sta per modificare o aggiornare:

- Individuare il file EAR o DSC originale nella directory di distribuzione.
- Copiare il file in un percorso di backup protetto all&#39;esterno della directory di distribuzione.
- Prima di procedere con gli aggiornamenti, verificare che il backup sia completo e accessibile.

Questa precauzione ti consente di ripristinare lo stato originale nel caso in cui si verifichino problemi durante il processo di aggiornamento.

### Opzione 1: (per gli utenti nella versione 6.5.23.0) installare l&#39;aggiornamento rapido più recente

1. [Scarica l&#39;aggiornamento rapido per 6.5.23.0](/help/release-notes/aem-forms-hotfix.md).
1. Segui le [istruzioni di installazione hotfix/patch standard](/help/release-notes/jee-patch-installer-65.md)
1. Se utilizzi Document Security (precedentemente Rights Management) su IBM WebSphere o Oracle WebLogic, imposta la seguente proprietà di sistema Java (argomento JVM) prima di avviare il server AEM Forms:

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. Riavvia il server applicazioni

### Opzione 2: (per gli utenti su 6.5.18.0 - 6.5.22.0) Installazione manuale degli hotfix

+++Installazione manuale degli hotfix per 6.5.18.0 tramite 6.5.22.0

**Passaggio 1: scarica ed estrai il pacchetto Hotfix**

- Scarica [hotfix per 6.5.18.0 - 6.5.22.](/help/release-notes/aem-forms-hotfix.md) dal portale di distribuzione software di Adobe
- Estrai localmente

**Passaggio 2: passare alla cartella della versione corretta**

- In base alla versione del Service Pack installata nel tuo ambiente, vai alla cartella corrispondente.

  Esempio per Service Pack 20 la cartella è:

  ```
  <extracted-hotfix>/SP20/
  ```

**Passaggio 3: individuare la directory di distribuzione**

- Nel server AEM Forms su JEE, vai a:

  ```
  [AEM installation directory]/deploy
  ```

  Esempio: `adobe/adobe-experience-manager-forms/deploy`



**Passaggio 4: aggiornare e sostituire i file EAR**

>[!BEGINTABS]

>[!TAB JBoss]

1. Apri `adobe-core-jboss.ear` e sostituisci `adminui.war` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

1. All&#39;interno di `adobe-core-jboss.ear`, passare alla cartella `lib/` e sostituire `adobe-uisupport.jar` con:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salvare l&#39;EAR. Assicurati che le modifiche siano salvate correttamente.


1. Sostituisci `adobe-edcserver-jboss.ear` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

1. Sostituisci `adobe-forms-jboss.ear` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. Apri `adobe-core-weblogic.ear` e sostituisci `adminui.war` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

1. All&#39;interno di `adobe-core-weblogic.ear`, sostituisci `adobe-uisupport.jar` con:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salvare l&#39;EAR. Assicurati che le modifiche siano salvate correttamente.


1. Sostituisci `adobe-edcserver-weblogic.ear` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

1. Sostituisci `adobe-forms-weblogic.ear` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. Apri `adobe-core-websphere.ear` e sostituisci `adminui.war` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

1. All&#39;interno di `adobe-core-websphere.ear`, sostituisci `adobe-uisupport.jar` con:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salvare l&#39;EAR. Assicurati che le modifiche siano salvate correttamente.


1. Sostituisci `adobe-edcserver-websphere.ear` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

1. Sostituisci `adobe-forms-websphere.ear` con

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   Ad esempio `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**Passaggio 5: aggiorna `adobe-rightsmanagement-<appserver>-dsc.jar`file con**

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

Ad esempio `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**Passaggio 6: configurazione aggiuntiva per Document Security su WebSphere e WebLogic**:

Se utilizzi Document Security (precedentemente Rights Management), imposta la seguente proprietà di sistema Java (argomento JVM) prima di avviare il server AEM Forms:

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**Passaggio 7: rieseguire Configuration Manager**

- Avvia Configuration Manager per ridistribuire l’EAR aggiornato e applicare l’hotfix

+++

### Opzione 3: percorso di aggiornamento per gli utenti di 6.5.17.0 e versioni precedenti

1. [Passare a una versione del Service Pack supportata](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. Segui le opzioni 1 o 2 di cui sopra in base alla nuova versione

## Riferimenti

- [CWE-611: restrizione non corretta del riferimento all&#39;entità esterna XML](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16: configurazione](https://cwe.mitre.org/data/definitions/16.html)
- [Scheda di riferimento sulla prevenzione di OWASP XXE](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Best practice per la sicurezza di Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=it)
