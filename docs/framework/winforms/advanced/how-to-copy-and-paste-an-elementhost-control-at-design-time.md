---
title: "Procedura: copiare e incollare un controllo ElementHost in fase di progettazione | Microsoft Docs"
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
  - "controllo ElementHost, copia e incolla in fase di progettazione"
  - "interoperabilità [WPF]"
  - "Windows Form, copiare e incollare contenuto"
  - "controllo utente WPF, hosting in Windows Form"
ms.assetid: e570375d-2a68-44ba-b4f7-c781af2d20e8
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: copiare e incollare un controllo ElementHost in fase di progettazione
In questa procedura viene illustrato come copiare un controllo Windows Presentation Foundation \(WPF\) in un Windows Form  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per copiare e incollare un controllo ElementHost in fase di progettazione  
  
1.  Aggiungere un nuovo controllo <xref:System.Windows.Controls.UserControl> WPF al progetto Windows Form.  Utilizzare il nome predefinito per il tipo di controllo, ovvero `UserControl1.xaml`.  Per ulteriori informazioni, vedere [Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  Nella finestra **Proprietà** impostare il valore delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> di `UserControl1` su `200`.  
  
3.  Impostare il valore della proprietà <xref:System.Windows.Controls.Control.Background%2A> su `Blue`.  
  
4.  Compilare il progetto.  
  
5.  Aprire `Form1` in Progettazione Windows Form.  
  
6.  Dalla **Casella degli strumenti**, trascinare un'istanza di `UserControl1` nel form.  
  
     Un'istanza di `UserControl1` viene inclusa in un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost1`.  
  
7.  Selezionare `elementHost1` e premere CTRL\+C per copiarlo negli Appunti.  
  
8.  Premere CTRL\+V per incollare il controllo copiato nel form.  
  
     Nel modulo verrà creato un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost2`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Procedura dettagliata: copiare e incollare un controllo ElementHost in Windows Form separati](../../../../docs/framework/winforms/advanced/copy--paste-an-elementhost-control-into-forms.md)   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Utilizzo di controlli WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)