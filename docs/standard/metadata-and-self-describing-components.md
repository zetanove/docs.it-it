---
title: "Metadati e componenti auto-descrittivi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Common Language Runtime, metadati"
  - "componenti [.NET Framework], metadati"
  - "linguaggi, interoperabilità"
  - "metadati, informazioni sui metadati"
  - "file PE, metadati"
  - "file eseguibili portabili, metadati"
  - "runtime, metadati"
  - "file autodescrittivi"
ms.assetid: 3dd13c5d-a508-455b-8dce-0a852882a5a7
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Metadati e componenti auto-descrittivi
In passato, un componente software \(EXE o DLL\) scritto in un linguaggio non poteva usare facilmente un componente software scritto in un linguaggio diverso.  Il sistema COM ha costituito un passo in avanti nella soluzione di questo problema.  Oggi .NET Framework rende l'interazione tra i componenti ancora più semplice consentendo ai compilatori di inserire informazioni dichiarative aggiuntive in tutti i moduli e in tutti gli assembly.  Queste informazioni, note come metadati, semplificano l'interazione tra i componenti.  
  
 I metadati sono informazioni binarie che descrivono un programma e vengono memorizzate in un file eseguibile portabile \(PE, Portable Executable\) di Common Language Runtime o in memoria.  Quando si compila il proprio codice in un file PE, i metadati vengono inseriti in una parte del file e il codice viene convertito in Microsoft Intermediate Language \(MSIL\) e inserito in un'altra parte del file.  Ogni tipo e membro definito e a cui si fa riferimento in un modulo o in un assembly è descritto nei metadati.  Quando il codice viene eseguito, il runtime carica i metadati in memoria e vi fa riferimento per ottenere informazioni sulle classi usate nel codice, come pure su membri, ereditarietà e così via.  
  
 I metadati consentono di descrivere ciascun tipo e membro definito nel codice in modo indipendente dal linguaggio.  I metadati archiviano le seguenti informazioni:  
  
-   Descrizione dell'assembly.  
  
    -   Identità \(nome, versione, impostazioni cultura, chiave pubblica\).  
  
    -   Tipi esportati.  
  
    -   Altri assembly da cui questo assembly dipende.  
  
    -   Autorizzazioni di sicurezza necessarie per l'esecuzione.  
  
-   Descrizione di tipi.  
  
    -   Nome, visibilità, classe di base e interfacce implementate.  
  
    -   Membri \(metodi, campi, proprietà, eventi e tipi annidati\).  
  
-   Attributi.  
  
    -   Elementi descrittivi aggiuntivi che modificano tipi e membri.  
  
## Vantaggi offerti dai metadati  
 I metadati costituiscono la chiave di un modello di programmazione più semplice ed eliminano la necessità di file del linguaggio di definizione dell'interfaccia \(IDL, Interface Definition Language\), di file di intestazione o di qualsiasi altro metodo esterno di riferimento ai componenti.  I metadati consentono ai linguaggi .NET Framework di descrivere se stessi automaticamente e in modo indipendente dal linguaggio, in modo trasparente sia per lo sviluppatore che per l'utente.  Le capacità dei metadati possono inoltre essere estese con l'uso degli attributi.  I metadati offrono i seguenti vantaggi principali:  
  
-   File autodescrittivi.  
  
     I moduli e gli assembly di Common Language Runtime sono autodescrittivi.  I metadati di un modulo contengono tutto il necessario per interagire con un altro modulo.  I metadati forniscono automaticamente le funzionalità di IDL in COM, consentendo di usare un solo file sia per la definizione che per l'implementazione.  Moduli e assembly di runtime non richiedono la registrazione presso il sistema operativo.  Pertanto, le descrizioni usate dal runtime rispecchiano sempre il codice effettivamente presente nel file compilato, incrementando così l'affidabilità dell'applicazione.  
  
-   Interoperabilità dei linguaggi e progettazione basata su componenti semplificata.  
  
     I metadati forniscono tutte le informazioni relative al codice compilato che occorrono per ereditare una classe da un file PE scritto in un linguaggio diverso.  È possibile creare un'istanza di una classe scritta in uno dei linguaggi gestiti \(qualsiasi linguaggio che si avvale di Common Language Runtime\) senza preoccuparsi del marshalling esplicito e senza usare codice di interoperabilità personalizzato.  
  
-   Attributi.  
  
     .NET Framework consente di dichiarare tipi specifici di metadati, detti attributi, nel proprio file compilato.  Gli attributi sono disponibili nell'intero contesto di .NET Framework e vengono usati per controllare in maggior dettaglio come si comporta il proprio programma in fase di esecuzione.  È anche possibile inserire i propri metadati personalizzati nei file di .NET Framework tramite attributi personalizzati definiti dall'utente.  Per altre informazioni, vedere [Attributi](../../docs/standard/attributes/index.md)  
  
