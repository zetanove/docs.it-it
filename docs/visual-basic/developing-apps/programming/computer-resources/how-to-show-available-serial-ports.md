---
title: "How to: Show Available Serial Ports in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "serial ports, availability"
  - "My.Computer.Ports.SerialPortNames property"
  - "My.Computer.Ports object"
  - "ports, serial port availability"
ms.assetid: eaf2ee5a-8103-4e10-a205-ed1d4db120ba
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# How to: Show Available Serial Ports in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento viene descritto come utilizzare `My.Computer.Ports` per visualizzare le porte seriali disponibili del computer in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 Per consentire a un utente di selezionare quale porta utilizzare, i nomi delle porte seriali si trovano in un controllo <xref:System.Windows.Forms.ListBox>.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrate tutte le stringhe restituite dalla proprietà `My.Computer.Ports.SerialPortNames`.  Queste stringhe rappresentano i nomi delle porte seriali disponibili sul computer.  
  
 Solitamente, un utente seleziona la porta seriale utilizzata dall'applicazione dall'elenco di porte disponibili.  Nell'esempio riportato di seguito i nomi delle porte seriali sono archiviati in un controllo <xref:System.Windows.Forms.ListBox>.  Per ulteriori informazioni, vedere [Controllo ListBox](../Topic/ListBox%20Control%20\(Windows%20Forms\).md).  
  
 [!code-vb[VbVbalrMyComputer#45](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#45)]  
  
 Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice, si trova in **Connettività e rete**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un riferimento al progetto a System.Windows.Forms.dll.  
  
-   Accesso ai membri dello spazio dei nomi <xref:System.Windows.Forms>.  Aggiungere un'istruzione `Imports` se i nomi dei membri all'interno del codice non sono specificati in modo completo.  Per ulteriori informazioni, vedere [Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
-   Il form deve contenere un controllo <xref:System.Windows.Forms.ListBox> denominato `ListBox1`.  
  
## Programmazione efficiente  
 Non utilizzare il controllo <xref:System.Windows.Forms.ListBox> per visualizzare i nomi delle porte seriali disponibili.  Utilizzare invece un <xref:System.Windows.Forms.ComboBox> o un altro tipo di controllo.  Se non è necessaria una risposta dall'utente, utilizzare un controllo <xref:System.Windows.Forms.TextBox> per visualizzare le informazioni.  
  
> [!NOTE]
>  È possibile che i nomi della porta restituiti da `My.Computer.Ports.SerialPortNames` non siano corretti quando viene eseguito Windows 98.  Per evitare errori dell'applicazione, utilizzare la gestione delle eccezioni, ad esempio l'istruzione `Try...Catch...Finally` o `Using`, quando si utilizzano i nomi delle porte per aprire le porte.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 [How to: Dial Modems Attached to Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)   
 [How to: Send Strings to Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [How to: Receive Strings From Serial Ports](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)