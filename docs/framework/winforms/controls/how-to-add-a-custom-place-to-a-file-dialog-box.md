---
title: "Procedura: aggiungere un percorso personalizzato a una finestra di dialogo File | Microsoft Docs"
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
  - "percorso personalizzato della finestra di dialogo"
  - "aggiunta di percorso personalizzato della finestra di dialogo"
  - "CustomPlaces (raccolta)"
ms.assetid: 63f6469b-59cd-40f6-9e61-8b5831856780
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: aggiungere un percorso personalizzato a una finestra di dialogo File
Il valore predefinito aprire e salvare le finestre di dialogo in [!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)] dispongono di un'area sul lato sinistro della finestra di dialogo intitolata **collegamenti Preferiti**. Questa area è denominata posizioni personalizzate. Il <xref:System.Windows.Forms.OpenFileDialog> e <xref:System.Windows.Forms.SaveFileDialog> classi consentono di aggiungere cartelle per il <xref:System.Windows.Forms.FileDialog.CustomPlaces%2A> insieme.  
  
> [!NOTE]
>  Affinché un percorso personalizzato venga visualizzato nel <xref:System.Windows.Forms.OpenFileDialog> o <xref:System.Windows.Forms.SaveFileDialog>, <xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A> proprietà deve essere impostata su `true` (predefinito).  
  
### <a name="to-add-a-custom-place-to-a-file-dialog-box"></a>Per aggiungere una posizione personalizzata per una finestra di dialogo  
  
-   Aggiungere un percorso, un GUID di cartella nota o un <xref:System.Windows.Forms.FileDialogCustomPlace> dell'oggetto per il <xref:System.Windows.Forms.FileDialog.CustomPlaces%2A> raccolta nella finestra di dialogo.  
  
     Esempio di codice seguente viene illustrato come aggiungere un percorso:  
  
    ```vb  
    OpenFileDialog1.CustomPlaces.Add("C:\MyCustomPlace")  
    ```  
  
    ```csharp  
    openFileDialog1.CustomPlaces.Add("C:\\MyCustomPlace");  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Forms.FileDialog>   
 <xref:System.Windows.Forms.FileDialogCustomPlacesCollection.Add%2A?displayProperty=fullName>   
 [GUID della cartella nota per percorsi personalizzati della finestra di dialogo File](../../../../docs/framework/winforms/controls/known-folder-guids-for-file-dialog-custom-places.md)