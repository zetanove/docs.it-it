---
title: "Download del pacchetto del registro dei nomi delle autorit&#224; emittenti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ff8b0014-c5d4-4614-90f0-13fcc0ba777a
caps.latest.revision: 3
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 3
---
# Download del pacchetto del registro dei nomi delle autorit&#224; emittenti
In questo argomento viene descritto come scaricare e utilizzare Validating Issuer Name Registry \(VINR\) nel progetto.  
  
## Download della convalida del registro dei nomi delle autorità emittenti  
 VINR è disponibile come pacchetto NuGet, che consente di aggiungere gli assembly e i riferimenti necessari al progetto.  Se NuGet non è già installato, andare su [nuget.org](http://nuget.org) per installarlo.  È possibile visualizzare la cronologia di controllo delle versioni per l'estensione visitando la pagina relativa in NuGet: [Convalida Microsoft del registro dei nomi delle autorità emittenti in NuGet](https://nuget.org/packages/System.IdentityModel.Tokens.ValidatingIssuerNameRegistry/)  
  
#### Download della convalida del registro dei nomi delle autorità emittenti tramite la GUI di Gestione pacchetti  
  
1.  In Visual Studio fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni**, quindi selezionare **Gestisci pacchetti NuGet**.  
  
2.  Nella finestra **Gestisci pacchetti NuGet**, fare clic sulla casella di ricerca e immettere `ValidatingIssuerNameRegistry`, quindi scegliere **Invio**.  
  
3.  Dal riquadro Risultati, fare clic sul pulsante **Installa** per il primo risultato.  
  
4.  Verrà avviato il download del pacchetto.  Prima che venga aggiunto al progetto, verrà visualizzata la finestra di dialogo di conferma della licenza.  Se si accettano i termini di licenza, fare clic su **Accetto**.  
  
5.  Gli assembly VINR più recenti verranno scaricati e aggiunti al progetto.  
  
#### Download della convalida del registro dei nomi delle autorità emittenti tramite la console di Gestione pacchetti  
  
1.  In Visual Studio, fare clic su **Strumenti**, **Gestione pacchetti di librerie**, quindi **Console di gestione pacchetti**.  
  
2.  Verrà aperta la **Console di gestione del pacchetto**.  Immettere il testo seguente e premere **INVIO**:  
  
    ```powershell  
    Install-Package System.IdentityModel.Tokens.ValidatingIssuerNameRegistry  
    ```  
  
3.  Gli assembly VINR più recenti verranno scaricati e aggiunti al progetto.