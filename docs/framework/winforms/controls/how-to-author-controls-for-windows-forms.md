---
title: "Procedura: creare controlli per Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form], creazione"
  - "controlli personalizzati [Windows Form], creazione"
  - "UserControl (classe), Windows Form"
ms.assetid: 7570e982-545b-4c3a-a7c7-55581d313400
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: creare controlli per Windows Form
Un controllo rappresenta un collegamento grafico tra l'utente e il programma.  Consente di fornire o elaborare dati, accettare input dell'utente, rispondere a eventi o eseguire diverse altre funzioni che connettono l'utente e l'applicazione.  Poiché un controllo è essenzialmente un componente con un'interfaccia grafica, è in grado di eseguire qualsiasi funzione effettuata da un componente, nonché fornire interazione con l'utente.  I controlli vengono creati per svolgere compiti specifici e la modifica dei controlli costituisce una delle attività di programmazione.  Tenendo presente queste informazioni, nei passaggi riportati di seguito viene offerta una panoramica sul processo di modifica dei controlli.  Nei collegamenti vengono fornite ulteriori informazioni sui singoli passaggi.  
  
> [!NOTE]
>  Per modificare un controllo personalizzato da utilizzare in Web Form, vedere [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md).  
>   
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per modificare un controllo  
  
1.  Stabilire quale operazione dovrà eseguire il controllo o quale ruolo assegnargli nell'applicazione.  Considerare i seguenti fattori:  
  
    -   Tipo di interfaccia grafica necessaria  
  
    -   Interazioni utente specifiche gestite dal controllo  
  
    -   Funzionalità necessaria fornita eventualmente da controlli esistenti  
  
    -   Possibilità di ottenere la funzionalità richiesta combinando diversi controlli Windows Form.  
  
2.  Se occorre un modello a oggetti per il controllo, definire in che modo distribuire la funzionalità in tale modello e suddividere la funzionalità tra il controllo e gli eventuali oggetti subordinati.  Un modello a oggetti può essere utile se si intende creare un controllo complesso o incorporare varie funzionalità.  
  
3.  Determinare il tipo di controllo necessario ai propri scopi, ad esempio controllo utente, controllo personalizzato, controllo Windows Form ereditato.  Per ulteriori informazioni, vedere [Consigli sui tipi di controlli](../../../../docs/framework/winforms/controls/control-type-recommendations.md) e [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md).  
  
4.  Definire la funzionalità sotto forma di proprietà, metodi ed eventi del controllo e dei relativi oggetti subordinati o strutture secondarie e assegnare i livelli di accesso appropriati, ad esempio Public, Protected e così via.  
  
5.  Se il controllo richiede il disegno personalizzato, aggiungere codice appropriato.  Per informazioni dettagliate, vedere [Disegno e rendering di controlli personalizzati](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md).  
  
6.  Se il controllo eredita da <xref:System.Windows.Forms.UserControl>, è possibile eseguire il test del comportamento di runtime compilando il progetto di controllo e eseguendolo in **UserControl Test Container**.  Per ulteriori informazioni, vedere [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
7.  Per poter eseguire il test e il debug del controllo è inoltre possibile creare un nuovo progetto, ad esempio un'applicazione Windows, e inserirlo in un contenitore.  Questo processo viene illustrato in [Procedura dettagliata: modifica di un controllo composito con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md).  
  
8.  Man mano che si aggiungono funzionalità, aggiungerle al progetto di test per verificarne il funzionamento.  
  
9. Ripetere i passaggi per definire la progettazione con maggiore precisione.  
  
10. Inserire il controllo in un package e distribuirlo.  Per informazioni dettagliate, vedere [Distribuzione di applicazioni, servizi e componenti](../Topic/Deploying%20Applications,%20Services,%20and%20Components.md).  
  
## Vedere anche  
 [Procedura dettagliata: modifica di un controllo composito con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [Procedura dettagliata: eredità da un controllo Windows Form con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [Procedura: ereditare dalla classe UserControl](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [Procedura: ereditare dalla classe Control](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [Procedura: ereditare da controlli di Windows Form esistenti](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)