---
title: Oggetto My. Resources | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.Resources
- My.Resources.MyResources.ResourceManager
- My.Resources.MyResources.Culture
dev_langs:
- VB
helpviewer_keywords:
- My.Resources object
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
caps.latest.revision: 22
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6ad5bd4e33438256719b59cb0936cf6bc8525ab1
ms.lasthandoff: 03/13/2017

---
# <a name="myresources-object"></a>Oggetto My.Resources
Fornisce classi e proprietà per accedere alle risorse dell'applicazione.  
  
## <a name="remarks"></a>Note  
 Il `My.Resources` oggetto fornisce accesso alle risorse dell'applicazione e consente in modo dinamico di recuperare le risorse per l'applicazione. Per ulteriori informazioni, vedere [risorse dell'applicazione di gestione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-resources-dotnet).  
  
 Il `My.Resources` oggetto espone solo le risorse globali. Non fornisce accesso ai file di risorse associati ai form. È necessario accedere alle risorse di modulo dal modulo. Per altre informazioni, vedere [Procedura dettagliata: Localizzazione di Windows Form](http://msdn.microsoft.com/en-us/9a96220d-a19b-4de0-9f48-01e5d82679e5).  
  
 È possibile accedere a file di risorse specifiche delle impostazioni cultura dell'applicazione dal `My.Resources` oggetto. Per impostazione predefinita, il `My.Resources` oggetto cerca le risorse dal file di risorse che corrisponde alla lingua nel <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A>proprietà.</xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> Tuttavia, è possibile ignorare questo comportamento e specificare determinate impostazioni cultura da utilizzare per le risorse. Per ulteriori informazioni, vedere [risorse nelle applicazioni Desktop](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890).  
  
## <a name="properties"></a>Proprietà  
 Le proprietà del `My.Resources` oggetto fornisce accesso in sola lettura alle risorse dell'applicazione. Per aggiungere o rimuovere risorse, utilizzare il **progettazione**. Per ulteriori informazioni, vedere [procedura: aggiungere o rimuovere risorse](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d). È possibile accedere alle risorse aggiunte mediante il **progettazione** utilizzando `My.Resources.``resourceName`.  
  
 È inoltre possibile aggiungere o rimuovere i file di risorse selezionando il progetto in **Esplora** e facendo clic su **Aggiungi nuovo elemento** o **Aggiungi elemento esistente** dal **progetto** menu. È possibile accedere alle risorse aggiunte in questo modo tramite `My.Resources.``resourceFileName`.`resourceName`.  
  
 Ogni risorsa ha un nome, categoria e valore, e queste impostazioni determinano l'aspetto delle proprietà per accedere alla risorsa nel `My.Resources` oggetto. Per le risorse aggiunte nel **progettazione**:  
  
-   Il nome determina il nome della proprietà,  
  
-   I dati della risorsa sono il valore della proprietà,  
  
-   La categoria determina il tipo della proprietà:  
  
|Categoria|Tipo di dati di proprietà|  
|---|---|  
|**Stringhe**|[String](../../../visual-basic/language-reference/data-types/string-data-type.md)|  
|**Immagini**|<xref:System.Drawing.Bitmap></xref:System.Drawing.Bitmap>|  
|**Icone**|<xref:System.Drawing.Icon></xref:System.Drawing.Icon>|  
|**Audio**|<xref:System.IO.UnmanagedMemoryStream></xref:System.IO.UnmanagedMemoryStream><br /><br /> La <xref:System.IO.UnmanagedMemoryStream>classe deriva dalla <xref:System.IO.Stream>classe, pertanto può essere utilizzato con metodi che accettano flussi, ad esempio il <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>(metodo).</xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> </xref:System.IO.Stream> </xref:System.IO.UnmanagedMemoryStream>|  
|**File**|-   [Stringa](../../../visual-basic/language-reference/data-types/string-data-type.md) per file di testo.<br />- <xref:System.Drawing.Bitmap>per i file di immagine.</xref:System.Drawing.Bitmap><br />- <xref:System.Drawing.Icon>per i file icona.</xref:System.Drawing.Icon><br />- <xref:System.IO.UnmanagedMemoryStream>per i file audio.</xref:System.IO.UnmanagedMemoryStream>|  
|**Altro**|Determinato dalle informazioni nella finestra di progettazione **tipo** colonna.|  
  
## <a name="classes"></a>Classi  
 Il `My.Resources` oggetto espone ogni file di risorse come una classe con le proprietà condivise. Il nome della classe è identico al nome del file di risorse. Come descritto nella sezione precedente, le risorse in un file di risorse sono esposte come proprietà nella classe.  
  
## <a name="example"></a>Esempio  
 In questo esempio imposta il titolo di un form per la risorsa di stringa denominata `Form1Title` nel file di risorse dell'applicazione. Per eseguire l'esempio, l'applicazione deve disporre di una stringa denominata `Form1Title` nel relativo file di risorse. Per ulteriori informazioni, vedere [procedura: aggiungere o rimuovere risorse](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d).  
  
 [!code-vb[VbVbalrMyResources n.&1;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_1.vb)]  
  
## <a name="example"></a>Esempio  
 In questo esempio imposta l'icona del form sull'icona denominata `Form1Icon` che viene archiviato nel file di risorse dell'applicazione. Per eseguire l'esempio, l'applicazione deve contenere un'icona denominata `Form1Icon` nel relativo file di risorse.  
  
 [!code-vb[VbVbalrMyResources n.&2;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_2.vb)]  
  
## <a name="example"></a>Esempio  
 In questo esempio imposta l'immagine di sfondo di un form per la risorsa immagine denominata `Form1Background`, ovvero nel file di risorse dell'applicazione. Per eseguire questo esempio, l'applicazione deve contenere una risorsa immagine denominata `Form1Background` nel relativo file di risorse.  
  
 [!code-vb[VbVbalrMyResources n.&3;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_3.vb)]  
  
## <a name="example"></a>Esempio  
 In questo esempio riproduce il suono che viene archiviato come una risorsa audio denominata `Form1Greeting` nel file di risorse dell'applicazione. Per eseguire l'esempio, l'applicazione deve contenere una risorsa audio denominata `Form1Greeting` nel relativo file di risorse. Il `My.Computer.Audio.Play` metodo è disponibile solo per le applicazioni Windows Form.  
  
 [!code-vb[VbVbalrMyResources n.&4;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_4.vb)]  
  
## <a name="example"></a>Esempio  
 In questo esempio recupera la versione in lingua francese di una risorsa di stringa dell'applicazione. La risorsa è denominata `Message`. Per modificare le impostazioni cultura che il `My.Resources` oggetto utilizza, l'esempio utilizza <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>  
  
 Per eseguire questo esempio, l'applicazione deve disporre di una stringa denominata `Message` in relativa risorsa file e l'applicazione deve avere la versione in lingua francese del file di risorse, ovvero Resources.fr-FR. resx. Per ulteriori informazioni, vedere [procedura: aggiungere o rimuovere risorse](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d). Se l'applicazione non dispone della versione in lingua francese del file di risorse, il `My.Resource` oggetto recupera la risorsa dal file di risorse di impostazioni cultura predefinite.  
  
 [!code-vb[VbVbalrMyResources&#10;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_5.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: aggiungere o rimuovere risorse](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d)   
 [La gestione delle risorse dell'applicazione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-resources-dotnet)   
 [Risorse nelle applicazioni Desktop](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)   
 [Procedura dettagliata: Localizzazione di Windows Form](http://msdn.microsoft.com/en-us/9a96220d-a19b-4de0-9f48-01e5d82679e5)
