---
title: AEM Commerce - Preparazione all’RGPD
description: Scopri le procedure per gestire le richieste RGPD in AEM Commerce e come utilizzarle.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Commerce - Preparazione all’RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli coperti sono applicabili a tutte le normative su privacy e protezione dei dati, come il RGPD e il CCPA.

Il Regolamento generale sulla protezione dei dati dell&#39;Unione Europea sui diritti relativi alla privacy dei dati entra in vigore a maggio 2018. Visita la pagina [RGPD all&#39;Adobe Privacy Center](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulta [Preparazione all&#39;AEM per il RGPD](/help/managing/data-protection-and-privacy.md) per ulteriori dettagli.

![schermata_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Con le integrazioni Commerce pronte all’uso di Adobe, l’AEM è il livello di esperienza, che utilizza servizi e invia dati alla piattaforma di e-commerce del cliente che viene eseguita in modalità headless.

Per alcune piattaforme commerce, Adobe memorizza le informazioni del profilo ( `/home/users`) e i token commerce (per accedere alla piattaforma commerce) nell&#39;AEM. Per questi casi d&#39;uso, leggi [Gestione delle richieste RGPD per la piattaforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![schermata_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestione delle richieste RGPD per AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Per l’integrazione con Salesforce Commerce Cloud, AEM Commerce non memorizza alcuna informazione rilevante ai fini del RGPD. Inoltra la richiesta a [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Per le integrazioni Hybris e HCL WebSphere® Commerce, sono disponibili alcuni dati nell&#39;AEM. Utilizza le [istruzioni RGPD per la piattaforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considera queste domande:

1. **Dove vengono memorizzati/utilizzati i dati?** Informazioni del profilo utente memorizzate nella cache come nome, identificatore utente commerce, token, password e dati dell&#39;indirizzo, come mostrato dall&#39;AEM.
1. **Con chi condivido i dati coperti dal RGPD?** Qualsiasi aggiornamento dei dati relativi al RGPD nel Commerce dell&#39;AEM non viene memorizzato (eccetto le informazioni del profilo rilevanti, come indicato sopra) ma viene inviato nuovamente alla piattaforma Commerce.
1. **Eliminare i dati utente**? Elimina il profilo utente in AEM e richiama l’eliminazione dell’utente sulla piattaforma commerce.

>[!NOTE]
>
>Dai un&#39;occhiata al [wiki hybris](https://wiki.hybris.com/) o alla [documentazione di Commerce WebSphere® HCL](https://help.hcltechsw.com/commerce/index.html), se necessario.
