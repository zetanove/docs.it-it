---
title: "Procedura: sviluppare un controllo di Windows Form semplice | Microsoft Docs"
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
  - "Control (classe), Windows Form"
  - "controlli [Windows Form]"
  - "controlli personalizzati [Windows Form], creazione di controlli (mediante il codice)"
ms.assetid: 86cbe435-45b7-4cb4-9b5a-47418369758d
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: sviluppare un controllo di Windows Form semplice
In questa sezione vengono illustrati i passaggi chiave necessari per la creazione di un controllo di Windows Form personalizzato.  Il controllo semplice sviluppato in questa procedura dettagliata consente di modificare l'allineamento della relativa proprietà <xref:System.Windows.Forms.Control.Text%2A>.  Non genera né gestisce alcun evento.  
  
### Per creare un controllo semplice personalizzato  
  
1.  Definire una classe che deriva da <xref:System.Windows.Forms.Control?displayProperty=fullName>.  
  
    ```vb  
    Public Class FirstControl  
       Inherits Control  
  
    End Class  
    ```  
  
    ```csharp  
    public class FirstControl:Control{}  
    ```  
  
2.  Definire delle proprietà.  La definizione di proprietà non è obbligatoria, in quanto i controlli ereditano numerose proprietà dalla classe <xref:System.Windows.Forms.Control>, ma per la maggior parte dei controlli personalizzati vengono in genere definite proprietà aggiuntive. Nel frammento di codice riportato di seguito viene definita una proprietà denominata `TextAlignment`  utilizzata da `FirstControl` per impostare il formato di visualizzazione della proprietà <xref:System.Windows.Forms.Control.Text%2A> ereditata da <xref:System.Windows.Forms.Control>.  Per ulteriori informazioni sulla definizione delle proprietà, vedere [Properties Overview](../Topic/Properties%20Overview.md).  
  
     [!code-csharp[System.Windows.Forms.FirstControl#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#3)]
     [!code-vb[System.Windows.Forms.FirstControl#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#3)]  
  
     Quando si imposta una proprietà che modifica la visualizzazione del controllo, è necessario chiamare il metodo <xref:System.Windows.Forms.Control.Invalidate%2A> per ridisegnare il controllo.  <xref:System.Windows.Forms.Control.Invalidate%2A> è definito nella classe <xref:System.Windows.Forms.Control>.  
  
3.  Eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> protetto ereditato da <xref:System.Windows.Forms.Control> per fornire la logica di rendering al controllo.  Se non si sottopone a override <xref:System.Windows.Forms.Control.OnPaint%2A>, non sarà possibile disegnare il controllo.  Nel frammento di codice riportato di seguito il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> visualizza la proprietà <xref:System.Windows.Forms.Control.Text%2A> ereditata da <xref:System.Windows.Forms.Control> con l'allineamento specificato nel campo `alignmentValue`.  
  
     [!code-csharp[System.Windows.Forms.FirstControl#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#4)]
     [!code-vb[System.Windows.Forms.FirstControl#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#4)]  
  
4.  Specificare attributi per il controllo.  Gli attributi consentono, in fase di progettazione, la corretta visualizzazione del controllo e delle proprietà e degli eventi a esso associati nelle finestre di progettazione visive.  Nel codice riportato di seguito vengono applicati attributi alla proprietà `TextAlignment`.  In una finestra di progettazione quale quella di Visual Studio l'attributo <xref:System.ComponentModel.CategoryAttribute.Category%2A> \(riportato nel frammento di codice\) determina la visualizzazione della proprietà in una categoria logica.  L'attributo <xref:System.ComponentModel.DescriptionAttribute.Description%2A> determina inoltre la visualizzazione di una stringa descrittiva nella parte inferiore della finestra **Proprietà** quando viene selezionata la proprietà `TextAlignment`.  Per ulteriori informazioni sugli attributi, vedere [Design\-Time Attributes for Components](../Topic/Design-Time%20Attributes%20for%20Components.md).  
  
     [!code-csharp[System.Windows.Forms.FirstControl#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#5)]
     [!code-vb[System.Windows.Forms.FirstControl#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#5)]  
  
5.  \(facoltativo\) Specificare risorse per il controllo.  È possibile fornire una risorsa, quale un'immagine bitmap, per il controllo mediante un'opzione di compilazione \(`/res` per C\#\) che consente di associare risorse al controllo.  In fase di esecuzione è possibile recuperare la risorsa utilizzando i metodi della classe <xref:System.Resources.ResourceManager>.  Per ulteriori informazioni sulla creazione e sull'utilizzo delle risorse, vedere [Risorse nelle applicazioni desktop](../../../../docs/framework/resources/index.md).  
  
6.  Compilare e distribuire il controllo.  Per compilare e distribuire `FirstControl,` eseguire i seguenti passaggi:  
  
    1.  Salvare il codice dell'esempio che segue in un file di origine, quale FirstControl.cs o FirstControl.vb.  
  
    2.  Compilare il codice sorgente in un assembly e salvarlo nella directory dell'applicazione.  A tal scopo eseguire il seguente comando dalla directory contenente il file di origine.  
  
        ```vb  
        vbc /t:library /out:[path to your application's directory]/CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll FirstControl.vb  
        ```  
  
        ```csharp  
        csc /t:library /out:[path to your application's directory]/CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll FirstControl.cs  
        ```  
  
         L'opzione di compilazione `/t:library` informa il compilatore che l'assembly creato è una libreria e non un eseguibile.  L'opzione `/out` specifica il percorso e il nome dell'assembly.  L'opzione `/r` fornisce il nome degli assembly ai quali il codice fa riferimento.  In questo esempio verrà creato un assembly privato utilizzabile solo dalle proprie applicazioni.  Sarà pertanto necessario salvarlo nella directory dell'applicazione.  Per ulteriori informazioni sulla creazione del package e sulla distribuzione di un controllo, vedere [Distribuzione](../../../../docs/framework/deployment/net-framework-and-applications.md).  
  
 Nell'esempio che segue è riportato il codice di `FirstControl`.  Il controllo è racchiuso nello spazio dei nomi `CustomWinControls`.  Gli spazi dei nomi forniscono un raggruppamento logico di tipi correlati.  È possibile creare il controllo in un nuovo spazio dei nomi o in uno spazio dei nomi esistente.  In C\# la dichiarazione `using` \(`Imports` in Visual Basic\) consente di accedere ai tipi da uno spazio dei nomi senza utilizzare il nome completo dei tipi.  Nell'esempio riportato di seguito la dichiarazione `using` consente al codice di accedere alla classe <xref:System.Windows.Forms.Control> da <xref:System.Windows.Forms?displayProperty=fullName> semplicemente come <xref:System.Windows.Forms.Control> anziché dovendo utilizzare il nome completo <xref:System.Windows.Forms.Control?displayProperty=fullName>.  
  
 [!code-csharp[System.Windows.Forms.FirstControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#1)]
 [!code-vb[System.Windows.Forms.FirstControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#1)]  
  
## Utilizzo del controllo personalizzato in un form  
 Nell'esempio che segue viene illustrato un form semplice che utilizza `FirstControl`.  Tale esempio consentirà di creare tre istanze di `FirstControl`, ciascuna con un valore differente per la proprietà `TextAlignment`.  
  
#### Per compilare ed eseguire l'esempio  
  
1.  Salvare il codice dell'esempio riportato di seguito in un file di origine, quale SimpleForm.cs o SimpleForms.vb.  
  
2.  Compilare il codice sorgente in un assembly eseguibile utilizzando il seguente comando dalla directory contenente il file di origine.  
  
    ```vb  
    vbc /r:CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll SimpleForm.vb  
    ```  
  
    ```csharp  
    csc /r:CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll SimpleForm.cs  
    ```  
  
     CustomWinControls.dll è l'assembly che contiene la classe`FirstControl`.  È necessario che questo assembly si trovi nella stessa directory del file di origine del form che vi accede \(SimpleForm.cs o SimpleForms.vb\).  
  
3.  Eseguire SimpleForm.exe utilizzando il seguente comando.  
  
    ```  
    SimpleForm  
    ```  
  
 [!code-csharp[System.Windows.Forms.FirstControl#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/SimpleForm.cs#10)]
 [!code-vb[System.Windows.Forms.FirstControl#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/SimpleForm.vb#10)]  
  
## Vedere anche  
 [Proprietà dei controlli Windows Form](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [Eventi nei controlli di Windows Form](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)