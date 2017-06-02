---
title: "Application Settings for Custom Controls | Microsoft Docs"
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
  - "custom controls [Windows Forms], application settings"
  - "application settings [Windows Forms], custom controls"
ms.assetid: f44afb74-76cc-44f2-890a-44b7cdc211a1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Application Settings for Custom Controls
Per consentire ai controlli personalizzati di rendere persistenti le impostazioni dell'applicazione quando sono inclusi in applicazioni di terze parti è necessario eseguire determinate attività.  
  
 La maggior parte della documentazione sulla funzione Impostazioni applicazione è scritta partendo dal presupposto che si crei un'applicazione autonoma.  Se tuttavia si crea un controllo che verrà utilizzato da altri sviluppatori nelle loro applicazioni, è necessario eseguire ulteriori operazioni per garantire la persistenza delle impostazioni del controllo.  
  
## Impostazioni delle applicazioni e controlli personalizzati  
 Per garantire la persistenza delle impostazioni del controllo, è necessario che il processo venga incapsulato nel controllo mediante la creazione di una classe wrapper delle impostazioni dell'applicazione dedicata, derivata dalla classe <xref:System.Configuration.ApplicationSettingsBase>.  La classe principale del controllo, inoltre, deve implementare l'interfaccia <xref:System.Configuration.IPersistComponentSettings>.  Questa contiene varie proprietà nonché due metodi, <xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A> e <xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>.  Se si aggiunge il controllo a un form utilizzando **Progettazione Windows Form** in Visual Studio, il metodo <xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A> verrà chiamato automaticamente all'inizializzazione del controllo. Il metodo <xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A> deve essere chiamato manualmente nel metodo `Dispose` del controllo.  
  
 Inoltre, è necessario implementare quanto segue affinché le impostazioni dell'applicazione per i controlli personalizzati funzionino correttamente in ambienti in fase di progettazione come Visual Studio:  
  
1.  Una classi personalizzata di impostazioni dell'applicazione con un costruttore che accetta <xref:System.ComponentModel.IComponent> come singolo parametro.  Utilizzare questa classe per salvare e caricare tutte le impostazioni dell'applicazione.  Quando si crea una nuova istanza di questa classe, passare il controllo personalizzato utilizzando il costruttore.  
  
2.  Creare questa classe personalizzata di impostazioni dopo aver creato e inserito il controllo in un form, ad esempio nel gestore eventi <xref:System.Windows.Forms.Form.Load> del form.  
  
 Per le istruzioni sulla creazione di una classe di impostazioni personalizzate, vedere [How to: Create Application Settings](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md).  
  
## Chiavi delle impostazioni e impostazioni condivise  
 Alcuni controlli possono essere utilizzati più volte nello stesso form.  In genere è opportuno che le impostazioni dei vari controlli siano rese persistenti.  La proprietà <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> dell'interfaccia <xref:System.Configuration.IPersistComponentSettings> consente di fornire una stringa univoca la cui funzione è di risolvere l'ambiguità tra le varie versioni di un controllo su un form.  
  
 Il modo più semplice per implementare la proprietà <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> consiste nell'utilizzare la proprietà <xref:System.Windows.Forms.Control.Name%2A> del controllo per la proprietà <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A>.  Quando si caricano o salvano le impostazioni del controllo, si passa il valore della proprietà <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> alla proprietà <xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A> della classe <xref:System.Configuration.ApplicationSettingsBase>.  Con la funzione Impostazioni applicazione viene utilizzata tale chiave univoca per rendere persistenti le impostazioni dell'utente in XML.  Nell'esempio di codice riportato di seguito viene illustrato come con la sezione `<userSettings>` venga cercata un'istanza di un controllo personalizzato denominato `CustomControl1` che salva un'impostazione per la proprietà `Text` .  
  
```  
<userSettings>  
    <CustomControl1>  
        <setting name="Text" serializedAs="string">  
            <value>Hello, World</value>  
        </setting>  
    </CustomControl1>  
</userSettings>  
```  
  
 Le istanze di un controllo che non forniscono un valore per la proprietà <xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A> condivideranno le stesse impostazioni.  
  
## Vedere anche  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.IPersistComponentSettings>   
 [Application Settings Architecture](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)