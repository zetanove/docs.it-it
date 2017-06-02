---
title: "Elaborazione di ordini con criteri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 66833724-dc36-4fad-86b0-59ffeaa3ba6a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Elaborazione di ordini con criteri
Nell’esempio dei Criteri di elaborazione degli ordini vengono illustrate alcune delle funzionalità principali introdotte nel [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] di Windows Workflow Foundation \(WF\).Di seguito viene esposta una nuova funzionalità per il motore di regole WF:  
  
-   supporto per l’overload degli operatori.  
  
-   Il supporto per l'operatore `new` consente agli utenti di creare nuovi oggetti e matrici dalle regole WF.  
  
-   Supporto per i metodi di estensione per migliorare l’esperienza utente nel chiamare metodi di estensione dalle regole WF compatibili con gli stili di codifica C\#.  
  
> [!NOTE]
>  Questo esempio richiede che [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] sia installato e pronto per la compilazione e l'esecuzione.Per aprire i file del progetto e della soluzione è richiesto [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
 Nell’esempio viene illustrato un progetto `OrderProcessingPolicy` nel quale viene immesso un ordine del cliente, costituito da un elenco numerato di elementi disponibili e un codice postale.L'ordine viene elaborato correttamente se entrambi le voci sono corrette; in caso contrario, i criteri creano oggetti di errore, utilizzando un operatore `+` di overload e un metodo di estensione predefinito per informare l'utente degli errori.  
  
