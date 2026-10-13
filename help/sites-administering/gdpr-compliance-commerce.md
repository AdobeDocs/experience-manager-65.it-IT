---
title: AEM Commerce - Compatibilità GDPR
description: Scopri le procedure per gestire le richieste RGPD in AEM Commerce e come utilizzarle.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%
---
# AEM Commerce - Compatibilità GDPR{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli coperti sono applicabili a tutte le normative su privacy e protezione dei dati, come il RGPD e il CCPA.

Il Regolamento generale sulla protezione dei dati dell&#39;Unione Europea sui diritti relativi alla privacy dei dati entra in vigore a maggio 2018. Visita la pagina [RGPD all&#39;Adobe Privacy Center](https://business.adobe.com/it/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Preparazione RGPD di AEM](/help/managing/data-protection-and-privacy.md).

![schermata_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Con le integrazioni Commerce predefinite di Adobe, AEM è il livello di esperienza, che utilizza servizi e invia dati alla piattaforma di customer commerce che viene eseguita in modalità headless.

Per alcune piattaforme commerce, Adobe memorizza le informazioni del profilo ( `/home/users`) e i token commerce (per accedere alla piattaforma commerce) in AEM. Per questi casi d&#39;uso, leggi [Gestione delle richieste RGPD per la piattaforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![schermata_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestione delle richieste RGPD per AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Per l’integrazione con Salesforce Commerce Cloud, AEM Commerce non memorizza alcuna informazione rilevante ai fini del RGPD. Inoltra la richiesta a [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Per le integrazioni Hybris e HCL WebSphere® Commerce, sono disponibili alcuni dati in AEM. Utilizza le [istruzioni RGPD per AEM Platform](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considera queste domande:

1. **Dove sono archiviati/utilizzati i dati?** Informazioni sul profilo utente memorizzate nella cache come nome, identificatore utente commerce, token, password e dati dell’indirizzo, come mostrato da AEM.
1. **Con chi condivido i dati coperti dal RGPD?** Qualsiasi aggiornamento dei dati relativi al RGPD in AEM Commerce non viene memorizzato (eccetto le informazioni del profilo rilevanti, come indicato sopra) ma viene inviato tramite proxy alla piattaforma commerce.
1. **Eliminare i dati utente**? Elimina il profilo utente in AEM e richiama l’eliminazione dell’utente sulla piattaforma commerce.

>[!NOTE]
>
>Dai un&#39;occhiata al [wiki hybris](https://wiki.hybris.com/) o alla [documentazione di Commerce WebSphere® HCL](https://help.hcltechsw.com/commerce/index.html), se necessario.
