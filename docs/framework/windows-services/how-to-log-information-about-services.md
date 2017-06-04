---
title: "How to: Log Information About Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "AutoLog property"
  - "services, logging information"
  - "Windows Service applications, logging information about"
  - "event logs, service applications"
  - "application event logs, service applications"
  - "logs, service applications"
ms.assetid: c0d8140f-c055-4d8e-a2e0-37358a550116
caps.latest.revision: 17
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 17
---
# How to: Log Information About Services
Per impostazione predefinita, tutti i progetti di servizio di Windows possono interagire con il log eventi dell'applicazione in cui possono scrivere informazioni ed eccezioni. È possibile usare la proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> per indicare se si vuole fornire questa funzionalità nell'applicazione. Per impostazione predefinita, la registrazione è attivata per tutti i servizi creati con il modello di progetto di servizio di Windows. È possibile usare un form statico della classe <xref:System.Diagnostics.EventLog> per scrivere le informazioni sul servizio in un log senza dover creare un'istanza di un componente <xref:System.Diagnostics.EventLog> o registrare manualmente un'origine.  
  
 Il programma di installazione del servizio registra automaticamente ogni servizio nel progetto come origine valida degli eventi con il registro applicazioni sul computer in cui è installato il servizio, quando la registrazione è attivata. Il servizio registra informazioni ogni volta che viene avviato, arrestato, sospeso, riavviato, installato o disinstallato, oltre a registrare tutti gli errori che si verificano. Non è necessario scrivere nessun codice per scrivere voci nel registro quando si usa il comportamento predefinito, perché è il servizio a farlo automaticamente.  
  
 Per scrivere in un registro eventi diverso dal registro applicazioni, è necessario impostare la proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> su `false`, creare il proprio registro eventi personalizzato nel codice dei servizi e registrare il servizio come origine valida delle voci di tale log. È quindi necessario scrivere il codice per registrare le voci nel log quando si verifica un'azione a cui si è interessati.  
  
> [!NOTE]
>  Se si usa un registro eventi personalizzato e si configura l'applicazione di servizio perché vi possa scrivere, è necessario non tentare di accedere al registro eventi prima di impostare la proprietà <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> del servizio nel codice. Il registro eventi ha bisogno del valore di questa proprietà per registrare il servizio come origine valida degli eventi.  
  
### Per abilitare la registrazione predefinita degli eventi per il servizio  
  
-   Impostare la proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> del componente su `true`.  
  
    > [!NOTE]
    >  Per impostazione predefinita, questa proprietà è impostata su `true`. Non è necessario impostarla esplicitamente a meno che non si debba eseguire un'elaborazione più complessa, ad esempio la valutazione di una condizione seguita dall'impostazione della proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> in base al risultato di tale condizione.  
  
### Per disabilitare la registrazione degli eventi per il servizio  
  
-   Impostare la proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> del componente su `false`.  
  
     [!code-csharp[VbRadconService#17](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#17)]
     [!code-vb[VbRadconService#17](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#17)]  
  
### Per configurare la registrazione in un log personalizzato  
  
1.  Impostare la proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> su `false`.  
  
    > [!NOTE]
    >  È necessario impostare <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> su false per usare un log personalizzato.  
  
2.  Configurare un'istanza di un componente <xref:System.Diagnostics.EventLog> nell'applicazione di servizio di Windows.  
  
3.  Creare un log personalizzato chiamando il metodo <xref:System.Diagnostics.EventLog.CreateEventSource%2A> e specificando la stringa di origine e il nome del file di log che si vuole creare.  
  
4.  Impostare la proprietà <xref:System.Diagnostics.EventLog.Source%2A> sull'istanza del componente <xref:System.Diagnostics.EventLog> per la stringa di origine creata nel passaggio 3.  
  
5.  Scrivere le voci accedendo al metodo <xref:System.Diagnostics.EventLog.WriteEntry%2A> nell'istanza del componente <xref:System.Diagnostics.EventLog>.  
  
     Il codice seguente illustra come configurare la registrazione in un log personalizzato.  
  
    > [!NOTE]
    >  In questo esempio di codice un'istanza di un componente <xref:System.Diagnostics.EventLog> è denominata `eventLog1` \(`EventLog1` in Visual Basic\). Se si è creata un'istanza con un altro nome nel passaggio 2, modificare il codice di conseguenza.  
  
     [!code-csharp[VbRadconService#14](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#14)]
     [!code-vb[VbRadconService#14](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#14)]  
    [!code-csharp[VbRadconService#15](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#15)]
    [!code-vb[VbRadconService#15](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#15)]  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)