## I metadati e la struttura dei file PE  
 I metadati vengono memorizzati in una sezione di un file eseguibile portabile \(PE, Portable Executable\) .NET Framework, mentre il codice Microsoft Intermediate Language \(MSIL\) viene memorizzato in una diversa sezione dello stesso file.  La parte del file che ospita i metadati contiene una serie di tabelle e di strutture di dati dell'heap.  La parte MSIL contiene codice MSIL e token di metadati che fanno riferimento alla parte del file PE che ospita i metadati.  I token dei metadati vengono usati, ad esempio, con strumenti come il [disassemblatore MSIL \(Ildasm.exe\)](../../docs/framework/tools/ildasm-exe-il-disassembler.md), che consente di visualizzare il proprio codice MSIL.  
  
### Tabelle e heap dei metadati  
 Ogni tabella dei metadati contiene informazioni sugli elementi di un programma.  Ad esempio, una tabella dei metadati descrive le classi presenti nel codice, un'altra tabella descrive i campi e così via.  Se il codice contiene dieci classi, la tabella delle classi sarà costituita da dieci righe, una per ogni classe.  Le tabelle dei metadati fanno riferimento ad altre tabelle e agli heap.  La tabella dei metadati che elenca le classi contiene ad esempio riferimenti alla tabella che elenca i metodi.  
  
 I metadati memorizzano informazioni anche in quattro strutture heap: stringhe, blob, stringhe utente e GUID.  Tutte le stringhe usate per denominare i tipi e i membri sono memorizzate nell'heap delle stringhe.  La tabella dei metodi, ad esempio, non memorizza il nome dei metodi direttamente, ma punta al nome del metodo memorizzato nell'heap delle stringhe.  
  
### Token di metadati  
 Ciascuna riga di ciascuna tabella dei metadati è identificata in modo univoco nella parte MSIL del file PE da un token di metadati.  I token di metadati sono concettualmente simili a puntatori, memorizzati in MSIL, che fanno riferimento a una determinata tabella dei metadati.  
  
 Un token di metadati è un numero a quattro byte.  Il byte più significativo indica la tabella dei metadati a cui il token fa riferimento \(metodi, tipi e così via\).  I rimanenti tre byte individuano la riga della tabella dei metadati che corrisponde all'elemento di programmazione che si sta descrivendo.  Se si definisce un metodo in C\# e lo si compila in un file PE, si potrà trovare il seguente token di metadati nella parte MSIL del file PE:  
  
```  
0x06000004  
```  
  
 Il byte più significativo \(`0x06`\) indica che si tratta di un token **MethodDef**.  I tre byte meno significativi \(`000004`\) indicano a Common Language Runtime di cercare le informazioni che descrivono la definizione di questo metodo nella quarta riga della tabella **MethodDef**.  
  
### Metadati all'interno di un file PE  
 Quando un programma viene compilato per Common Language Runtime, viene convertito in un file PE, costituito da tre parti.  Nella tabella che segue viene descritto il contenuto di ciascuna parte.  
  
|Sezione del PE|Contenuto|  
|--------------------|---------------|  
|Intestazione del PE|L'indice delle sezioni principali del file PE e l'indirizzo del punto di ingresso.<br /><br /> Il runtime usa queste informazioni per identificare il file come file PE e per determinare da che punto iniziare l'esecuzione quando carica il programma in memoria.|  
|Istruzioni MSIL|Le istruzioni MSIL che costituiscono il codice.  Molte istruzioni MSIL sono accompagnate da token di metadati.|  
|Metadati|Le tabelle e gli heap dei metadati.  Il runtime usa questa sezione per memorizzare informazioni sui tutti i tipi e i membri presenti nel codice.  Questa sezione include anche attributi personalizzati e informazioni sulla sicurezza.|  
  
## Utilizzo dei metadati in fase di esecuzione  
 Per meglio comprendere i metadati e il ruolo che essi rivestono in Common Language Runtime, può essere utile creare un piccolo programma e illustrare come i metadati ne influenzino l'esecuzione.  Nell'esempio di codice che segue vengono mostrati due metodi all'interno di una classe denominata `MyApp`.  Il metodo `Main` è il punto di ingresso del programma, mentre il metodo `Add` restituisce semplicemente la somma di due argomenti Integer.  
  
```vb  
Public Class MyApp  
   Public Shared Sub Main()  
      Dim ValueOne As Integer = 10  
      Dim ValueTwo As Integer = 20  
      Console.WriteLine("The Value is: {0}", Add(ValueOne, ValueTwo))  
   End Sub  
  
   Public Shared Function Add(One As Integer, Two As Integer) As Integer  
      Return (One + Two)  
   End Function  
End Class  
```  
  
