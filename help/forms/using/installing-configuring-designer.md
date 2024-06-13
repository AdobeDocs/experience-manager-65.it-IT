---
title: Installazione e configurazione di Designer
description: Designer è disponibile come programma di installazione autonomo ed è fornito in bundle con Workbench. Scopri come installare Designer autonomo.
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin, User, Developer
feature: Forms Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 09eae6e3550e9e8505c042e23d6569971841d441
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Installazione e configurazione di Designer{#installing-and-configuring-designer}

## Prerequisiti {#pre-requisites}

+++ Per AEM Forms Designer a 64 bit (scelta consigliata)

* Installare la versione a 64 bit di  [Visual C++ 2019 ridistribuibile (x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Prima di avviare l’installazione, assicurati che siano installati i pacchetti runtime ridistribuibili precedentemente menzionati.
* Utente con diritti di amministratore per installare o disinstallare AEM Forms Designer.

+++

+++ Per AEM Forms Designer a 32 bit

* Installare la versione a 32 bit di  [Visual C++ 2019 ridistribuibile (x64)](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170). Prima di avviare l’installazione, assicurati che siano installati i pacchetti runtime ridistribuibili precedentemente menzionati.
* Utente con diritti di amministratore per installare o disinstallare AEM Forms Designer.

+++

>[!NOTE]
>
>* La versione a 64 bit del designer è stata introdotta con AEM 6.5 Forms Service Pack 19 (6.5.19.0).
>* La versione a 32 bit della finestra di progettazione è obsoleta a partire dal rilascio di [AEM Forms Service Pack 21 (6.5.21.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

Per ulteriori informazioni sull&#39;installazione di Forms Designer, visitare [Domande frequenti](#fandq).

## Installare AEM Forms Designer {#install-designer}

Designer è disponibile come programma di installazione autonomo ed è anche fornito in bundle con WorkBench. Se si utilizza un programma di installazione autonomo per AEM Forms Designer, effettuare le seguenti operazioni:

1. Disinstalla la versione precedente di AEM Forms Designer, se è già installata.
1. Scarica AEM Forms Designer a 64 bit (consigliato) o AEM Forms Designer a 32 bit in base alle tue esigenze.

   >[!NOTE]
   > 
   >* La versione di Forms Designer a 32 bit diventerà obsoleta con AEM 6.5 Forms Service Pack 20 (6.5.20.0). L&#39;Adobe consiglia di eseguire l&#39;aggiornamento a Forms Designer a 64 bit.
   >* Forms Designer a 64 bit è disponibile solo per AEM 6.5 Forms Service Pack 19 (6.5.19.0) o versioni successive.
   >* Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0) e versioni successive di Forms Designer includono anche la versione Service Pack. Ad esempio, per Service Pack 15 il numero di versione è 6.5.15.20221112.1.0. In questo esempio, 6.5.15 è la versione del service pack.

1. Avviare il programma di installazione di AEM Forms Designer facendo doppio clic su setup.exe.
1. Procedi e fornisci i tuoi dettagli e il numero di serie nella schermata Personalizzazione.

   >[!NOTE]
   >
   >* Ottenere il codice di licenza di Forms Designer da [Sito Web Adobe Licensing](https://licensing.adobe.com/).

1. Se si accetta il contratto di licenza, fare clic su Avanti per continuare.
1. (Facoltativo) Se si desidera installare Designer in un percorso scelto, modificare il percorso di installazione predefinito. Fai clic su Avanti.
1. Fare clic su Indietro per modificare le preferenze. Per installare Designer, fai clic su Installa.
1. Al termine dell&#39;installazione, fare clic su Fine.

In alternativa, è possibile installare AEM Forms Designer tramite la riga di comando utilizzando la modalità passiva o invisibile all’utente.

* Installazione passiva da riga di comando: il programma di installazione visualizza una barra di avanzamento che indica che l&#39;installazione è in corso ma non vengono visualizzati prompt o messaggi di errore. Una volta avviata, non è possibile annullare l&#39;installazione.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Installazione automatica da riga di comando: il programma di installazione esegue l&#39;installazione senza visualizzare un&#39;interfaccia utente. Non vengono visualizzati prompt, messaggi o finestre di dialogo. Una volta avviata, non è possibile annullare l&#39;installazione.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## Aggiornare AEM Forms Designer {#update-forms-designer}

Esistono due casi in cui si aggiorna l’ultima versione di AEM Forms Designer 6.5.16.0:

* **Caso 1**: quando l’utente dispone di AEM Forms Designer versione precedente al 6.5.15.0.
* **Caso 2**: quando l’utente dispone della versione 6.5.15.0 di AEM Forms Designer.

+++**Se la versione di AEM Forms Designer dell’utente è precedente alla 6.5.15.0.**

Se si utilizza un programma di installazione autonomo per AEM Forms Designer, effettuare le seguenti operazioni:

1. Prima dell’installazione **AEM Forms Designer 6.5.16.0**, gli utenti devono disinstallare tutte le versioni precedenti.
1. Scarica e installa [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) dalla pagina Rilasci del modulo AEM.
1. Dopo aver installato correttamente **AEM Forms Designer 6.5.15.0**, scaricare e installare [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) facendo doppio clic sul file di installazione scaricato.

+++

+++**Se l’utente dispone della versione 6.5.15.0 di AEM Forms Designer**

Se si utilizza un programma di installazione autonomo per AEM Forms Designer, effettuare le seguenti operazioni:
1. Scarica la versione più recente di AEM Forms Designer da [Portale di distribuzione software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Installare la versione più recente di AEM Forms Designer facendo doppio clic sul file di installazione scaricato.

+++

## Domande frequenti {#fandq}

* **Un utente può effettuare l&#39;aggiornamento direttamente a 64 bit?**
   * Sì, gli utenti possono eseguire direttamente l’aggiornamento a designer a 64 bit. Per eseguire l&#39;aggiornamento, installare [SP19](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html?package=/content/software-distribution/it/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip) programma di installazione completo di designer e applicare la versione successiva della patch di designer.

* **Gli utenti possono mantenere installati sia a 32 bit che a 64 bit sul proprio sistema?**
   * No, l&#39;installazione a 32 bit e a 64 bit non funzionerà sullo stesso computer. L&#39;utente può disporre di una finestra di progettazione a 32 bit o a 64 bit.

* **Come verificare se un utente utilizza una finestra di progettazione a 64 bit o a 32 bit?**
   * Esistono due modi per controllare la versione di Forms Designer:

      1. Apri Designer, vai alla Guida in linea, fai clic su Informazioni su Designer e visualizzerai le informazioni sulla versione del designer insieme alle informazioni sui bit. Ad esempio, vedrai che è scritto 64 bit alla fine, come mostrato di seguito:
         `6.5.21.20240522.1.161 | 64 bit`
      1. Apri Designer, in alto a sinistra è visibile un&#39;icona di branding contenente informazioni a 64 bit sul nome del prodotto.