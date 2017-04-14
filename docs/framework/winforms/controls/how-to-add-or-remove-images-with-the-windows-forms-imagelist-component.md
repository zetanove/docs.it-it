---
title: "Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form | Microsoft Docs"
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
  - "ImageList (componente) [Windows Form], aggiunta di immagini"
  - "ImageList (componente) [Windows Form], rimozione di immagini"
  - "immagini [Windows Form], aggiunta al componente ImageList"
  - "immagini [Windows Form], visualizzazione con controlli"
  - "immagini [Windows Form], rimozione dal componente ImageList"
  - "immagini [Windows Form], archiviazione per i controlli"
ms.assetid: c5eacc56-f769-4e2e-bfb7-f756620913db
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form
Il componente <xref:System.Windows.Forms.ImageList> Windows Form viene solitamente compilato mediante immagini prima di essere associato a un controllo.  Tuttavia, è possibile aggiungere e rimuovere le immagini dopo aver associato l'elenco a un controllo.  
  
> [!NOTE]
>  Se si rimuovono immagini, verificare che la proprietà <xref:System.Windows.Forms.ButtonBase.ImageIndex%2A> di eventuali controlli associati continui a essere valida.  
  
### Per aggiungere le immagini a livello di codice  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A> della proprietà <xref:System.Windows.Forms.ImageList.Images%2A> dell'elenco immagini.  
  
     Nell'esempio di codice riportato di seguito il percorso impostato per la posizione dell'immagine corrisponde alla cartella **Documenti**.  Questo percorso viene utilizzato per il fatto che si suppone che questa directory sia presente sulla maggior parte dei computer con sistema operativo Windows.  Questa scelta consente inoltre agli utenti con livelli minimi di accesso al sistema di eseguire l'applicazione in modo più sicuro.  Per l'esempio è necessario un form a cui sia già stato aggiunto un controllo <xref:System.Windows.Forms.ImageList>.  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add(myImage)  
    End Sub  
  
    ```  
  
    ```csharp  
    public void addImage()  
    {  
    // Be sure that you use an appropriate escape sequence (such as the   
    // @) when specifying the location of the file.  
       System.Drawing.Image myImage =   
         Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
       imageList1.Images.Add(myImage);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void addImage()  
       {  
       // Replace the bold image in the following sample   
       // with your own icon.  
       // Be sure that you use an appropriate escape sequence (such as   
       // \\) when specifying the location of the file.  
          System::Drawing::Image ^ myImage =   
             Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
          imageList1->Images->Add(myImage);  
       }  
    ```  
  
### Per aggiungere immagini con un valore di chiave  
  
-   Utilizzare uno dei metodi <xref:System.Windows.Forms.ImageList.ImageCollection.Add%2A> della proprietà <xref:System.Windows.Forms.ImageList.Images%2A> dell'elenco immagini che accetta un valore di chiave.  
  
     Nell'esempio di codice riportato di seguito il percorso impostato per la posizione dell'immagine corrisponde alla cartella **Documenti**.  Questo percorso viene utilizzato per il fatto che si suppone che questa directory sia presente sulla maggior parte dei computer con sistema operativo Windows.  Questa scelta consente inoltre agli utenti con livelli minimi di accesso al sistema di eseguire l'applicazione in modo più sicuro.  Per l'esempio è necessario un form a cui sia già stato aggiunto un controllo <xref:System.Windows.Forms.ImageList>.  
  
    ```vb  
    Public Sub LoadImage()  
       Dim myImage As System.Drawing.Image = _  
         Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
       ImageList1.Images.Add("myPhoto", myImage)  
    End Sub  
  
    ```  
  
```csharp  
public void addImage()  
{  
// Be sure that you use an appropriate escape sequence (such as the   
// @) when specifying the location of the file.  
   System.Drawing.Image myImage =   
     Image.FromFile  
   (System.Environment.GetFolderPath  
   (System.Environment.SpecialFolder.Personal)  
   + @"\Image.gif");  
   imageList1.Images.Add("myPhoto", myImage);  
}  
  
```  
  
### Per rimuovere tutte le immagini a livello di codice  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.ImageList.ImageCollection.Remove%2A> per rimuovere una singola immagine  
  
     oppure  
  
     Utilizzare il metodo <xref:System.Windows.Forms.ImageList.ImageCollection.Clear%2A> per eliminare tutte le immagini nell'elenco immagini.  
  
    ```vb  
    ' Removes the first image in the image list  
    ImageList1.Images.Remove(myImage)  
    ' Clears all images in the image list  
    ImageList1.Images.Clear()  
  
    ```  
  
```csharp  
// Removes the first image in the image list.  
imageList1.Images.Remove(myImage);  
// Clears all images in the image list.  
imageList1.Images.Clear();  
  
```  
  
### Per rimuovere immagini in base alla chiave  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.ImageList.ImageCollection.RemoveByKey%2A> per rimuovere una singola immagine in base alla propria chiave.  
  
    ```vb  
    ' Removes the image named "myPhoto" from the list.  
    ImageList1.Images.RemoveByKey("myPhoto")  
  
    ```  
  
```csharp  
// Removes the image named "myPhoto" from the list.  
imageList1.Images.RemoveByKey("myPhoto");  
  
```  
  
## Vedere anche  
 [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)   
 [Cenni preliminari sul componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-overview-windows-forms.md)   
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)