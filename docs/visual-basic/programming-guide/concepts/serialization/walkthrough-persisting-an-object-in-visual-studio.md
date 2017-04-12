---
title: Persistenza di un oggetto in Visual Studio (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
ms.assetid: f1d0b562-e349-4dce-ab5f-c05108467030
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0ff6320aee65850b8b445f445f80b4bbe2c9c254
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-persisting-an-object-in-visual-studio-visual-basic"></a>Procedura dettagliata: Persistenza di un oggetto in Visual Studio (Visual Basic)
Sebbene sia possibile impostare proprietà di un oggetto per i valori predefiniti in fase di progettazione, tutti i valori immessi in fase di esecuzione vengono persi quando l'oggetto viene eliminato. È possibile utilizzare la serializzazione per rendere persistenti i dati di un oggetto tra le istanze, che consente di archiviare i valori e recuperarli la volta successiva che viene creata un'istanza dell'oggetto.  
  
> [!NOTE]
>  In Visual Basic, per archiviare dati semplici, ad esempio un nome o numero, è possibile utilizzare il `My.Settings` oggetto. Per ulteriori informazioni, vedere [oggetto My. Settings](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
 In questa procedura dettagliata, si creerà una semplice `Loan` dell'oggetto e mantenere i dati in un file. Si recupererà i dati dal file quando si ricrea l'oggetto.  
  
> [!IMPORTANT]
>  Questo esempio crea un nuovo file, se il file non esiste già. Se un'applicazione deve creare un file, l'applicazione deve `Create` autorizzazione per la cartella. Le autorizzazioni vengono impostate utilizzando gli elenchi di controllo di accesso. Se il file esiste già, l'applicazione deve solo `Write` autorizzazione, un'autorizzazione inferiore. Dove possibile, è più sicuro creare il file durante la distribuzione e concedere solo `Read` delle autorizzazioni per un singolo file (invece di creare autorizzazioni per una cartella). Inoltre, è più sicuro scrivere dati nelle cartelle utente anziché nella cartella radice o la cartella di file di programma.  
  
> [!IMPORTANT]
>  In questo esempio archivia i dati in un file binario. Non utilizzare questi formati per i dati riservati, quali password o informazioni sulla carta di credito.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa/Esporta impostazioni** dal menu **Strumenti** . Per altre informazioni, vedere [Personalizzazione delle impostazioni di sviluppo in Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="creating-the-loan-object"></a>Creazione dell'oggetto di prestito  
 Il primo passaggio consiste nel creare un `Loan` classe e un'applicazione che utilizza la classe di test.  
  
### <a name="to-create-the-loan-class"></a>Per creare la classe di prestito  
  
1.  Creare un nuovo progetto libreria di classi e denominarla "LoanClass". Per altre informazioni, vedere [Creazione di soluzioni e progetti](http://docs.microsoft.com/visualstudio/ide/creating-solutions-and-projects).  
  
2.  In **Esplora**, aprire il menu di scelta rapida per il file Class1 e scegliere **rinominare**. Rinominare il file in `Loan` e premere INVIO. Ridenominazione del file verrà anche rinominare la classe come `Loan`.  
  
3.  Aggiungere i seguenti membri pubblici alla classe:  
  
    ```vb  
    Public Class Loan  
        Implements System.ComponentModel.INotifyPropertyChanged  
  
        Public Property LoanAmount As Double  
        Public Property InterestRate As Double  
        Public Property Term As Integer  
  
        Private p_Customer As String  
        Public Property Customer As String  
            Get  
                Return p_Customer  
            End Get  
            Set(ByVal value As String)  
                p_Customer = value  
                RaiseEvent PropertyChanged(Me,  
                  New System.ComponentModel.PropertyChangedEventArgs("Customer"))  
            End Set  
        End Property  
  
        Event PropertyChanged As System.ComponentModel.PropertyChangedEventHandler _  
          Implements System.ComponentModel.INotifyPropertyChanged.PropertyChanged  
  
        Public Sub New(ByVal loanAmount As Double,  
                       ByVal interestRate As Double,  
                       ByVal term As Integer,  
                       ByVal customer As String)  
  
            Me.LoanAmount = loanAmount  
            Me.InterestRate = interestRate  
            Me.Term = term  
            p_Customer = customer  
        End Sub  
    End Class  
    ```  
  
 È inoltre necessario creare una semplice applicazione che utilizza la `Loan` classe.  
  
### <a name="to-create-a-test-application"></a>Per creare un'applicazione di test  
  
1.  Per aggiungere un progetto applicazione Windows Form alla soluzione, nel **File** menu, scegliere **Aggiungi**,**nuovo progetto**.  
  
2.  Nel **Aggiungi nuovo progetto** finestra di dialogo scegliere **applicazione Windows Form**, quindi immettere `LoanApp` come nome del progetto e quindi fare clic su **OK** per chiudere la finestra di dialogo.  
  
3.  In **Esplora**, scegliere il progetto LoanApp.  
  
4.  Nel **progetto** menu, scegliere **imposta come progetto di avvio**.  
  
5.  Scegliere **Aggiungi riferimento** dal menu **Progetto**.  
  
6.  Nel **Aggiungi riferimento** finestra di dialogo scegliere la **progetti** scheda e quindi scegliere il progetto LoanClass.  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
8.  Nella finestra di progettazione, aggiungere quattro <xref:System.Windows.Forms.TextBox>controlli al form.</xref:System.Windows.Forms.TextBox>  
  
9. Nell'editor di codice aggiungere il seguente codice:  
  
    ```vb  
    Private WithEvents TestLoan As New LoanClass.Loan(10000.0, 0.075, 36, "Neil Black")  
  
    Private Sub Form1_Load() Handles MyBase.Load  
        TextBox1.Text = TestLoan.LoanAmount.ToString  
        TextBox2.Text = TestLoan.InterestRate.ToString  
        TextBox3.Text = TestLoan.Term.ToString  
        TextBox4.Text = TestLoan.Customer  
    End Sub  
    ```  
  
10. Aggiungere un gestore eventi per il `PropertyChanged` eventi al modulo tramite il codice seguente:  
  
    ```vb  
    Public Sub CustomerPropertyChanged(  
          ByVal sender As Object,  
          ByVal e As System.ComponentModel.PropertyChangedEventArgs  
        ) Handles TestLoan.PropertyChanged  
  
        MsgBox(e.PropertyName & " has been changed.")  
    End Sub  
    ```  
  
 A questo punto, è possibile compilare ed eseguire l'applicazione. Si noti che i valori predefiniti di `Loan` classe vengono visualizzati nelle caselle di testo. Provare a modificare il valore di tasso di interesse da 7.5 in 7.1, quindi chiudere l'applicazione ed eseguirla nuovamente, verrà ripristinato il valore predefinito di 7.5.  
  
 Nel mondo reale, tassi di interesse variano periodicamente, ma non necessariamente ogni volta che l'applicazione viene eseguita. Invece di fare in modo che l'utente aggiorni il tasso di interesse ogni volta che viene eseguita l'applicazione, è preferibile mantenere il tasso di interesse più recente tra le istanze dell'applicazione. Nel passaggio successivo, verranno effettuate solo che tramite l'aggiunta di serializzazione per la classe di prestito.  
  
## <a name="using-serialization-to-persist-the-object"></a>Utilizzo della serializzazione per la persistenza dell'oggetto  
 Per rendere persistenti i valori per la classe di prestito, è innanzitutto necessario contrassegnare la classe con il `Serializable` attributo.  
  
### <a name="to-mark-a-class-as-serializable"></a>Per contrassegnare una classe come serializzabile  
  
-   Modificare la dichiarazione di classe per la classe di prestito come segue:  
  
    ```vb  
    <Serializable()>  
    Public Class Loan  
    ```  
  
 Il `Serializable` attributo indica al compilatore che tutti gli elementi nella classe possono essere resi persistenti in un file. Poiché il `PropertyChanged` evento è gestito da un oggetto Windows Form, non può essere serializzato. Il `NonSerialized` attributo può essere utilizzato per contrassegnare i membri di classe che non devono essere mantenuti.  
  
### <a name="to-prevent-a-member-from-being-serialized"></a>Per impedire la serializzazione di un membro  
  
-   Modificare la dichiarazione di `PropertyChanged` evento come indicato di seguito:  
  
    ```vb  
    <NonSerialized()>  
    Event PropertyChanged As System.ComponentModel.PropertyChangedEventHandler _  
      Implements System.ComponentModel.INotifyPropertyChanged.PropertyChanged  
    ```  
  
 Il passaggio successivo consiste nell'aggiungere il codice serializzazione all'applicazione LoanApp. Per serializzare la classe e scriverlo in un file, si utilizzerà il <xref:System.IO>e <xref:System.Xml.Serialization>gli spazi dei nomi.</xref:System.Xml.Serialization> </xref:System.IO> Per evitare di digitare i nomi completi, è possibile aggiungere riferimenti alle librerie di classe necessarie.  
  
### <a name="to-add-references-to-namespaces"></a>Per aggiungere riferimenti agli spazi dei nomi  
  
-   Aggiungere le istruzioni seguenti all'inizio della `Form1` classe:  
  
    ```vb  
    Imports System.IO  
    Imports System.Runtime.Serialization.Formatters.Binary  
    ```  
  
     In questo caso, si utilizza un formattatore binario per salvare l'oggetto in un formato binario.  
  
 Il passaggio successivo consiste nell'aggiungere codice per deserializzare l'oggetto dal file quando viene creato l'oggetto.  
  
### <a name="to-deserialize-an-object"></a>Per deserializzare un oggetto  
  
1.  Aggiungere una costante per la classe per il nome di file di dati serializzati.  
  
    ```vb  
    Const FileName As String = "..\..\SavedLoan.bin"  
    ```  
  
2.  Modificare il codice di `Form1_Load` routine evento come indicato di seguito:  
  
    ```vb  
    Private WithEvents TestLoan As New LoanClass.Loan(10000.0, 0.075, 36, "Neil Black")  
  
    Private Sub Form1_Load() Handles MyBase.Load  
        If File.Exists(FileName) Then  
            Dim TestFileStream As Stream = File.OpenRead(FileName)  
            Dim deserializer As New BinaryFormatter  
            TestLoan = CType(deserializer.Deserialize(TestFileStream), LoanClass.Loan)  
            TestFileStream.Close()  
        End If  
  
        AddHandler TestLoan.PropertyChanged, AddressOf Me.CustomerPropertyChanged  
  
        TextBox1.Text = TestLoan.LoanAmount.ToString  
        TextBox2.Text = TestLoan.InterestRate.ToString  
        TextBox3.Text = TestLoan.Term.ToString  
        TextBox4.Text = TestLoan.Customer  
    End Sub  
    ```  
  
     Si noti che è necessario dapprima verificare che il file esista. Se esiste, creare un <xref:System.IO.Stream>classe per leggere il file binario e <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>(classe) per convertire il file.</xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> </xref:System.IO.Stream> È necessario convertire il tipo di flusso per il tipo di oggetto di prestito.  
  
 Successivamente è necessario aggiungere il codice per salvare i dati immessi nelle caselle di testo per il `Loan` (classe), quindi è necessario serializzare la classe in un file.  
  
### <a name="to-save-the-data-and-serialize-the-class"></a>Per salvare i dati e serializzare la classe  
  
-   Aggiungere il codice seguente per il `Form1_FormClosing` routine evento:  
  
    ```vb  
    Private Sub Form1_FormClosing() Handles MyBase.FormClosing  
        TestLoan.LoanAmount = CDbl(TextBox1.Text)  
        TestLoan.InterestRate = CDbl(TextBox2.Text)  
        TestLoan.Term = CInt(TextBox3.Text)  
        TestLoan.Customer = TextBox4.Text  
  
        Dim TestFileStream As Stream = File.Create(FileName)  
        Dim serializer As New BinaryFormatter  
        serializer.Serialize(TestFileStream, TestLoan)  
        TestFileStream.Close()  
    End Sub  
    ```  
  
 A questo punto, è ancora possibile compilare ed eseguire l'applicazione. Inizialmente, i valori predefiniti vengono visualizzati nelle caselle di testo. Provare a modificare i valori e immettere un nome nella quarta casella di testo. Chiudere l'applicazione e quindi eseguirlo nuovamente. Si noti che i nuovi valori vengono ora visualizzati nelle caselle di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)
