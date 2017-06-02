---
title: "Procedura: aggiungere controlli senza interfaccia a un Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "NonVisualSelection"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form], non visivi"
  - "controlli invisibili"
  - "controlli non visivi"
  - "controlli Windows Form, aggiunta a form"
  - "controlli Windows Form, non visivi"
ms.assetid: 52134d9c-cff6-4eed-8e2b-3d5eb3bd494e
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: aggiungere controlli senza interfaccia a un Windows Form
Un controllo non visivo, detto anche componente, fornisce funzionalità all'applicazione.  A differenza di altri controlli, i componenti non forniscono un'interfaccia utente e non è quindi necessario visualizzarli nell'area di Progettazione Windows Form.  Quando un componente viene aggiunto a un form, Progettazione Windows Form visualizza un contenitore ridimensionabile nella parte inferiore del form dove vengono visualizzati tutti i componenti.  Una volta aggiunto un controllo al contenitore dei componenti, è possibile selezionare il componente e impostarne le proprietà come per qualsiasi altro controllo del form.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere un componente a un Windows Form  
  
1.  Aprire il form.  Per informazioni, vedere [How to: Display Windows Forms in the Designer](http://msdn.microsoft.com/it-it/bf3f1e5b-ea07-4529-85c6-6af3ded0cec5).  
  
2.  Nella **Casella degli strumenti** fare clic su un componente e trascinarlo nel form.  
  
     Il componente verrà visualizzato nella barra dei componenti.  
  
 È anche possibile aggiungere componenti a un form in fase di esecuzione.  Si tratta di una situazione che si presenta spesso soprattutto perché a differenza dei controlli, che dispongono di un'interfaccia utente, i componenti mancano di forma visiva.  Nell'esempio che segue viene aggiunto un componente <xref:System.Windows.Forms.Timer> in fase di esecuzione.  In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] sono disponibili vari timer diversi; in questo caso, viene utilizzato un componente <xref:System.Windows.Forms.Timer> Windows Form.  Per ulteriori informazioni sui diversi timer in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], vedere [Introduction to Server\-Based Timers](http://msdn.microsoft.com/it-it/adc0bc0a-a519-4812-bafc-fb9d1a5801fc).  
  
> [!CAUTION]
>  I componenti spesso presentano proprietà specifiche dei controlli che è necessario impostare per il corretto funzionamento dei componenti.  Nel caso del componente <xref:System.Windows.Forms.Timer> dell'esempio viene impostata la proprietà `Interval`.  Quando si aggiungono componenti a un progetto, verificare che vengano impostate le proprietà necessarie per un determinato componente.  
  
#### Per aggiungere un componente a un Windows Form a livello di programmazione  
  
1.  Creare un'istanza della classe <xref:System.Windows.Forms.Timer> nel codice.  
  
2.  Impostare la proprietà `Interval` per determinare il tempo tra gli scatti del timer.  
  
3.  Configurare eventuali altre proprietà necessarie per il componente.  
  
     Nel codice riportato di seguito viene illustrata la creazione di un oggetto <xref:System.Windows.Forms.Timer> con la relativa proprietà `Interval` impostata.  
  
    ```vb  
    Public Sub CreateTimer()  
       Dim timerKeepTrack As New System.Windows.Forms.Timer  
       timerKeepTrack.Interval = 1000  
    End Sub  
  
    ```  
  
    ```csharp  
    public void createTimer()  
    {  
       System.Windows.Forms.Timer timerKeepTrack = new  
           System.Windows.Forms.Timer();  
       timerKeepTrack.Interval = 1000;  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void createTimer()  
       {  
          System::Windows::Forms::Timer^ timerKeepTrack = gcnew  
             System::Windows::Forms::Timer();  
          timerKeepTrack->Interval = 1000;  
       }  
    ```  
  
    > [!IMPORTANT]
    >  Il riferimento a un controllo UserControl dannoso può esporre il computer locale a un rischio relativo alla sicurezza.  Questo problema diventa grave nel momento in cui si aggiunge inconsapevolmente al proprio progetto un controllo personalizzato dannoso appositamente sviluppato da un utente con pochi scrupoli.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)   
 [Procedura: aggiungere i controlli ActiveX a Windows Form](../../../../docs/framework/winforms/controls/how-to-add-activex-controls-to-windows-forms.md)   
 [Procedura: copiare i controlli tra Windows Form](../../../../docs/framework/winforms/controls/how-to-copy-controls-between-windows-forms.md)   
 [Inserimento di controlli in Windows Form](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)