---
title: Persistenza di un oggetto in Visual Studio (Visual Basic) | Microsoft Docs
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: f4b78654f79913d90667daa9e75c88f45f8efbdc
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="walkthrough-persisting-an-object-in-visual-studio-visual-basic"></a>Procedura dettagliata: Persistenza di un oggetto in Visual Studio (Visual Basic)
Sebbene sia possibile impostare le proprietà di un oggetto sui valori predefiniti in fase di progettazione, tutti i valori immessi in fase di esecuzione vengono persi quando l'oggetto viene eliminato. È possibile usare la serializzazione per rendere persistenti i dati di un oggetto tra le istanze, consentendo di archiviare i valori e di recuperarli alla successiva creazione di un'istanza dell'oggetto.  
  
> [!NOTE]
>  In Visual Basic, per archiviare dati semplici, ad esempio un nome o numero, è possibile usare l'oggetto `My.Settings`. Per altre informazioni, vedere [Oggetto My.Settings](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
 In questa procedura verrà creato un oggetto `Loan` semplice i cui dati verranno resi persistenti in un file. I dati verranno quindi recuperati dal file quando si ricrea l'oggetto.  
  
> [!IMPORTANT]
>  Questo esempio crea un nuovo file, se il file non esiste. Se un'applicazione deve creare un file, per tale applicazione deve essere disponibile l'autorizzazione `Create` per la cartella. Le autorizzazioni vengono impostate usando gli elenchi di controllo di accesso. Se il file esiste già, per l'applicazione è necessaria solo l'autorizzazione `Write`, di livello inferiore. Se possibile, è più sicuro creare il file durante la distribuzione e concedere solo autorizzazioni `Read` per un singolo file, anziché autorizzazioni Create per una cartella. Inoltre, è più sicuro scrivere dati nelle cartelle utente anziché nella cartella radice o nella cartella dei file di programma.  
  
