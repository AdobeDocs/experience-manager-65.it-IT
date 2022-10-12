---
title: Sicurezza
seo-title: Security
description: La sicurezza dell'applicazione viene avviata durante la fase di sviluppo
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Sicurezza{#security}

La sicurezza dell&#39;applicazione viene avviata durante la fase di sviluppo. Adobe consiglia di applicare le seguenti best practice di sicurezza.

## Usa sessione di richiesta {#use-request-session}

In base al principio del privilegio minimo, l&#39;Adobe raccomanda che ogni accesso all&#39;archivio venga effettuato utilizzando la sessione associata alla richiesta dell&#39;utente e al controllo di accesso adeguato.

## Protect contro lo scripting tra siti (XSS) {#protect-against-cross-site-scripting-xss}

Lo scripting tra siti (XSS) consente agli aggressori di inserire codice nelle pagine web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtrare tutti i contenuti forniti dall’utente al momento dell’output. La prevenzione di XSS viene data la massima priorità sia durante lo sviluppo che durante i test.

Il meccanismo di protezione XSS fornito da AEM si basa sul [Libreria Java AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornito da [OWASP (il progetto di sicurezza dell&#39;applicazione Web aperta)](https://www.owasp.org/). La configurazione predefinita di AntiSamy si trova in

`/libs/cq/xssprotection/config.xml`

È importante adattare questa configurazione alle tue esigenze di sicurezza sovrapponendo il file di configurazione. Il funzionario [Documentazione di AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ti fornirà tutte le informazioni necessarie per implementare i tuoi requisiti di sicurezza.

>[!NOTE]
>
>Ti consigliamo vivamente di accedere sempre all’API di protezione XSS utilizzando [XSSAPI fornito da AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Inoltre, un firewall per applicazioni web, come [mod_security per Apache](https://www.modsecurity.org), può fornire un controllo centrale affidabile sulla sicurezza dell’ambiente di distribuzione e proteggere da attacchi di script tra siti non rilevati in precedenza.

## Accesso alle informazioni sul Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Le ACL per le informazioni sul Cloud Service e le impostazioni OSGi necessarie per proteggere l&#39;istanza sono automatizzate come parte del [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Ciò significa che non è necessario apportare manualmente le modifiche di configurazione, ma è comunque consigliabile rivederle prima di iniziare a utilizzare la distribuzione.

Quando [integrare l’istanza AEM con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) utilizzi [Configurazioni Cloud Service](/help/sites-developing/extending-cloud-config.md). Le informazioni su queste configurazioni, insieme a eventuali statistiche raccolte, sono memorizzate nel repository. Se utilizzi questa funzionalità, ti consigliamo di verificare se la protezione predefinita di queste informazioni corrisponde ai tuoi requisiti.

Il modulo webservicesupport scrive statistiche e informazioni di configurazione in:

`/etc/cloudservices`

Con le autorizzazioni predefinite:

* Ambiente di authoring: `read` per `contributors`

* Ambiente di pubblicazione: `read` per `everyone`

## Protect contro attacchi di falsificazione di richieste intersito {#protect-against-cross-site-request-forgery-attacks}

Per ulteriori informazioni sui meccanismi di sicurezza AEM utilizzati per attenuare gli attacchi CSRF, consulta la [Filtro Sling Referrer](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) della lista di controllo della sicurezza e [Documentazione del quadro di protezione CSRF](/help/sites-developing/csrf-protection.md).
