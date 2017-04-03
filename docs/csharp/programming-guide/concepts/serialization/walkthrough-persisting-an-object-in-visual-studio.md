---
title: 'Procedura dettagliata: Persistenza di un oggetto in Visual Studio (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: get-started-article
dev_langs:
- CSharp
ms.assetid: a544ce46-ee25-49da-afd4-457a3d59bf63
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f76e40e2503bf857922490d728c3a9f3432aa31f
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-persisting-an-object-in-visual-studio-c"></a>Procedura dettagliata: Persistenza di un oggetto in Visual Studio (C#)
Sebbene sia possibile impostare le proprietà di un oggetto sui valori predefiniti in fase di progettazione, tutti i valori immessi in fase di esecuzione vengono persi quando l'oggetto viene eliminato. È possibile usare la serializzazione per rendere persistenti i dati di un oggetto tra le istanze, consentendo di archiviare i valori e di recuperarli alla successiva creazione di un'istanza dell'oggetto.  
  
 In questa procedura verrà creato un oggetto `Loan` semplice i cui dati verranno resi persistenti in un file. I dati verranno quindi recuperati dal file quando si ricrea l'oggetto.  
  
> [!IMPORTANT]
>  Questo esempio crea un nuovo file se il file non esiste già. Se un'applicazione deve creare un file, per tale applicazione deve essere disponibile l'autorizzazione `Create` per la cartella. Le autorizzazioni vengono impostate usando gli elenchi di controllo di accesso. Se il file esiste già, per l'applicazione è necessaria solo l'autorizzazione `Write`, di livello inferiore. Se possibile, è più sicuro creare il file durante la distribuzione e concedere solo autorizzazioni `Read` per un singolo file, anziché autorizzazioni Create per una cartella. Inoltre, è più sicuro scrivere dati nelle cartelle utente anziché nella cartella radice o nella cartella dei file di programma.  
  
