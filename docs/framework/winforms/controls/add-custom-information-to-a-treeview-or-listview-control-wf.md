---
title: "Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ListItem"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "esempi [Windows Form], ListView (controllo)"
  - "esempi [Windows Form], TreeView (controllo)"
  - "ListView (controllo) [Windows Form], aggiunta di informazioni personalizzate"
  - "Tag (proprietà)"
  - "TreeView (controllo) [Windows Form], aggiunta di informazioni personalizzate"
ms.assetid: 68be11de-1d5b-430e-901f-cfbe48d14b19
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView (Windows Form)
È possibile creare un nodo derivato in un controllo <xref:System.Windows.Forms.TreeView> Windows Form o un elemento derivato in un controllo <xref:System.Windows.Forms.ListView>.  La derivazione consente di aggiungere eventuali campi necessari, oltre a metodi e costruttori personalizzati per gestirli.  Questa funzionalità può essere utilizzata, ad esempio, per associare un oggetto Customer a ciascun nodo della struttura ad albero o voce dell'elenco.  Negli esempi seguenti viene utilizzato il controllo <xref:System.Windows.Forms.TreeView>, tuttavia è possibile eseguire la stessa procedura anche con il controllo <xref:System.Windows.Forms.ListView>.  
  
### Per derivare un nodo della struttura ad albero  
  
-   Creare una nuova classe del nodo, derivata dalla classe <xref:System.Windows.Forms.TreeNode>, che presenta un campo personalizzato per la registrazione del percorso di un file.  
  
    ```vb  
    Class myTreeNode  
       Inherits TreeNode  
  
       Public FilePath As String  
  
       Sub New(ByVal fp As String)  
          MyBase.New()  
          FilePath = fp  
          Me.Text = fp.Substring(fp.LastIndexOf("\"))  
       End Sub  
    End Class  
  
    ```  
  
    ```csharp  
    class myTreeNode : TreeNode  
    {  
       public string FilePath;  
  
       public myTreeNode(string fp)  
       {  
          FilePath = fp;  
          this.Text = fp.Substring(fp.LastIndexOf("\\"));  
       }  
    }  
  
    ```  
  
    ```cpp  
    ref class myTreeNode : public TreeNode  
    {  
    public:  
       System::String ^ FilePath;  
  
       myTreeNode(System::String ^ fp)  
       {  
          FilePath = fp;  
          this->Text = fp->Substring(fp->LastIndexOf("\\"));  
       }  
    };  
    ```  
  
### Per utilizzare un nodo della struttura ad albero derivato  
  
1.  È possibile utilizzare il nuovo nodo della struttura ad albero derivato come parametro per le chiamate di funzione.  
  
     Nell'esempio riportato di seguito, il percorso impostato per la posizione del file di testo coincide con la cartella Documenti.  Si consiglia di utilizzare questa posizione perché tale cartella è presente nella maggior parte dei computer che esegue il sistema operativo Windows.  La scelta di questa posizione consente inoltre di eseguire l'applicazione senza problemi agli utenti che dispongono di livelli di accesso minimo.  
  
    ```vb  
    ' You should replace the bold text file   
    ' in the sample below with a text file of your own choosing.  
    TreeView1.Nodes.Add(New myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\ TextFile.txt ") )  
  
    ```  
  
    ```csharp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    treeView1.Nodes.Add(new myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\TextFile.txt") );  
  
    ```  
  
    ```cpp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    treeView1->Nodes->Add(new myTreeNode(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\TextFile.txt")));  
    ```  
  
2.  Se il nodo della struttura ad albero è stato passato e viene indicato come una classe <xref:System.Windows.Forms.TreeNode>, sarà necessario effettuare il cast sulla classe derivata.  Il cast è una conversione esplicita da un tipo di oggetto a un altro.  Per ulteriori informazioni sul cast, vedere [Implicit and Explicit Conversions](../Topic/Implicit%20and%20Explicit%20Conversions%20\(Visual%20Basic\).md) \([!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\), [Operatore \(\)](../Topic/\(\)%20Operator%20\(C%23%20Reference\).md) \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]\) o [Operatore cast: \(\)](../../../../amples/snippets/visualbasic/VS_Snippets_Wpf/DocumentStructure/visualbasic/spec_withstructure-xps/_rels/.rels) \([!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\).  
  
    ```vb  
    Public Sub TreeView1_AfterSelect(ByVal sender As Object, ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       Dim mynode As myTreeNode  
       mynode = CType(e.node, myTreeNode)  
       MessageBox.Show("Node selected is " & mynode.filepath)  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,  
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       myTreeNode myNode = (myTreeNode)e.Node;  
       MessageBox.Show("Node selected is " + myNode.FilePath);  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          myTreeNode ^ myNode = safe_cast<myTreeNode^>(e->Node);  
          MessageBox::Show(String::Concat("Node selected is ",   
             myNode->FilePath));  
       }  
    ```  
  
## Vedere anche  
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)