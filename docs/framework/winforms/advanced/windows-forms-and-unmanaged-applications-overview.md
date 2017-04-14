---
title: "Cenni preliminari su Windows Form e applicazioni non gestite | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "COM [Windows Form]"
  - "Windows Form, non gestito"
  - "interoperabilità COM"
  - "Controlli ActiveX [Windows Form], informazioni sui controlli ActiveX"
  - "Windows Form, interoperabilità"
ms.assetid: 0a26d99d-8135-4895-8760-c9a2b5f67f14
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari su Windows Form e applicazioni non gestite
Le applicazioni e i controlli Windows Form possono interagire con le applicazioni non gestite, con alcune raccomandazioni. Nelle sezioni che seguono vengono descritti configurazioni e scenari supportati e non supportati dalle applicazioni e dai controlli Windows Form.  
  
## Controlli Windows Form e applicazioni ActiveX  
 Fatta eccezione per Microsoft Internet Explorer e MFC \(Microsoft Foundation Classes\), i controlli Windows Form non sono supportati in applicazioni progettate per ospitare controlli ActiveX. Le altre applicazioni e gli strumenti per lo sviluppo in grado di ospitare controlli ActiveX, come i Test Container ActiveX di versioni di Visual Studio precedenti a Visual Studio .NET 2003, non sono host supportati per i controlli Windows Form.  
  
 Queste limitazioni si applicano anche all'uso dei controlli Windows Form tramite l'interoperabilità COM \(Component Object Model\). L'uso di un controllo Windows Form tramite COM Callable Wrapper \(CCW\) è supportato solo in Internet Explorer. Per altre informazioni sull'interoperabilità COM, vedere  
  
 [COM Interop](../Topic/COM%20Interop%20\(Visual%20Basic\).md).  
  
 Nella tabella riportata di seguito è illustrato il supporto per l'hosting ActiveX per i controlli Windows Form.  
  
|Versione di Windows Form|Supporto|  
|------------------------------|--------------|  
|.NET Framework versione 1.0|Internet Explorer 5.01 e versioni successive|  
|.NET Framework 1.1 e versioni successive|Internet Explorer 5.01 e versioni successive<br /><br /> MFC \(Microsoft Foundation Classes\) 7.0 e versioni successive|  
  
## Hosting dei componenti Windows Form come controlli ActiveX  
 In .NET Framework 1.1, il supporto è stato esteso per includere MFC 7.0 e versioni successive. Questo supporto include tutti i contenitori completamente compatibili con il contenitore di controlli ActiveX di MFC 7.0 e versioni successive.  
  
 La registrazione dei controlli Windows Form come controlli ActiveX non è tuttavia supportata, analogamente alla chiamata al metodo `com.ms.win32.Ole32.CoCreateInstance` per i controlli Windows Form. È supportata solo l'attivazione gestita dei controlli Windows Form. Dopo aver creato un controllo Windows Form, è possibile inserirlo in un'applicazione MFC come se fosse un controllo ActiveX.  
  
 Per usare i controlli Windows Form nell'applicazione non gestita, inserire il CLR usando le API per l'hosting del CLR non gestito oppure usare le funzioni di interoperabilità C\+\+. Si consiglia di usare le funzioni di interoperabilità C\+\+.  
  
## Windows Form in applicazioni client COM  
 Quando si apre un Windows Form da un'applicazione client COM, come un'applicazione Visual Basic 6.0 o un'applicazione MFC, il form può presentare comportamenti imprevisti. Ad esempio, quando si preme il tasto TAB, lo stato di attivazione non passa da un controllo a un altro. Se si preme il tasto INVIO quando un pulsante di comando è nello stato di attivazione, l'evento <xref:System.Windows.Forms.Control.Click> del pulsante non viene generato. Può verificarsi un comportamento imprevisto anche per le pressioni dei tasti o l'attività del mouse.  
  
 Questo comportamento si verifica in quanto l'applicazione non gestita non implementa il supporto del ciclo di messaggi richiesto per il funzionamento corretto di Windows Form. Il ciclo di messaggi fornito dall'applicazione client COM è fondamentalmente diverso dal ciclo di messaggi di Windows Form.  
  
 Il ciclo di messaggi di un'applicazione è un ciclo interno di programma che recupera i messaggi dalla coda di messaggi di un thread, li converte e li invia all'applicazione per la gestione. Il ciclo di messaggi di Windows Form non dispone della stessa architettura dei cicli di messaggi fornita dalle applicazioni precedenti, come le applicazioni Visual Basic 6.0 e le applicazioni MFC. I messaggi inseriti nel ciclo dei messaggi possono essere gestiti in modo diverso da quanto previsto nel Windows Form. Di conseguenza, può prodursi un comportamento imprevisto. Alcune combinazioni di tasti potrebbero non funzionare, così come alcune operazioni eseguite con il mouse, oppure alcuni eventi potrebbero non essere generati in modo appropriato.  
  
## Risoluzione di problemi di interoperabilità  
 È possibile risolvere i problemi di interoperabilità visualizzando il form in un ciclo di messaggi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], creato usando il metodo <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName>.  
  
 Perché un Windows Form funzioni correttamente da un'applicazione client COM, è necessario eseguirlo in un ciclo di messaggi Windows Form. Per eseguire questa operazione, adottare uno degli approcci seguenti:  
  
-   Usare il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> per visualizzare il Windows Form. Per altre informazioni, vedere [Procedura: supportare l'interoperabilità COM visualizzando un Windows Form con il metodo ShowDialog](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md).  
  
-   Visualizzare ogni Windows Form in un nuovo thread. Per altre informazioni, vedere [Procedura: supportare l'interoperabilità COM mediante la visualizzazione di ogni Windows Form nel relativo thread](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md).  
  
## Vedere anche  
 [Windows Forms and Unmanaged Applications](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)   
 [COM Interop](../Topic/COM%20Interop%20\(Visual%20Basic\).md)   
 [COM Interoperability in .NET Framework Applications](../Topic/COM%20Interoperability%20in%20.NET%20Framework%20Applications%20\(Visual%20Basic\).md)   
 [COM Interoperability Samples](http://msdn.microsoft.com/it-it/09c38567-6380-4d70-848a-e896a4ca05f4)   
 [Aximp.exe \(Windows Forms ActiveX Control Importer\)](../../../../docs/framework/tools/aximp-exe-windows-forms-activex-control-importer.md)   
 [Exposing .NET Framework Components to COM](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Packaging an Assembly for COM](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)   
 [Registering Assemblies with COM](../../../../docs/framework/interop/registering-assemblies-with-com.md)   
 [Procedura: supportare l'interoperabilità COM visualizzando un Windows Form con il metodo ShowDialog](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)   
 [Procedura: supportare l'interoperabilità COM mediante la visualizzazione di ogni Windows Form nel relativo thread](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)