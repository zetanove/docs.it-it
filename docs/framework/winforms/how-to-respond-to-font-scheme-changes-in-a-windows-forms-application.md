---
title: "How to: Respond to Font Scheme Changes in a Windows Forms Application | Microsoft Docs"
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
  - "Windows Forms, font scheme changes"
ms.assetid: 4db27702-22e7-43bf-a07d-9a004549853c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Respond to Font Scheme Changes in a Windows Forms Application
Nei sistemi operativi Windows l'utente può modificare le impostazioni dei tipi di caratteri a livello di sistema, per variare le dimensioni di visualizzazione del tipo di carattere predefinito.  La modifica di tali impostazioni è fondamentale per gli utenti con problemi di vista e che richiedono tipi di caratteri più grandi per la lettura dei testi sullo schermo.  È possibile impostare l'applicazione Windows Form per rispondere a queste modifiche aumentando o riducendo le dimensioni dei tipi di caratteri e di tutto il testo relativo ogni volta che viene modificata la combinazione dei tipi di caratteri.  Per fare in modo che il form gestisca le modifiche delle dimensioni dei tipi di caratteri in modo dinamico, è possibile aggiungere codice al form.  
  
 Generalmente, il tipo di carattere predefinito utilizzato da Windows Form è quello restituito dalla chiamata dello spazio dei nomi <xref:Microsoft.Win32> a `GetStockObject(DEFAULT_GUI_FONT)`.  Il tipo di carattere restituito dalla chiamata si modifica solo quando viene modificata la risoluzione dello schermo.  Come illustrato nella procedura seguente, è necessario che il codice modifichi il tipo di carattere predefinito in <xref:System.Drawing.SystemFonts.IconTitleFont%2A> per rispondere alle modifiche delle dimensioni del tipo di carattere.  
  
### Per utilizzare il tipo di carattere del desktop e rispondere alle modifiche della combinazioni dei tipi di caratteri  
  
1.  Creare il form e aggiungere i controlli desiderati.  Per ulteriori informazioni, vedere [How to: Create a Windows Forms Application from the Command Line](../../../docs/framework/winforms/how-to-create-a-windows-forms-application-from-the-command-line.md) e [Controlli da utilizzare in Windows Form](../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md).  
  
2.  Aggiungere un riferimento allo spazio dei nomi <xref:Microsoft.Win32> al codice.  
  
     [!code-csharp[WinFormsAutoScaling#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#2)]
     [!code-vb[WinFormsAutoScaling#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#2)]  
  
3.  Aggiungere il codice riportato di seguito al costruttore del form per associare i gestori eventi necessari e per modificare il tipo di carattere predefinito da utilizzare nel form.  
  
     [!code-csharp[WinFormsAutoScaling#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#3)]
     [!code-vb[WinFormsAutoScaling#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#3)]  
  
4.  Implementare un gestore per l'evento <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> che determini il ridimensionamento automatico nel form quando la categoria <xref:Microsoft.Win32.UserPreferenceCategory> si modifica.  
  
     [!code-csharp[WinFormsAutoScaling#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#4)]
     [!code-vb[WinFormsAutoScaling#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#4)]  
  
5.  Infine implementare un gestore per l'evento <xref:System.Windows.Forms.Form.FormClosing> che disconnetta il gestore eventi <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged>.  
  
> [!IMPORTANT]
>  La mancata inclusione del codice determinerà un problema di memoria nell'applicazione.  
  
 [!code-csharp[WinFormsAutoScaling#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#5)]
 [!code-vb[WinFormsAutoScaling#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#5)]  
  
1.  Compilare il codice ed eseguirlo.  
  
### Per modificare manualmente la combinazione dei tipi di caratteri in Windows XP  
  
1.  Mentre l'applicazione Windows Form è in esecuzione, fare clic con il pulsante destro del mouse sul desktop di Windows e scegliere **Proprietà** dal menu di scelta rapida.  
  
2.  Nella finestra di dialogo **Proprietà schermo** fare clic sulla scheda **Aspetto**.  
  
3.  Dalla casella di riepilogo a discesa **Dimensione carattere** selezione una nuova dimensione per il carattere.  
  
     Il form risponderà alle modifiche in fase di esecuzione apportate alla combinazione dei tipi di caratteri del desktop.  Quando l'utente passa da **Normale** a **Caratteri grandi** o a **Caratteri molto grandi**, nel form il tipo di carattere viene modificato e ridimensionato di conseguenza.  
  
## Esempio  
 [!code-csharp[WinFormsAutoScaling#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/WinFormsAutoScaling/CS/Form1.cs#1)]
 [!code-vb[WinFormsAutoScaling#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WinFormsAutoScaling/VB/Form1.vb#1)]  
  
 Il costruttore nell'esempio di codice include una chiamata a `InitializeComponent`, definito al momento della creazione di un nuovo progetto Windows Form in Visual Studio.  Rimuovere questa riga di codice se si sta compilando l'applicazione dalla riga di comando.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>   
 [Automatic Scaling in Windows Forms](../../../docs/framework/winforms/automatic-scaling-in-windows-forms.md)