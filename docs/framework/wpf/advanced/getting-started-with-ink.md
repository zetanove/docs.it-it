---
title: "Nozioni di base sull&#39;input penna | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "animazione, colori dei pennelli sfumati"
  - "pennelli, animazione dei colori"
  - "pennello sfumato, animazione dei colori"
  - "codice procedurale anziché XAML"
  - "XAML, codice procedurale anziché"
ms.assetid: 760332dd-594a-475d-865b-01659db8cab7
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Nozioni di base sull&#39;input penna
Incorporare l'input penna nelle applicazioni è più facile che mai.  Nata per effetto del metodo di programmazione di Windows Forms e COM, questa tecnologia si è evoluta fino a raggiungere la piena integrazione in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Non è necessario installare SDK o librerie di runtime distinte.  
  
## Prerequisiti  
 Per poter utilizzare gli esempi seguenti, è necessario installare Microsoft Visual Studio 2005 e [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)].  È inoltre necessario disporre di conoscenze su come scrivere applicazioni per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per ulteriori informazioni su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  
  
## Avvio rapido  
 Questa sezione consente di scrivere una semplice applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che raccoglie input penna.  
  
 Se questa operazione non è già stata eseguita, installare Microsoft Visual Studio 2005 e [!INCLUDE[TLA#tla_winfxsdk](../../../../includes/tlasharptla-winfxsdk-md.md)].  È in genere necessario compilare le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] prima di poterle visualizzare, anche se sono costituite interamente da codice [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Tuttavia, [!INCLUDE[TLA#tla_winfxsdk](../../../../includes/tlasharptla-winfxsdk-md.md)] include un'applicazione, XAMLPad, progettata per velocizzare il processo di implementazione di un'interfaccia utente basata su [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  È possibile utilizzare tale applicazione per visualizzare e iniziare a eseguire i primi esempi riportati in questo documento.  Il processo di creazione di applicazioni compilate da [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] viene descritto più avanti in questo documento.  
  
 Per avviare XAMLPad, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Windows SDK**, **Strumenti**e quindi **XAMLPad**.  Nel riquadro di rendering XAMLPad esegue il rendering del codice XAML scritto nel riquadro del codice.  È possibile modificare il codice XAML. In questo caso, le modifiche verranno immediatamente visualizzate nel riquadro di rendering.  
  
#### Input penna già disponibile  
 Per avviare la prima applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che supporta l'input penna:  
  
1.  Aprire Microsoft Visual Studio 2005  
  
2.  Creare una nuova **applicazione Windows \(WPF\)**  
  
3.  Digitare `<InkCanvas/>` tra i tag `<Grid>`  
  
4.  Premere **F5** per avviare l'applicazione nel debugger  
  
5.  Utilizzando uno stilo o il mouse, scrivere hello world nella finestra  
  
 È stato scritto l'equivalente dell'input penna di un'applicazione "hello world" con appena 12 battute di tasti.  
  
#### Personalizzare l'applicazione  
 Per sfruttare alcune funzionalità di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)],  sostituire tutto il contenuto tra il tag di apertura \<Window\> e il tag di chiusura \<\/Window\> con il seguente markup per ottenere uno sfondo con pennello a sfumatura sulla superficie dell'input penna.  
  
 [!code-xml[DigitalInkTopics#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml#1)]  
[!code-xml[DigitalInkTopics#1a](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml#1a)]  
  
#### Utilizzo dell'animazione  
 Per aggiungere un effetto divertente, animare i colori del pennello a sfumatura.  Aggiungere il seguente codice [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] dopo il tag di chiusura `</InkCanvas>` ma prima del tag di chiusura `</Page>`.  
  
 [!code-xml[DigitalInkTopics#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml#2)]  
  
#### Aggiunta di codice sottostante a XAML  
 Anche se il linguaggio XAML consente di progettare molto agevolmente l'interfaccia utente, per le applicazioni reali è necessario aggiungere codice per gestire gli eventi.  Di seguito è riportato un semplice esempio in cui l'input penna viene ingrandito in risposta a un clic con il pulsante destro del mouse:  
  
 Impostare il gestore `MouseRightButtonUp` in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]:  
  
 [!code-xml[DigitalInkTopics#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#3)]  
  
 In Esplora soluzioni di Visual Studio espandere Windows1.xaml e aprire il file code\-behind, ossia Window1.xaml.cs o Window1.xaml.vb se si utilizza Visual Basic.  Aggiungere il codice del gestore eventi seguente:  
  
 [!code-csharp[DigitalInkTopics#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml.cs#4)]
 [!code-vb[DigitalInkTopics#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window2.xaml.vb#4)]  
  
 A questo punto, eseguire l'applicazione.  Aggiungere un input penna e quindi fare clic con il pulsante destro del mouse o eseguire un'operazione equivalente tenendo premuto un tasto con uno stilo.  
  
#### Utilizzo di codice procedurale anziché XAML  
 È possibile accedere a tutte le funzionalità di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] da codice procedurale.  Di seguito è riportata un'applicazione "Hello Ink World" di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che non utilizza [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Incollare il codice seguente in un'applicazione console vuota in Visual Studio.  Aggiungere i riferimenti agli assembly PresentationCore, PresentationFramework e WindowsBase, quindi compilare l'applicazione premendo **F5**:  
  
 [!code-csharp[InkCanvasConsoleApp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasConsoleApp/CSharp/Program.cs#1)]
 [!code-vb[InkCanvasConsoleApp#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InkCanvasConsoleApp/VisualBasic/Module1.vb#1)]  
  
## Vedere anche  
 [Input penna](../../../../docs/framework/wpf/advanced/digital-ink.md)   
 [Raccolta di input penna](../../../../docs/framework/wpf/advanced/collecting-ink.md)   
 [Riconoscimento della grafia](../../../../docs/framework/wpf/advanced/handwriting-recognition.md)   
 [Memorizzazione dell'input penna](../../../../docs/framework/wpf/advanced/storing-ink.md)