> [!NOTE]
>  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] metodi di estensione, vedere [C\# Version 3.0 Specification](http://go.microsoft.com/fwlink/?LinkId=95402).  
  
 L’esempio comprende i progetti seguenti:  
  
-   `OrderErrorLibrary`  
  
     `OrderErrorLibrary` è una libreria di classi che definisce le classi `OrderError` e `OrderErrorCollection`.Un'istanza `OrderError` viene creata quando viene immesso un input non valido.La libreria fornisce anche un metodo di estensione sulla classe `OrderErrorCollection` che restituisce la proprietà `ErrorText` su tutti gli oggetti `OrderError` in `OrderErrorCollection`.  
  
-   `OrderProcessingPolicy`  
  
     Il progetto `OrderProcessingPolicy` è un'applicazione console di WF che definisce una sola attività `PolicyFromFile`.L'attività dispone delle regole seguenti:  
  
    -   `invalidItemNum`  
  
         Questa regola convalida che il numero dell'elemento è compreso tra 1 e 6, incluso.Se il numero dell'elemento rientra nell'intervallo valido, la regola non esegue alcuna operazione \(ad eccezione della stampa alla console\).Se il numero dell'elemento non rientra tra 1 e 6, la regola `invalidItemNum` esegue le operazioni seguenti:  
  
        1.  Crea un oggetto `OrderError` nuovo, passando a quest’ultimo il numero dell'elemento immesso, e imposta le proprietà `ErrorText` e `CustomerName` sull'oggetto.  
  
        2.  Crea un oggetto `invalidItemNumErrorCollection`.  
  
        3.  Aggiunge l’istanza `OrderError` di recente creazione a `invalidItemNumErrorCollection`.  
  
         In questo modo viene illustrato il supporto per l'operatore `new` con il quale è possibile creare un'istanza di oggetti nelle regole.  
  
    -   `invalidZip`  
  
         Questa regola convalida che il CAP dispone di 5 cifre ed è compreso nell'intervallo da 600 a 99998.Se il numero del CAP rientra nell'intervallo valido, la regola non esegue alcuna operazione \(ad eccezione della stampa nella console\).Se il codice postale è costituito da meno di 5 cifre o non rientra nell'intervallo compreso tra 00600 and 99998, la regola `invalidZip` esegue le operazioni seguenti:  
  
        1.  Crea un oggetto `OrderError`, passando a quest’ultimo il codice postale immesso, e imposta le proprietà `ErrorText` e `CustomerName` sull'oggetto.  
  
        2.  Crea un oggetto `invalidZipCodeErrorCollection`.  
  
        3.  Aggiunge l’istanza `OrderError` di recente creazione a `invalidZipCodeErrorCollection` di recente creazione.  
  
         In questa regola viene nuovamente illustrato il supporto per l'operatore `new` che consente di creare un'istanza di oggetti nelle regole.  
  
    -   `displayErrors`  
  
         Questa regola consente di controllare la presenza di eventuali errori aggiunti dalle due regole precedenti nei due oggetti `OrderErrorCollection``invalidItemNumErrorCollection` e `invalidIZipCodeErrorCollection`.Se sono stati rilevati errori \( `invalidItemNumErrorCollection` o `invalidZipCodeErrorCollection` non è `null`\), la regola esegue le operazioni seguenti:  
  
        1.  chiama l'operatore `+` di overload per copiare il contenuto di `invalidItemNumErrorCollection` e `invalidZipCodeErrorCollection` in un'istanza `invalidOrdersCollection``OrderErrorCollection`.  
  
        2.  Chiama il metodo di estensione `PrintOrderErrors` su `invalidOrdersCollection` e restituisce la proprietà `ErrorText` su ogni `orderError` oggetto in `invalidOrdersCollection`.  
  
 L'operatore `+` di overload su `OrderErrorCollection` è definito nella classe `OrderErrorCollection`, nel progetto `OrderErrorLibrary`.Prende due oggetti `OrderErrorCollection` e li combina in un oggetto `OrderErrorCollection`.  
  
 Il metodo di estensione `PrintOrderErrors` è definito anche nel progetto `OrderErrorLibrary`.I metodi di estensione rappresentano una nuova funzionalità C\# che consente agli sviluppatori di aggiungere nuovi metodi al contratto pubblico di un tipo CLR esistente, senza che sia necessario derivarne una classe o ricompilare il tipo originale.  
  
 Quando si esegue l'esempio viene richiesto di immettere un nome, il numero dell'elemento da acquistare e un codice postale.Queste informazioni vengono quindi verificate dalle regole definite nell'attività dei criteri.Di seguito è riportato un esempio di output generato dal programma.  
  
```  
Please enter your name: John  
  
What would you like to purchase?  
        (1) Vista Ultimate DVD  
        (2) Vista Ultimate Upgrade DVD  
        (3) Vista Home Premium DVD  
        (4) Vista Home Premium Upgrade DVD  
        (5) Vista Home Basic DVD  
        (6) Vista Home Basic Upgrade DVD  
  
Please enter an item number: 1  
  
Please enter your 5-Digit zip code: 98102  
  
        Executing Rule: invalidItemNum  
        Executing Rule: invalidZip  
        Executing Rule: displayErrors  
  
                              Thank you for your order, it has been processed.  
  
Workflow Completed  
Another Order? (Y/N): y  
  
Please enter your name: Joel  
  
What would you like to purchase?  
        (1) Vista Ultimate DVD  
        (2) Vista Ultimate Upgrade DVD  
        (3) Vista Home Premium DVD  
        (4) Vista Home Premium Upgrade DVD  
        (5) Vista Home Basic DVD  
        (6) Vista Home Basic Upgrade DVD  
  
Please enter an item number: 8  
  
Please enter your 5-Digit zip code: 0000  
  
        Executing Rule: invalidItemNum  
        Executing Rule: invalidZip  
        Executing Rule: displayErrors  
  
                              Your order contains the following error(s)  
  
Error: No item number found. Please choose an available item.  
Error: Invalid zip code. Please choose a zip code between 00600 and 99998.  
  
Workflow Completed  
Another Order? (Y/N): n  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire il file di progetto OrderProcessingPolicy.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Esistono due progetti diversi nella soluzione: `OrderErrorLibrary` e `OrderProcessingPolicy`.Il progetto `OrderProcessingPolicy` utilizza classi e metodi definiti in `OrderErrorLibrary`.  
  
3.  Compilare tutti i progetti.  
  
4.  Scegliere **Esegui**.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Rules\OrderProcessingPolicy`  
  
## Vedere anche