> [!IMPORTANT]
>  In questo esempio i dati vengono archiviati in un file binario. Non usare questi formati per i dati riservati, ad esempio password o informazioni sulla carta di credito.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa/Esporta impostazioni** dal menu **Strumenti** . Per altre informazioni, vedere [Personalizzazione delle impostazioni di sviluppo in Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="creating-the-loan-object"></a>Creare l'oggetto Loan  
 Il primo passaggio consiste nel creare una classe `Loan` e un'applicazione di test che usa la classe.  
  
### <a name="to-create-the-loan-class"></a>Per creare la classe Loan  
  
1.  Creare un nuovo progetto di libreria di classi denominato "LoanClass". Per altre informazioni, vedere [Creazione di soluzioni e progetti](http://docs.microsoft.com/visualstudio/ide/creating-solutions-and-projects).  
  
2.  In **Esplora soluzioni** aprire il menu di scelta rapida per il file Class1 e scegliere **Rinomina**. Rinominare il file `Loan` e premere INVIO. Modificando il nome del file, anche la classe verrà rinominata `Loan`.  
  
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
  
 Sarà anche necessario creare un'applicazione semplice che usa la classe `Loan`.  
  
### <a name="to-create-a-test-application"></a>Per creare un'applicazione di test  
  
1.  Per aggiungere un progetto di Windows Form Application alla soluzione, nel menu **File** scegliere **Aggiungi**, **Nuovo progetto**.  
  
2.  Scegliere **Windows Forms Application** nella finestra di dialogo **Aggiungi nuovo progetto**, quindi immettere `LoanApp` come nome del progetto e quindi fare clic su **OK** per chiudere la finestra di dialogo.  
  
3.  Scegliere il progetto LoanApp in **Esplora soluzioni**.  
  
4.  Nel menu **Progetto** scegliere **Imposta come progetto di avvio**.  
  
5.  Scegliere **Aggiungi riferimento** dal menu **Progetto**.  
  
6.  Nella finestra di dialogo **Aggiungi riferimento** scegliere la scheda **Progetti** e quindi il progetto LoanClass.  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
8.  Nella finestra di progettazione aggiungere quattro controlli <xref:System.Windows.Forms.TextBox> al form.  
  
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
  
10. Aggiungere al form un gestore eventi per l'evento `PropertyChanged` usando il codice seguente:  
  
    ```vb  
    Public Sub CustomerPropertyChanged(  
          ByVal sender As Object,  
          ByVal e As System.ComponentModel.PropertyChangedEventArgs  
        ) Handles TestLoan.PropertyChanged  
  
        MsgBox(e.PropertyName & " has been changed.")  
    End Sub  
    ```  
  
 A questo punto, è possibile compilare ed eseguire l'applicazione. Si noti che i valori predefiniti della classe `Loan` vengono visualizzati nelle caselle di testo. Provare a modificare il valore del tasso di interesse da 7.5 a 7.1, quindi chiudere l'applicazione ed eseguirla nuovamente: verrà ripristinato il valore predefinito 7.5.  
  
 Nel mondo reale i tassi di interesse variano periodicamente, ma non necessariamente ogni volta che l'applicazione viene eseguita. Anziché fare in modo che l'utente aggiorni il tasso di interesse ogni volta che viene eseguita l'applicazione, è preferibile mantenere il tasso di interesse più recente tra le istanze dell'applicazione. Nel passaggio successivo verrà eseguita questa operazione, aggiungendo la serializzazione alla classe Loan.  
  
## <a name="using-serialization-to-persist-the-object"></a>Usare la serializzazione per la persistenza dell'oggetto  
 Per rendere persistenti i valori per la classe Loan, per prima cosa contrassegnare la classe con l'attributo `Serializable`.  
  
### <a name="to-mark-a-class-as-serializable"></a>Per contrassegnare una classe come serializzabile  
  
-   Modificare la dichiarazione della classe per la classe Loan come segue:  
  
    ```vb  
    <Serializable()>  
    Public Class Loan  
    ```  
  
 L'attributo `Serializable` indica al compilatore che tutti gli elementi nella classe possono essere resi persistenti in un file. Poiché l'evento `PropertyChanged` è gestito da un oggetto Windows Form, non può essere serializzato. L'attributo `NonSerialized` può essere usato per contrassegnare i membri della classe che non devono essere resi persistenti.  
  
### <a name="to-prevent-a-member-from-being-serialized"></a>Per impedire la serializzazione di un membro  
  
-   Modificare la dichiarazione per l'evento `PropertyChanged` come indicato di seguito:  
  
    ```vb  
    <NonSerialized()>  
    Event PropertyChanged As System.ComponentModel.PropertyChangedEventHandler _  
      Implements System.ComponentModel.INotifyPropertyChanged.PropertyChanged  
    ```  
  
 Il passaggio successivo consiste nell'aggiungere il codice di serializzazione all'applicazione LoanApp. Per serializzare la classe e scriverla in un file, si useranno gli spazi dei nomi <xref:System.IO> e <xref:System.Xml.Serialization>. Per evitare di digitare i nomi completi, è possibile aggiungere riferimenti alle librerie di classe necessarie.  
  
### <a name="to-add-references-to-namespaces"></a>Per aggiungere riferimenti agli spazi dei nomi  
  
-   Aggiungere le seguenti istruzioni all'inizio della classe `Form1`:  
  
    ```vb  
    Imports System.IO  
    Imports System.Runtime.Serialization.Formatters.Binary  
    ```  
  
     In questo caso, si usa un formattatore binario per salvare l'oggetto in formato binario.  
  
 Il passaggio successivo consiste nell'aggiungere codice per deserializzare l'oggetto dal file quando viene creato l'oggetto.  
  
### <a name="to-deserialize-an-object"></a>Per deserializzare un oggetto  
  
1.  Aggiungere una costante alla classe per il nome del file di dati serializzati.  
  
    ```vb  
    Const FileName As String = "..\..\SavedLoan.bin"  
    ```  
  
2.  Modificare il codice nella routine evento `Form1_Load` come indicato di seguito:  
  
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
  
     Si noti che è necessario prima verificare che il file esista. Se esiste, creare una classe <xref:System.IO.Stream> per leggere il file binario e una classe <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> per convertire il file. È anche necessario eseguire la conversione dal tipo di flusso al tipo di oggetto Loan.  
  
 Successivamente è necessario aggiungere codice alla classe `Loan` per il salvataggio dei dati immessi nelle caselle di testo e quindi serializzare la classe in un file.  
  
### <a name="to-save-the-data-and-serialize-the-class"></a>Per salvare i dati e serializzare la classe  
  
-   Aggiungere il codice seguente alla routine evento `Form1_FormClosing`:  
  
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
  
 A questo punto, è nuovamente possibile compilare ed eseguire l'applicazione. Inizialmente i valori predefiniti vengono visualizzati nelle caselle di testo. Provare a modificare i valori e immettere un nome nella quarta casella di testo. Chiudere l'applicazione ed eseguirla nuovamente. Si noti che i nuovi valori ora appaiono nelle caselle di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)
