---
title: "My.Resources Object | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.Resources"
  - "My.Resources.MyResources.ResourceManager"
  - "My.Resources.MyResources.Culture"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Resources object"
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# My.Resources Object
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce proprietà e classi per accedere alle risorse dell'applicazione.  
  
## Note  
 L'oggetto `My.Resources` fornisce accesso alle risorse dell'applicazione e consente di recuperarle dinamicamente.  Per ulteriori informazioni, vedere [Gestione delle risorse delle applicazioni \(.NET\)](/visual-studio/ide/managing-application-resources-dotnet).  
  
 L'oggetto `My.Resources` espone soltanto risorse globali.  Non consente di accedere ai file di risorse associati ai form.  È necessario accedere alle risorse del form dal form stesso.  Per ulteriori informazioni, vedere [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/it-it/9a96220d-a19b-4de0-9f48-01e5d82679e5).  
  
 È possibile accedere ai file di risorse specifici delle impostazioni cultura dell'applicazione dall'oggetto `My.Resources`.  Per impostazione predefinita, l'oggetto `My.Resources` cerca le risorse nel file delle risorse che corrisponde alle impostazioni cultura nella proprietà <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A>.  È comunque possibile eseguire l'override di tale comportamento e specificare impostazioni cultura particolari da utilizzare per le risorse.  Per ulteriori informazioni, vedere [Risorse nelle applicazioni desktop](../Topic/Resources%20in%20Desktop%20Apps.md).  
  
## Proprietà  
 Le proprietà dell'oggetto `My.Resources` forniscono l'accesso di sola lettura alle risorse dell'applicazione.  Per aggiungere o rimuovere risorse, utilizzare **Progettazione progetti**.  Per ulteriori informazioni, vedere [How to: Add or Remove Resources](http://msdn.microsoft.com/it-it/7b77bc06-3952-4799-b029-def3f8f7f88d).  È possibile accedere alle risorse aggiunte mediante **Progettazione progetti** utilizzando `My.Resources.``resourceName`.  
  
 È inoltre possibile aggiungere o rimuovere file di risorse selezionando il progetto in **Esplora soluzioni** e scegliendo **Aggiungi nuovo elemento** o **Aggiungi elemento esistente** dal menu **Progetto**.  È possibile accedere alle risorse aggiunte in tal modo tramite `My.Resources.``resourceFileName`.`resourceName`.  
  
 Per ogni risorsa vengono specificati un nome, una categoria e un valore e queste impostazioni determinano il modo in cui la proprietà che consente l'accesso alla risorsa viene visualizzata nell'oggetto `My.Resources`.  Per le risorse aggiunte in **Progettazione progetti**:  
  
-   Il nome equivale al nome della proprietà,  
  
-   I dati della risorsa equivalgono al valore della proprietà,  
  
-   La categoria equivale al tipo della proprietà:  
  
|||  
|-|-|  
|Categoria|Tipo di dati della proprietà|  
|**Stringhe**|[String](../../../visual-basic/language-reference/data-types/string-data-type.md)|  
|**Immagini**|<xref:System.Drawing.Bitmap>|  
|**Icone**|<xref:System.Drawing.Icon>|  
|**Audio**|<xref:System.IO.UnmanagedMemoryStream><br /><br /> La classe <xref:System.IO.UnmanagedMemoryStream> viene derivata dalla classe <xref:System.IO.Stream> e può quindi essere utilizzata con metodi che accettano flussi, ad esempio il metodo <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>.|  
|**File**|-   [Stringa](../../../visual-basic/language-reference/data-types/string-data-type.md) per file di testo.<br />-   <xref:System.Drawing.Bitmap> per file di immagini.<br />-   <xref:System.Drawing.Icon> per file di icona.<br />-   <xref:System.IO.UnmanagedMemoryStream> per file audio.|  
|**Altro**|Viene determinato dalle informazioni contenute nella colonna **Tipo** nella finestra di progettazione.|  
  
## Classi  
 L'oggetto `My.Resources` espone ogni file di risorse come classe con proprietà condivise.  Il nome della classe equivale al nome del file di risorse.  Come descritto nella sezione precedente, le risorse di un file di risorse vengono esposte come proprietà all'interno della classe.  
  
## Esempio  
 Questo esempio consente di impostare il titolo di un form nella risorsa di tipo stringa denominata `Form1Title` nel file di risorse dell'applicazione.  Per l'esempio funzioni, l'applicazione deve contenere una stringa denominata `Form1Title` nel file di risorse.  Per ulteriori informazioni, vedere [How to: Add or Remove Resources](http://msdn.microsoft.com/it-it/7b77bc06-3952-4799-b029-def3f8f7f88d).  
  
 [!code-vb[VbVbalrMyResources#1](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#1)]  
  
## Esempio  
 Nell'esempio seguente l'icona del form viene impostata sull'icona denominata `Form1Icon` che è memorizzata nel file di risorse dell'applicazione.  Per l'esempio funzioni, l'applicazione deve contenere un'icona denominata `Form1Icon` nel file di risorse.  
  
 [!code-vb[VbVbalrMyResources#2](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#2)]  
  
## Esempio  
 In questo esempio l'immagine di sfondo di un form la risorsa immagine denominata `Form1Background`, che si trova nel file di risorse dell'applicazione.  Per questo esempio funzioni, l'applicazione deve contenere una risorsa immagine denominata `Form1Background` nel file di risorse.  
  
 [!code-vb[VbVbalrMyResources#3](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#3)]  
  
## Esempio  
 In questo esempio viene riprodotto un suono archiviato come risorsa audio denominata `Form1Greeting` nel file di risorse dell'applicazione.  Per l'esempio funzioni, l'applicazione deve contenere una risorsa audio denominata `Form1Greeting` nel file di risorse.  Il metodo `My.Computer.Audio.Play` è disponibile solo per le applicazioni Windows Form.  
  
 [!code-vb[VbVbalrMyResources#4](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#4)]  
  
## Esempio  
 In questo esempio vengono recuperati dalla versione con impostazioni cultura francesi di una risorsa di tipo stringa dell'applicazione.  La risorsa viene denominata `Message`.  Per modificare le impostazioni cultura che `My.Resources` utilizzo dell'oggetto, gli utilizzi di esempio  <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>.  
  
 Per questo esempio funzioni, l'applicazione deve contenere una stringa denominata `Message` nel file di risorse e dell'applicazione disponga della versione con impostazioni cultura francesi del file di risorse, corretto.  Per ulteriori informazioni, vedere [How to: Add or Remove Resources](http://msdn.microsoft.com/it-it/7b77bc06-3952-4799-b029-def3f8f7f88d).  Se l'applicazione non dispone della versione con impostazioni cultura francesi del file di risorse, `My.Resource` l'oggetto recupera la risorsa da un file di risorse delle impostazioni cultura predefinite.  
  
 [!code-vb[VbVbalrMyResources#10](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#10)]  
  
## Vedere anche  
 [How to: Add or Remove Resources](http://msdn.microsoft.com/it-it/7b77bc06-3952-4799-b029-def3f8f7f88d)   
 [Gestione delle risorse delle applicazioni \(.NET\)](/visual-studio/ide/managing-application-resources-dotnet)   
 [Risorse nelle applicazioni desktop](../Topic/Resources%20in%20Desktop%20Apps.md)   
 [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/it-it/9a96220d-a19b-4de0-9f48-01e5d82679e5)