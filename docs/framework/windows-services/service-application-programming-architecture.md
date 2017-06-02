---
title: "Service Application Programming Architecture | Microsoft Docs"
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
  - "ServiceController components, programming architecture"
  - "ServiceBase class, service states"
  - "Windows Service applications, code model"
  - "services, programming architecture"
  - "ServiceController class"
  - "services, states"
  - "ServiceProcessInstaller class, service application code model"
  - "Windows Service applications, states"
ms.assetid: 83230026-d068-4174-97ff-e264c896eb2f
caps.latest.revision: 15
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 15
---
# Service Application Programming Architecture
Le applicazioni di servizio Windows sono basate su una classe che eredita dalla classe <xref:System.ServiceProcess.ServiceBase?displayProperty=fullName>.  Per determinare il comportamento del servizio si esegue l'override dei metodi di questa classe e se ne definiscono le funzionalità.  
  
 Di seguito vengono riportate le classi principali legate alla creazione del servizio.  
  
-   <xref:System.ServiceProcess.ServiceBase?displayProperty=fullName> \- L'override dei metodi dalla classe <xref:System.ServiceProcess.ServiceBase> viene eseguito quando si crea un servizio e si definisce il codice per stabilire il funzionamento del servizio in tale classe ereditata.  
  
-   <xref:System.ServiceProcess.ServiceProcessInstaller?displayProperty=fullName> e <xref:System.ServiceProcess.ServiceInstaller?displayProperty=fullName> \- Consentono di installare e di disinstallare il servizio.  
  
 Per modificare il servizio, è inoltre possibile utilizzare una classe denominata <xref:System.ServiceProcess.ServiceController>.  Questa classe non è legata alla creazione di un servizio, ma può essere utilizzata per avviare, interrompere e passare i comandi al servizio, nonché per restituire una serie di enumerazioni.  
  
## Definizione del comportamento del servizio  
 Nella classe di servizio, si esegue l'override delle funzioni della classe base che stabiliscono ciò che accade quando lo stato del servizio viene modificato in Gestione controllo servizi.  La classe <xref:System.ServiceProcess.ServiceBase> espone i metodi riportati di seguito. Per aggiungere un comportamento personalizzato, è possibile eseguire l'override di tali metodi.  
  
|Metodo|Eseguirne l'override per|  
|------------|------------------------------|  
|<xref:System.ServiceProcess.ServiceBase.OnStart%2A>|Indicare quali operazioni devono essere eseguite quando il servizio viene avviato.  Per un'esecuzione utile del servizio, occorre scrivere il codice in questa routine.|  
|<xref:System.ServiceProcess.ServiceBase.OnPause%2A>|Indicare quali operazioni devono essere eseguite quando il servizio viene sospeso.|  
|<xref:System.ServiceProcess.ServiceBase.OnStop%2A>|Indicare quali operazioni devono essere eseguite quando il servizio viene arrestato.|  
|<xref:System.ServiceProcess.ServiceBase.OnContinue%2A>|Indicare quali operazioni devono essere eseguite quando il servizio riprende il normale funzionamento dopo la sospensione.|  
|<xref:System.ServiceProcess.ServiceBase.OnShutdown%2A>|Indicare quali operazioni devono essere eseguite prima della chiusura del sistema, nel caso in cui il servizio sia in esecuzione in quel momento.|  
|<xref:System.ServiceProcess.ServiceBase.OnCustomCommand%2A>|Indicare quali operazioni devono essere eseguite quando il servizio riceve un comando personalizzato.  Per ulteriori informazioni sui comandi personalizzati, visitare MSDN Online.|  
|<xref:System.ServiceProcess.ServiceBase.OnPowerEvent%2A>|Indicare quali operazioni devono essere eseguite quando il servizio riceve un evento di risparmio energia, come quelli che indicano lo stato di batteria scarica o sospensione.|  
  
> [!NOTE]
>  Tali metodi rappresentano gli stati che il servizio assume nel corso della propria durata, passando da uno stato al successivo.  Il servizio, ad esempio, non risponde a un comando <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> prima che venga chiamato il metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A>.  
  
 Esistono diverse altre proprietà e metodi interessanti,  tra cui:  
  
-   Il metodo <xref:System.ServiceProcess.ServiceBase.Run%2A> della classe <xref:System.ServiceProcess.ServiceBase>.  Si tratta del punto di ingresso principale del servizio.  Quando si crea un servizio utilizzando il modello Servizio Windows, il codice viene inserito nel metodo `Main` dell'applicazione per eseguire il servizio.  Il codice è simile al seguente:  
  
     [!code-csharp[VbRadconService#6](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#6)]
     [!code-vb[VbRadconService#6](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#6)]  
  
    > [!NOTE]
    >  In questi esempi viene utilizzata una matrice di tipo <xref:System.ServiceProcess.ServiceBase>, in cui è possibile aggiungere ciascun servizio contenuto nell'applicazione. Di conseguenza, è possibile eseguire tutti i servizi contemporaneamente.  Se si crea un unico servizio, tuttavia, è possibile non utilizzare la matrice, dichiarare un nuovo oggetto che eredita dalla classe <xref:System.ServiceProcess.ServiceBase> e successivamente eseguirlo.  Per un esempio, vedere [How to: Write Services Programmatically](../../../docs/framework/windows-services/how-to-write-services-programmatically.md).  
  
-   Una serie di proprietà della classe <xref:System.ServiceProcess.ServiceBase>,  che definiscono i metodi da chiamare nel servizio.  Quando la proprietà <xref:System.ServiceProcess.ServiceBase.CanStop%2A>, ad esempio, è impostata su `true`, è possibile chiamare il metodo <xref:System.ServiceProcess.ServiceBase.OnStop%2A>.  Quando la proprietà <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> è impostata su `true`,è possibile chiamare i metodi <xref:System.ServiceProcess.ServiceBase.OnPause%2A> e <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>.  Quando una di queste proprietà viene impostata su `true`, è pertanto necessario eseguire l'override dei metodi associati e definirne l'elaborazione.  
  
    > [!NOTE]
    >  Per un funzionamento corretto, è necessario che il servizio esegua l'override almeno dei metodi <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e <xref:System.ServiceProcess.ServiceBase.OnStop%2A>.  
  
 Per comunicare con un servizio esistente e controllarne il comportamento, è inoltre possibile utilizzare un componente denominato <xref:System.ServiceProcess.ServiceController>.  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)