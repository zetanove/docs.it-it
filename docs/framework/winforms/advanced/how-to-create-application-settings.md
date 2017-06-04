---
title: "How to: Create Application Settings | Microsoft Docs"
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
  - "application settings, Windows Forms"
  - "application settings, creating"
ms.assetid: 1e7aa347-af75-41e5-89ca-f53cab704f72
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# How to: Create Application Settings
Usando il codice gestito, è possibile creare nuove impostazioni dell'applicazione e associarle alle proprietà nel form o nei controlli del form, in modo che queste impostazioni vengano caricate e salvate automaticamente in fase di esecuzione.  
  
 Nella routine seguente, viene creata manualmente una classe wrapper che deriva da <xref:System.Configuration.ApplicationSettingsBase>.  A questa classe è possibile aggiungere una proprietà accessibile pubblicamente per ogni impostazione dell'applicazione da esporre.  
  
 È anche possibile eseguire questa routine usando la quantità minima di codice nella finestra di progettazione di Visual Studio.  Vedere anche [Procedura: Creare le impostazioni applicazione usando la finestra di progettazione](http://msdn.microsoft.com/library/wabtadw6\(v=vs.110\)).  
  
### Per creare nuove impostazioni dell'applicazione a livello di codice  
  
1.  Aggiungere una nuova classe al progetto e rinominarlo.  Per questa routine la classe verrà chiamata  `MyUserSettings`.  Modificare la definizione della classe in modo che la classe derivi da <xref:System.Configuration.ApplicationSettingsBase>.  
  
2.  Definire una proprietà in questa classe wrapper per ogni impostazione dell'applicazione richiesta e applicare la proprietà con <xref:System.Configuration.ApplicationScopedSettingAttribute> o <xref:System.Configuration.UserScopedSettingAttribute>, in base all'ambito dell'impostazione.  Per altre informazioni sull'ambito delle impostazioni, vedere [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md).  A questo punto, il codice dovrebbe risultare simile al seguente:  
  
     [!code-csharp[ApplicationSettings.Create#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/MyAppSettings.cs#1)]
     [!code-vb[ApplicationSettings.Create#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/MyAppSettings.vb#1)]  
  
3.  Creare un'istanza della classe wrapper nell'applicazione.  Generalmente è un membro privato del form principale.  Dopo aver definito la classe, è necessario associarla a una proprietà. In questo caso, la proprietà <xref:System.Windows.Forms.Form.BackColor%2A> del form.  È possibile farlo con il gestore eventi del form,  `Load` .  
  
     [!code-csharp[ApplicationSettings.Create#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/Form1.cs#2)]
     [!code-vb[ApplicationSettings.Create#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/Form1.vb#2)]  
  
4.  Se si fornisce un modo per modificare le impostazioni in fase di esecuzione, sarà necessario salvare le impostazioni correnti dell'utente su disco quando il form viene chiuso altrimenti le modifiche andranno perse.  
  
     [!code-csharp[ApplicationSettings.Create#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/Form1.cs#3)]
     [!code-vb[ApplicationSettings.Create#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/Form1.vb#3)]  
  
     È stata creata una nuova impostazione dell’applicazione, che è stata associata correttamente alla proprietà specificata.  
  
## Sicurezza di .NET Framework  
 Il provider di impostazioni predefinito, <xref:System.Configuration.LocalFileSettingsProvider>, memorizza le informazioni nei file di configurazione come testo normale.  Questo riduce la protezione dell'accesso ai file fornito dal sistema operativo per l'utente corrente.  Per questo motivo, è necessario prestare attenzione alle informazioni archiviate nei file di configurazione.  Ad esempio, un utilizzo comune per le impostazioni dell'applicazione consiste nell'archiviare le stringhe di connessione che puntano all'archivio dati dell'applicazione.  Tuttavia, per motivi di sicurezza, queste stringhe non devono includere le password.  Per altre informazioni sulle stringhe di connessione, vedere <xref:System.Configuration.SpecialSetting>.  
  
## Vedere anche  
 <xref:System.Configuration.SpecialSettingAttribute>   
 <xref:System.Configuration.LocalFileSettingsProvider>   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [How to: Validate Application Settings](../../../../docs/framework/winforms/advanced/how-to-validate-application-settings.md)