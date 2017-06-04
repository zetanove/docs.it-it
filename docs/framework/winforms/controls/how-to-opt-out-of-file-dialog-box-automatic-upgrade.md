---
title: "Procedura: rifiutare esplicitamente l&#39;aggiornamento automatico della finestra di dialogo File | Microsoft Docs"
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
  - "OpenFileDialog [Windows Form] rifiutare esplicitamente l'aggiornamento automatico"
  - "la finestra di dialogo [Windows Form] il file, rifiutare l'aggiornamento automatico"
  - "Finestra di dialogo file Windows Vista fare rifiutare esplicitamente l'aggiornamento automatico"
  - "SaveFileDialog [Windows Form] rifiutare esplicitamente l'aggiornamento automatico"
  - "AutoUpgradeEnabled (proprietà)"
ms.assetid: 522e482e-cc01-48b1-8d59-9617dc2c4ac1
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: rifiutare esplicitamente l&#39;aggiornamento automatico della finestra di dialogo File
Quando il <xref:System.Windows.Forms.OpenFileDialog> e <xref:System.Windows.Forms.SaveFileDialog> classi vengono utilizzate in un'applicazione, l'aspetto e comportamento dipendono dalla versione di Windows è in esecuzione l'applicazione. Quando un'applicazione che è stata creata il [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] oppure viene visualizzato in precedenza su [!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)], <xref:System.Windows.Forms.OpenFileDialog> e <xref:System.Windows.Forms.SaveFileDialog> vengono visualizzati automaticamente con il [!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)] aspetto e comportamento. A partire dal [!INCLUDE[net_v30_short](../../../../includes/net-v30-short-md.md)], è possibile rifiutare esplicitamente l'aggiornamento automatico per visualizzare il <xref:System.Windows.Forms.OpenFileDialog> e <xref:System.Windows.Forms.SaveFileDialog> con un [!INCLUDE[winxp](../../../../includes/winxp-md.md)]-aspetto e il comportamento.  
  
### <a name="to-opt-out-of-file-dialog-box-automatic-upgrade"></a>Per rifiutare esplicitamente l'aggiornamento automatico della finestra di dialogo file  
  
1.  Impostare il <xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A> proprietà di <xref:System.Windows.Forms.OpenFileDialog> o <xref:System.Windows.Forms.SaveFileDialog> per `false` prima di visualizzare la finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Forms.FileDialog>