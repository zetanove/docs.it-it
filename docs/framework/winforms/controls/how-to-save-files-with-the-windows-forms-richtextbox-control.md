---
title: "Procedura: salvare file con il controllo RichTextBox Windows Form | Microsoft Docs"
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
  - ".rtf (file), salvataggio nel controllo RichTextBox"
  - "esempi [Windows Form], caselle di testo"
  - "file, salvataggio con il controllo RichTextBox"
  - "RichTextBox (controllo) [Windows Form], salvataggio di file"
  - "RTF (file), salvataggio nel controllo RichTextBox"
  - "salvataggio di file"
  - "salvataggio di file, RichTextBox (controllo)"
  - "testo (file), salvataggio dal controllo RichTextBox"
ms.assetid: 4a58ec19-84d1-4383-9110-298c06adcfca
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: salvare file con il controllo RichTextBox Windows Form
Il controllo <xref:System.Windows.Forms.RichTextBox> Windows Form consente di scrivere le informazioni da visualizzare in uno dei seguenti formati:  
  
-   Testo normale  
  
-   Testo normale Unicode  
  
-   RTF \(Rich\-Text Format\)  
  
-   RTF con spazi al posto di oggetti OLE  
  
-   Testo normale con una rappresentazione in forma di testo di oggetti OLE  
  
 Per salvare un file, chiamare il metodo <xref:System.Windows.Forms.RichTextBox.SaveFile%2A>,  che può essere utilizzato anche per salvare dati in un flusso.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.RichTextBox.SaveFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>.  
  
### Per salvare il contenuto del controllo in un file  
  
1.  Determinare il percorso del file da salvare.  
  
     Per eseguire questa operazione in un'applicazione reale, viene in genere utilizzato il componente <xref:System.Windows.Forms.SaveFileDialog>.  Per informazioni generali, vedere [Cenni preliminari sul componente SaveFileDialog](../../../../docs/framework/winforms/controls/savefiledialog-component-overview-windows-forms.md).  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> del controllo <xref:System.Windows.Forms.RichTextBox>, specificando il file da salvare e, facoltativamente, un tipo di file.  Se si chiama il metodo utilizzando come unico argomento un nome file, il file verrà salvato come RTF.  Per specificare un altro tipo di file, chiamare il metodo con un valore dell'enumerazione <xref:System.Windows.Forms.RichTextBoxStreamType> come secondo argomento.  
  
     Nell'esempio riportato di seguito, il percorso impostato per la posizione del file RTF coincide con la cartella **Documenti**.  Si consiglia di utilizzare questa posizione perché tale cartella è presente nella maggior parte dei computer che esegue il sistema operativo Windows.  La scelta di questa posizione consente inoltre di eseguire l'applicazione senza problemi agli utenti che dispongono di livelli di accesso minimo.  Nell'esempio riportato di seguito si presuppone che un controllo <xref:System.Windows.Forms.RichTextBox> sia già stato aggiunto al form.  
  
    ```vb  
    Public Sub SaveFile()  
       ' You should replace the bold file name in the   
       ' sample below with a file name of your own choosing.  
       RichTextBox1.SaveFile(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Testdoc.rtf", _  
          RichTextBoxStreamType.RichNoOleObjs)  
    End Sub  
  
    ```  
  
    ```csharp  
    public void SaveFile()  
    {  
       // You should replace the bold file name in the   
       // sample below with a file name of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       richTextBox1.SaveFile(System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Testdoc.rtf",  
          RichTextBoxStreamType.RichNoOleObjs);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void SaveFile()  
       {  
          // You should replace the bold file name in the   
          // sample below with a file name of your own choosing.  
          richTextBox1->SaveFile(String::Concat  
             (System::Environment::GetFolderPath  
             (System::Environment::SpecialFolder::Personal),  
             "\\Testdoc.rtf"), RichTextBoxStreamType::RichNoOleObjs);  
       }  
    ```  
  
    > [!IMPORTANT]
    >  Se il file non esiste, ne viene creato uno nuovo nell'esempio.  Per poter creare un file in un'applicazione, è necessario che l'applicazione disponga di accesso in creazione alla cartella.  Le autorizzazioni vengono impostate tramite gli elenchi di controllo di accesso \(ACL\).  Se il file è già esistente, l'applicazione necessita solo dell'accesso in scrittura, ossia di un privilegio inferiore.  Laddove possibile, è più sicuro creare il file durante la fase di distribuzione e concedere solo accesso in lettura a un unico file, anziché accesso in creazione a una cartella.  È inoltre più sicuro scrivere i dati nelle cartelle utente anziché nella cartella radice o nella cartella Programmi.  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)