> [!IMPORTANT]
>  In questo esempio i dati vengono archiviati in un file in formato binario. Non usare questi formati per i dati riservati, ad esempio password o informazioni sulla carta di credito.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa/Esporta impostazioni** dal menu **Strumenti** . Per altre informazioni, vedere [Personalizzazione delle impostazioni di sviluppo in Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="creating-the-loan-object"></a>Creare l'oggetto Loan  
 Il primo passaggio consiste nel creare una classe `Loan` e un'applicazione di test che usa la classe.  
  
### <a name="to-create-the-loan-class"></a>Per creare la classe Loan  
  
1.  Creare un nuovo progetto di libreria di classi denominato "LoanClass". Per altre informazioni, vedere [Creazione di soluzioni e progetti](https://docs.microsoft.com/visualstudio/ide/creating-solutions-and-projects).  
  
2.  In **Esplora soluzioni** aprire il menu di scelta rapida per il file Class1 e scegliere **Rinomina**. Rinominare il file `Loan` e premere INVIO. Modificando il nome del file, anche la classe verrà rinominata `Loan`.  
  
3.  Aggiungere i seguenti membri pubblici alla classe:  
  
    ```csharp  
    public class Loan : System.ComponentModel.INotifyPropertyChanged  
    {  
        public double LoanAmount {get; set;}  
        public double InterestRate {get; set;}  
        public int Term {get; set;}  
  
        private string p_Customer;  
        public string Customer  
        {  
            get { return p_Customer; }  
            set   
            {  
                p_Customer = value;  
                PropertyChanged(this,  
                  new System.ComponentModel.PropertyChangedEventArgs("Customer"));  
            }  
        }  
  
        public event System.ComponentModel.PropertyChangedEventHandler PropertyChanged;  
  
        public Loan(double loanAmount,  
                    double interestRate,  
                    int term,  
                    string customer)  
        {  
            this.LoanAmount = loanAmount;  
            this.InterestRate = interestRate;  
            this.Term = term;  
            p_Customer = customer;  
        }  
    }  
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
  
    ```csharp  
    private LoanClass.Loan TestLoan = new LoanClass.Loan(10000.0, 0.075, 36, "Neil Black");  
  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        textBox1.Text = TestLoan.LoanAmount.ToString();  
        textBox2.Text = TestLoan.InterestRate.ToString();  
        textBox3.Text = TestLoan.Term.ToString();  
        textBox4.Text = TestLoan.Customer;  
    }  
    ```  
  
10. Aggiungere al form un gestore eventi per l'evento `PropertyChanged` usando il codice seguente:  
  
    ```csharp  
    private void CustomerPropertyChanged(object sender,   
        System.ComponentModel.PropertyChangedEventArgs e)  
    {  
        MessageBox.Show(e.PropertyName + " has been changed.");  
    }  
    ```  
  
 A questo punto, è possibile compilare ed eseguire l'applicazione. Si noti che i valori predefiniti della classe `Loan` vengono visualizzati nelle caselle di testo. Provare a modificare il valore del tasso di interesse da 7.5 a 7.1, quindi chiudere l'applicazione ed eseguirla nuovamente: verrà ripristinato il valore predefinito 7.5.  
  
 Nel mondo reale i tassi di interesse variano periodicamente, ma non necessariamente ogni volta che l'applicazione viene eseguita. Anziché fare in modo che l'utente aggiorni il tasso di interesse ogni volta che viene eseguita l'applicazione, è preferibile mantenere il tasso di interesse più recente tra le istanze dell'applicazione. Nel passaggio successivo verrà eseguita questa operazione, aggiungendo la serializzazione alla classe Loan.  
  
## <a name="using-serialization-to-persist-the-object"></a>Usare la serializzazione per la persistenza dell'oggetto  
 Per rendere persistenti i valori per la classe Loan, per prima cosa contrassegnare la classe con l'attributo `Serializable`.  
  
### <a name="to-mark-a-class-as-serializable"></a>Per contrassegnare una classe come serializzabile  
  
-   Modificare la dichiarazione della classe per la classe Loan come segue:  
  
    ```csharp  
    [Serializable()]  
    public class Loan : System.ComponentModel.INotifyPropertyChanged  
    {  
    ```  
  
 L'attributo `Serializable` indica al compilatore che tutti gli elementi nella classe possono essere resi persistenti in un file. Poiché l'evento `PropertyChanged` è gestito da un oggetto Windows Form, non può essere serializzato. L'attributo `NonSerialized` può essere usato per contrassegnare i membri della classe che non devono essere resi persistenti.  
  
### <a name="to-prevent-a-member-from-being-serialized"></a>Per impedire la serializzazione di un membro  
  
-   Modificare la dichiarazione per l'evento `PropertyChanged` come indicato di seguito:  
  
    ```csharp  
    [field: NonSerialized()]  
    public event System.ComponentModel.PropertyChangedEventHandler PropertyChanged;  
    ```  
  
 Il passaggio successivo consiste nell'aggiungere il codice di serializzazione all'applicazione LoanApp. Per serializzare la classe e scriverla in un file, si useranno gli spazi dei nomi <xref:System.IO> e <xref:System.Xml.Serialization>. Per evitare di digitare i nomi completi, è possibile aggiungere riferimenti alle librerie di classe necessarie.  
  
### <a name="to-add-references-to-namespaces"></a>Per aggiungere riferimenti agli spazi dei nomi  
  
-   Aggiungere le seguenti istruzioni all'inizio della classe `Form1`:  
  
    ```csharp  
    using System.IO;  
    using System.Runtime.Serialization.Formatters.Binary;  
    ```  
  
     In questo caso, si usa un formattatore binario per salvare l'oggetto in formato binario.  
  
 Il passaggio successivo consiste nell'aggiungere codice per deserializzare l'oggetto dal file quando viene creato l'oggetto.  
  
### <a name="to-deserialize-an-object"></a>Per deserializzare un oggetto  
  
1.  Aggiungere una costante alla classe per il nome del file di dati serializzati.  
  
    ```csharp  
    const string FileName = @"..\..\SavedLoan.bin";  
    ```  
  
2.  Modificare il codice nella routine evento `Form1_Load` come indicato di seguito:  
  
    ```csharp  
    private LoanClass.Loan TestLoan = new LoanClass.Loan(10000.0, 0.075, 36, "Neil Black");  
  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        if (File.Exists(FileName))  
        {  
            Stream TestFileStream = File.OpenRead(FileName);  
            BinaryFormatter deserializer = new BinaryFormatter();  
            TestLoan = (LoanClass.Loan)deserializer.Deserialize(TestFileStream);  
            TestFileStream.Close();  
        }  
  
        TestLoan.PropertyChanged += this.CustomerPropertyChanged;  
  
        textBox1.Text = TestLoan.LoanAmount.ToString();  
        textBox2.Text = TestLoan.InterestRate.ToString();  
        textBox3.Text = TestLoan.Term.ToString();  
        textBox4.Text = TestLoan.Customer;  
    }  
    ```  
  
     Si noti che è necessario prima verificare che il file esista. Se esiste, creare una classe <xref:System.IO.Stream> per leggere il file binario e una classe <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> per convertire il file. È anche necessario eseguire la conversione dal tipo di flusso al tipo di oggetto Loan.  
  
 Successivamente è necessario aggiungere codice alla classe `Loan` per il salvataggio dei dati immessi nelle caselle di testo e quindi serializzare la classe in un file.  
  
### <a name="to-save-the-data-and-serialize-the-class"></a>Per salvare i dati e serializzare la classe  
  
-   Aggiungere il codice seguente alla routine evento `Form1_FormClosing`:  
  
    ```csharp  
    private void Form1_FormClosing(object sender, FormClosingEventArgs e)  
    {  
        TestLoan.LoanAmount = Convert.ToDouble(textBox1.Text);  
        TestLoan.InterestRate = Convert.ToDouble(textBox2.Text);  
        TestLoan.Term = Convert.ToInt32(textBox3.Text);  
        TestLoan.Customer = textBox4.Text;  
  
        Stream TestFileStream = File.Create(FileName);  
        BinaryFormatter serializer = new BinaryFormatter();  
        serializer.Serialize(TestFileStream, TestLoan);  
        TestFileStream.Close();  
    }  
    ```  
  
 A questo punto, è nuovamente possibile compilare ed eseguire l'applicazione. Inizialmente i valori predefiniti vengono visualizzati nelle caselle di testo. Provare a modificare i valori e immettere un nome nella quarta casella di testo. Chiudere l'applicazione ed eseguirla nuovamente. Si noti che i nuovi valori ora appaiono nelle caselle di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione (C#)](../../../../csharp/programming-guide/concepts/serialization/index.md)   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)

