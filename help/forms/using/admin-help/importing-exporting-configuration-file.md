---
title: Importare ed esportare il file di configurazione
description: Scopri come importare ed esportare il file di configurazione per modificare le preferenze del server o per configurare un’altra istanza prodotto di AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 100%
---
# Importare ed esportare il file di configurazione {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizza la pagina Configurazione manuale per scaricare una copia delle impostazioni di configurazione in formato XML. Le impostazioni di questo file controllano tutte le preferenze del server. Puoi quindi modificare il file e caricarlo nuovamente sul server. Inoltre puoi utilizzare il file per configurare un’altra istanza del prodotto AEM Forms.

Per evitare rischi per la sicurezza, il valore della password di associazione per il server delle directory non viene incluso in un file di configurazione esportato. Aggiorna la password nel file XML prima di importare il file in un nuovo sistema.

>[!NOTE]
>
>L’importazione del file di configurazione riconfigura AEM Forms in base alle informazioni presenti nel file. Solo un amministratore di sistema o un consulente di Servizi Professionali che ha familiarità con il prodotto AEM Forms e con il linguaggio XML può valutare la possibilità di modificare il file di configurazione. Tale utente potrebbe dover modificare il file di configurazione, ad esempio, per riconfigurare un’impostazione danneggiata.

**Esportare le informazioni di configurazione**

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Esporta. Se utilizzi Microsoft Internet Explorer ti verrà richiesto di specificare il percorso in cui salvare il file. Se utilizzi Firefox, il file viene salvato sul desktop.

**Importare le informazioni di configurazione**

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Sfoglia per trovare il file di configurazione, fai clic su Importa e quindi su OK.