```csharp  
using System;    
public class MyApp  
{  
   public static int Main()  
   {  
      int ValueOne = 10;  
      int ValueTwo = 20;           
      Console.WriteLine("The Value is: {0}", Add(ValueOne, ValueTwo));  
      return 0;  
   }  
   public static int Add(int One, int Two)  
   {  
      return (One + Two);  
   }  
}  
```  
  
 Durante l'esecuzione del codice, il runtime carica il modulo in memoria e cerca questa classe nei metadati.  Dopo il caricamento, il runtime compie un'analisi approfondita del flusso Microsoft Intermediate Language \(MSIL\) del metodo per convertirlo in veloci istruzioni macchina native.  Il runtime consente di usare un compilatore JIT \(Just\-In\-Time\) per convertire le istruzioni MSIL in codice macchina nativo, procedendo un metodo alla volta, in base alle necessità.  
  
 Nell'esempio che segue viene illustrata parte del codice MSIL prodotto dalla funzione `Main` del codice precedente.  È possibile vedere il codice MSIL e i metadati di qualsiasi applicazione .NET Framework usando [MSIL Disassembler \(Ildasm.exe\)](../../docs/framework/tools/ildasm-exe-il-disassembler.md).  
  
```  
.entrypoint  
.maxstack  3  
.locals ([0] int32 ValueOne,  
         [1] int32 ValueTwo,  
         [2] int32 V_2,  
         [3] int32 V_3)  
IL_0000:  ldc.i4.s   10  
IL_0002:  stloc.0  
IL_0003:  ldc.i4.s   20  
IL_0005:  stloc.1  
IL_0006:  ldstr      "The Value is: {0}"  
IL_000b:  ldloc.0  
IL_000c:  ldloc.1  
IL_000d:  call int32 ConsoleApplication.MyApp::Add(int32,int32) /* 06000003 */  
```  
  
 Il compilatore JIT legge il codice MSIL dell'intero metodo, lo analizza approfonditamente, quindi genera efficienti istruzioni native corrispondenti.  All'istruzione `IL_000d` il runtime incontra un token di metadati che punta al metodo `Add` \(`/*` `06000003 */`\); il token viene usato per consultare la terza riga della tabella **MethodDef**.  
  
 Nella tabella che segue viene illustrata la parte di **MethodDef** a cui fa riferimento il token di metadati che descrive il metodo `Add`.  Benché questo assembly includa altre tabelle di metadati, ciascuna con i propri valori univoci, viene qui discussa solo questa tabella.  
  
|Riga|RVA \(Relative Virtual Address\)|ImplFlags|Flag|Nome<br /><br /> \(punta all'heap delle stringhe\)|Firma \(punta all'heap dei blob\)|  
|----------|--------------------------------------|---------------|----------|------------------------------------------------|---------------------------------------|  
|1|0x00002050|IL<br /><br /> Gestito|Public<br /><br /> ReuseSlot<br /><br /> SpecialName<br /><br /> RTSpecialName<br /><br /> .ctor|.ctor \(costruttore\)||  
|2|0x00002058|IL<br /><br /> Gestito|Public<br /><br /> Statico<br /><br /> ReuseSlot|Main|Stringa|  
|3|0x0000208c|IL<br /><br /> Gestito|Public<br /><br /> Statico<br /><br /> ReuseSlot|Aggiungi|int, int, int|  
  
 Ogni colonna della tabella contiene importanti informazioni sul codice.  La colonna **RVA**consente al runtime di calcolare l'indirizzo di memoria iniziale del codice MSIL che definisce questo metodo.  Le colonne **ImplFlags** e **Flag** contengono maschere di bit che descrivono il metodo \(indicano ad esempio se il metodo è pubblico o privato\).  La colonna **Nome** indicizza il nome del metodo nell'heap delle stringhe.  La colonna **Firma** indicizza la definizione della firma del metodo nell'heap dei blob.  
  
 Il runtime calcola l'indirizzo di offset desiderato dalla colonna **RVA** nella terza riga e restituisce tale indirizzo al compilatore JIT, che quindi procede con il nuovo indirizzo.  Il compilatore JIT continua a processare il codice MSIL al nuovo indirizzo fino a quando incontra un altro token di metadati e il processo si ripete.  
  
 Grazie ai metadati, il runtime ha accesso a tutte le informazioni necessarie per caricare il codice e convertirlo in istruzioni macchina native.  In questo modo, i metadati consentono l'esistenza dei file autodescrittivi e, unitamente al sistema di tipi comune, l'ereditarietà tra linguaggi diversi.  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Attributi](../../docs/standard/attributes/index.md)|Viene descritto come applicare attributi, scrivere attributi personalizzati e recuperare le informazioni archiviate negli attributi.|