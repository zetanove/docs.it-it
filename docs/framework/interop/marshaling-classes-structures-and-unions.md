---
title: "Marshaling Classes, Structures, and Unions | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "data marshaling, classes"
  - "marshaling, unions"
  - "marshaling, structures"
  - "marshaling, samples"
  - "data marshaling, structures"
  - "platform invoke, marshaling data"
  - "marshaling, classes"
  - "data marshaling, unions"
  - "data marshaling, samples"
  - "data marshaling, platform invoke"
  - "marshaling, platform invoke"
ms.assetid: 027832a2-9b43-4fd9-9b45-7f4196261a4e
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Marshaling Classes, Structures, and Unions
In .NET Framework classi e strutture sono simili.  Entrambe possono avere campi, proprietà ed eventi  nonché metodi statici e non statici.  Una differenza fondamentale è data dal fatto che le strutture sono tipi di valore e le classi sono tipi di riferimento.  
  
 Nella tabella seguente sono elencate le opzioni di marshalling per le classi, le strutture e le unioni con la descrizione dell'utilizzo e un collegamento all'esempio corrispondente di platform invoke.  
  
|Tipo|Descrizione|Esempio|  
|----------|-----------------|-------------|  
|Classe per valore.|Passa una classe con membri Integer come parametro in\/out, come il case gestito.|SysTime \(esempio\)|  
|Struttura per valore.|Passa le strutture come parametri in.|Structures \(esempio\)|  
|Struttura per riferimento.|Passa le strutture come parametri in\/out.|OSInfo \(esempio\)|  
|Struttura con strutture annidate \(semplificata\).|Passa una classe che rappresenta una struttura con strutture annidate nella funzione non gestita.  La struttura viene semplificata in una sola grande struttura nel prototipo gestito.|FindFile \(esempio\)|  
|Struttura con puntatore a un'altra struttura.|Passa una struttura che contiene un puntatore a una seconda struttura come membro.|Structures \(esempio\)|  
|Matrice di strutture con Integer per valore.|Passa una matrice di strutture che contengono solo Integer come un parametro in\/out.  È possibile modificare i membri della matrice.|Arrays \(esempio\)|  
|Matrice di strutture con Integer e stringhe per riferimento.|Passa una matrice di strutture che contengono Integer e stringhe come un parametro out.  La memoria per la matrice viene allocata dalla funzione chiamata.|OutArrayOfStructs \(esempio\)|  
|Unioni con tipi di valore.|Passa le unioni con tipi di valore \(Integer e Double\).|Unions \(esempio\)|  
|Unioni con tipi misti.|Passa unioni con tipi misti \(Integer e String\).|Unions \(esempio\)|  
|Valori null nella struttura.|Passa un riferimento null \(**Nothing** in Visual Basic\) invece di un riferimento a un tipo di valore.|HandleRef \(esempio\)|  
  
## Structures \(esempio\)  
 In questo esempio viene dimostrato come passare una struttura che punta a una seconda struttura, una struttura con una struttura incorporata e una struttura con una matrice incorporata.  
  
 Nell'esempio di strutture vengono usate le seguenti funzioni non gestite, illustrate con le dichiarazioni di funzione originali:  
  
-   **TestStructInStruct** esportata da PinvokeLib.dll.  
  
    ```  
    int TestStructInStruct(MYPERSON2* pPerson2);  
    ```  
  
-   **TestStructInStruct3** esportata da PinvokeLib.dll.  
  
    ```  
    void TestStructInStruct3(MYPERSON3 person3);  
    ```  
  
-   **TestArrayInStruct** esportata da PinvokeLib.dll.  
  
    ```  
    void TestArrayInStruct( MYARRAYSTRUCT* pStruct );  
    ```  
  
 [PinvokeLib](http://msdn.microsoft.com/it-it/5d1438d7-9946-489d-8ede-6c694a08f614) è una libreria non gestita personalizzata contenente implementazioni per le funzioni elencate in precedenza e quattro strutture, ovvero: **MYPERSON**, **MYPERSON2**, **MYPERSON3** e **MYARRAYSTRUCT**.  Le strutture contengono gli elementi seguenti:  
  
```  
typedef struct _MYPERSON  
{  
   char* first;   
   char* last;   
} MYPERSON, *LP_MYPERSON;  
  
typedef struct _MYPERSON2  
{  
   MYPERSON* person;  
   int age;   
} MYPERSON2, *LP_MYPERSON2;  
  
typedef struct _MYPERSON3  
{  
   MYPERSON person;  
   int age;   
} MYPERSON3;  
  
typedef struct _MYARRAYSTRUCT  
{  
   bool flag;  
   int vals[ 3 ];   
} MYARRAYSTRUCT;  
```  
  
 Le strutture gestite `MyPerson`, `MyPerson2`, `MyPerson3` e `MyArrayStruct` hanno le caratteristiche seguenti:  
  
-   `MyPerson` contiene solo membri stringa.  Le stringhe vengono impostate sul formato ANSI dal campo [CharSet](../../../docs/framework/interop/specifying-a-character-set.md), quando viene passato alla funzione non gestita.  
  
-   `MyPerson2` contiene un tipo **IntPtr** alla struttura `MyPerson`.  Il tipo **IntPtr** sostituisce il puntatore originale alla struttura non gestita poiché nelle applicazioni .NET Framework non vengono usati i puntatori a meno che il codice non sia contrassegnato come **unsafe**.  
  
-   `MyPerson3` contiene `MyPerson` come struttura incorporata.  È possibile semplificare una struttura incorporata in un'altra struttura posizionandone gli elementi direttamente nella struttura principale oppure mantenerla incorporata, come accade in questo esempio.  
  
-   `MyArrayStruct` contiene una matrice di Integer.  Il valore dell'enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> viene impostato dall'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> su **ByValArray**, che consente di indicare il numero di elementi nella matrice.  
  
 Per tutte le strutture di questo esempio, l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> viene applicato in modo che i membri vengano disposti in sequenza nella memoria, nell'ordine in cui appaiono.  
  
 La classe `LibWrap` contiene prototipi gestiti per i metodi `TestStructInStruct`, `TestStructInStruct3` e `TestArrayInStruct` chiamati dalla classe `App`.  Ciascun prototipo dichiara un singolo parametro, come indicato di seguito:  
  
-   `TestStructInStruct` dichiara un riferimento al tipo `MyPerson2` come parametro.  
  
-   `TestStructInStruct3` dichiara il tipo `MyPerson3` come parametro e passa il parametro per valore.  
  
-   `TestArrayInStruct` dichiara un riferimento al tipo `MyArrayStruct` come parametro.  
  
 Come argomenti per i metodi, le strutture vengono passate per valore a meno che il parametro non contenga la parola chiave **ref** \(**ByRef** in Visual Basic\).  Ad esempio, il metodo `TestStructInStruct` passa un riferimento, ossia il valore di un indirizzo, a un oggetto di tipo `MyPerson2` al codice non gestito.  Per modificare la struttura alla quale punta `MyPerson2`, nell'esempio viene creato un buffer di dimensioni specificate e ne viene restituito l'indirizzo combinando i metodi <xref:System.Runtime.InteropServices.Marshal.AllocCoTaskMem%2A?displayProperty=fullName> e <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=fullName>.  In seguito, il contenuto della struttura gestita viene copiato nel buffer non gestito.  Infine, il metodo <xref:System.Runtime.InteropServices.Marshal.PtrToStructure%2A?displayProperty=fullName> viene usato per effettuare il marshalling dei dati dal buffer non gestito in un oggetto gestito, mentre il metodo <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A?displayProperty=fullName> viene usato per liberare il blocco di memoria non gestito.  
  
### Dichiarazione dei prototipi  
 [!code-cpp[Conceptual.Interop.Marshaling#23](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/structures.cpp#23)]
 [!code-csharp[Conceptual.Interop.Marshaling#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/structures.cs#23)]
 [!code-vb[Conceptual.Interop.Marshaling#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/structures.vb#23)]  
  
### Chiamata delle funzioni  
 [!code-cpp[Conceptual.Interop.Marshaling#24](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/structures.cpp#24)]
 [!code-csharp[Conceptual.Interop.Marshaling#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/structures.cs#24)]
 [!code-vb[Conceptual.Interop.Marshaling#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/structures.vb#24)]  
  
## FindFile \(esempio\)  
 In questo esempio viene illustrato come passare una struttura che contiene una seconda struttura incorporata a una funzione non gestita.  Viene inoltre illustrato come usare l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> per dichiarare una matrice a lunghezza fissa all'interno della struttura.  Nell'esempio gli elementi della struttura incorporata vengono aggiunti alla struttura padre.  Per un esempio di struttura incorporata non semplificata, vedere [Esempio di strutture](http://msdn.microsoft.com/it-it/96a62265-dcf9-4608-bc0a-1f762ab9f48e).  
  
 Nell'esempio FindFile viene usata la seguente funzione non gestita, illustrata con la relativa dichiarazione di funzione originale:  
  
-   **FindFirstFile** esportata da Kernel32.dll.  
  
    ```  
    HANDLE FindFirstFile(LPCTSTR lpFileName, LPWIN32_FIND_DATA lpFindFileData);  
    ```  
  
 La struttura originale passata alla funzione contiene gli elementi seguenti:  
  
```  
typedef struct _WIN32_FIND_DATA   
{  
  DWORD    dwFileAttributes;   
  FILETIME ftCreationTime;   
  FILETIME ftLastAccessTime;   
  FILETIME ftLastWriteTime;   
  DWORD    nFileSizeHigh;   
  DWORD    nFileSizeLow;   
  DWORD    dwReserved0;   
  DWORD    dwReserved1;   
  TCHAR    cFileName[ MAX_PATH ];   
  TCHAR    cAlternateFileName[ 14 ];   
} WIN32_FIND_DATA, *PWIN32_FIND_DATA;  
```  
  
 In questo esempio, la classe `FindData` contiene un membro dati corrispondente per ogni elemento della struttura originale e della struttura incorporata.  Al posto di due buffer di caratteri originali, la classe usa delle stringhe.  **MarshalAsAttribute** imposta l'enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> su **ByValTStr**, che consente di identificare le matrici di caratteri inline a lunghezza fissa visualizzate all'interno delle strutture non gestite.  
  
 La classe `LibWrap` contiene un prototipo gestito del metodo `FindFirstFile`, che passa la classe `FindData` come parametro.  Il parametro deve essere dichiarato con gli attributi <xref:System.Runtime.InteropServices.InAttribute> e <xref:System.Runtime.InteropServices.OutAttribute> perché le classi, che sono tipi di riferimento, per impostazione predefinita vengono passate come parametri in.  
  
### Dichiarazione dei prototipi  
 [!code-cpp[Conceptual.Interop.Marshaling#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/findfile.cpp#17)]
 [!code-csharp[Conceptual.Interop.Marshaling#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/findfile.cs#17)]
 [!code-vb[Conceptual.Interop.Marshaling#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/findfile.vb#17)]  
  
### Chiamata delle funzioni  
 [!code-cpp[Conceptual.Interop.Marshaling#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/findfile.cpp#18)]
 [!code-csharp[Conceptual.Interop.Marshaling#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/findfile.cs#18)]
 [!code-vb[Conceptual.Interop.Marshaling#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/findfile.vb#18)]  
  
## Unions \(esempio\)  
 In questo esempio viene dimostrato come passare le strutture contenenti solo tipi di valore e le strutture contenenti un tipo di valore e una stringa come parametri a una funzione non gestita per la quale è prevista un'unione.  Un'unione rappresenta un percorso di memoria che può essere condiviso da due o più variabili.  
  
 Nell'esempio di unioni viene usata la seguente funzione non gestita, illustrata con la dichiarazione di funzione originale:  
  
-   **TestUnion** esportata da PinvokeLib.dll.  
  
    ```  
    void TestUnion(MYUNION u, int type);  
    ```  
  
 [PinvokeLib.dll](http://msdn.microsoft.com/it-it/5d1438d7-9946-489d-8ede-6c694a08f614) è una libreria non gestita personalizzata contenente un'implementazione per la funzione elencata in precedenza e due unioni, **MYUNION** e **MYUNION2**.  Le unioni contengono i seguenti elementi:  
  
```  
union MYUNION  
{  
    int number;  
    double d;  
}  
  
union MYUNION2  
{  
    int i;  
    char str[128];  
};  
```  
  
 Nel codice gestito, le unioni sono definite come strutture.   La struttura `MyUnion` contiene due tipi di valore come membri, ovvero un Integer e un Double.  L'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> è impostato in modo da controllare l'esatta posizione di ciascun membro dati.  L'attributo <xref:System.Runtime.InteropServices.FieldOffsetAttribute> fornisce la posizione fisica dei campi all'interno della rappresentazione non gestita di un'unione.  Poiché entrambi hanno gli stessi valori di offset, i membri possono definire la stessa porzione di memoria.  
  
 `MyUnion2_1` e `MyUnion2_2` contengono rispettivamente un tipo di valore \(Integer\) e una stringa.  Nel codice gestito i tipi di valore e quelli di riferimento non possono sovrapporsi.  In questo esempio l'overload dei metodi consente al chiamante di usare entrambi i tipi nella chiamata alla stessa funzione non gestita.  Il layout di `MyUnion2_1` è esplicito e ha un valore di offset preciso.  Al contrario, `MyUnion2_2` ha un layout sequenziale, poiché i layout espliciti non sono consentiti con i tipi di riferimento.  L'enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> viene impostata dall'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> su **ByValTStr**, che consente di identificare le matrici di caratteri inline a lunghezza fissa presenti nella rappresentazione non gestita dell'unione.  
  
 La classe `LibWrap` contiene i prototipi per i metodi `TestUnion` e `TestUnion2`.  `TestUnion2` viene sottoposto a overload allo scopo di dichiarare `MyUnion2_1` o `MyUnion2_2` come parametri.  
  
### Dichiarazione dei prototipi  
 [!code-cpp[Conceptual.Interop.Marshaling#28](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/unions.cpp#28)]
 [!code-csharp[Conceptual.Interop.Marshaling#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/unions.cs#28)]
 [!code-vb[Conceptual.Interop.Marshaling#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/unions.vb#28)]  
  
### Chiamata delle funzioni  
 [!code-cpp[Conceptual.Interop.Marshaling#29](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/unions.cpp#29)]
 [!code-csharp[Conceptual.Interop.Marshaling#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/unions.cs#29)]
 [!code-vb[Conceptual.Interop.Marshaling#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/unions.vb#29)]  
  
## SysTime \(esempio\)  
 In questo esempio viene dimostrato come passare un puntatore a una classe a una funzione non gestita per la quale è previsto un puntatore a una struttura.  
  
 Nell'esempio SysTime viene usata la seguente funzione non gestita, illustrata con la dichiarazione di funzione originale:  
  
-   **GetSystemTime** esportata da Kernel32.dll.  
  
    ```  
    VOID GetSystemTime(LPSYSTEMTIME lpSystemTime);  
    ```  
  
 La struttura originale passata alla funzione contiene gli elementi seguenti:  
  
```  
typedef struct _SYSTEMTIME {   
    WORD wYear;   
    WORD wMonth;   
    WORD wDayOfWeek;   
    WORD wDay;   
    WORD wHour;   
    WORD wMinute;   
    WORD wSecond;   
    WORD wMilliseconds;   
} SYSTEMTIME, *PSYSTEMTIME;  
```  
  
 In questo esempio la classe `SystemTime` contiene gli elementi della struttura originale rappresentati come membri di classe.  L'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> è impostato in modo da garantire che i membri vengano inseriti in memoria in sequenza, nell'ordine in cui appaiono.  
  
 La classe `LibWrap` contiene un prototipo gestito del metodo `GetSystemTime`, che passa la classe `SystemTime` come parametro in\/out per impostazione predefinita.  Il parametro deve essere dichiarato con gli attributi <xref:System.Runtime.InteropServices.InAttribute> e <xref:System.Runtime.InteropServices.OutAttribute> perché le classi, che sono tipi di riferimento, per impostazione predefinita vengono passate come parametri in.  Affinché il chiamante riceva i risultati, è necessario applicare questi [attributi direzionali](http://msdn.microsoft.com/it-it/241ac5b5-928e-4969-8f58-1dbc048f9ea2) in modo esplicito.  Con la classe `App` si crea una nuova istanza della classe `SystemTime` e si accede ai relativi campi di dati.  
  
### Esempi di codice  
 [!code-cpp[Conceptual.Interop.Marshaling#25](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/systime.cpp#25)]
 [!code-csharp[Conceptual.Interop.Marshaling#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/systime.cs#25)]
 [!code-vb[Conceptual.Interop.Marshaling#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/systime.vb#25)]  
  
## OutArrayOfStructs \(esempio\)  
 In questo esempio viene illustrato come passare una matrice di strutture che contiene Integer e stringhe come parametri out a una funzione non gestita.  
  
 L'esempio dimostra come chiamare una funzione nativa usando la classe <xref:System.Runtime.InteropServices.Marshal> e usando codice di tipo unsafe.  
  
 Nell'esempio vengono usate funzioni wrapper e operazioni platform invoke definite in [PinvokeLib.dll](http://msdn.microsoft.com/it-it/5d1438d7-9946-489d-8ede-6c694a08f614), anche fornite anche nei file di origine.  Vengono usate la funzione `TestOutArrayOfStructs` e la struttura `MYSTRSTRUCT2`.  La struttura contiene gli elementi seguenti:  
  
```  
typedef struct _MYSTRSTRUCT2  
{  
   char* buffer;  
   UINT size;   
} MYSTRSTRUCT2;  
```  
  
 La classe `MyStruct` contiene un oggetto stringa di caratteri ANSI.  Il campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> specifica il formato ANSI.  `MyUnsafeStruct` è una struttura contenente un tipo <xref:System.IntPtr> anziché una stringa.  
  
 La classe `LibWrap` contiene il metodo prototipo `TestOutArrayOfStructs` di overload.  Se un metodo dichiara un puntatore come parametro, la classe deve essere contrassegnata con la parola chiave `unsafe`.  Poiché [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] non può usare codice unsafe, il metodo di overload, il modificatore unsafe e la struttura `MyUnsafeStruct` non sono necessari.  
  
 La `App` classe implementa il metodo `UsingMarshaling` che esegue tutte le attività necessarie per passare la matrice.  La matrice è contrassegnata con la parola chiave `out` \(`ByRef` in Visual Basic\) per indicare che i dati passano dal chiamato al chiamante.  L'implementazione usa i seguenti metodi della classe <xref:System.Runtime.InteropServices.Marshal>:  
  
-   <xref:System.Runtime.InteropServices.Marshal.PtrToStructure%2A> per il marshalling dei dati dal buffer non gestito a un oggetto gestito.  
  
-   <xref:System.Runtime.InteropServices.Marshal.DestroyStructure%2A> per rilasciare la memoria riservata alle stringhe nella struttura.  
  
-   <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> per rilasciare la memoria riservata alla matrice.  
  
 Come accennato in precedenza, C\# consente il codice unsafe, mentre [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] non lo consente.  Nell'esempio C\#, `UsingUnsafePointer` è un'implementazione alternativa del metodo che usa puntatori anziché la classe <xref:System.Runtime.InteropServices.Marshal> per passare nuovamente la matrice che contiene la struttura `MyUnsafeStruct`.  
  
### Dichiarazione dei prototipi  
 [!code-cpp[Conceptual.Interop.Marshaling#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/outarrayofstructs.cpp#20)]
 [!code-csharp[Conceptual.Interop.Marshaling#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/outarrayofstructs.cs#20)]
 [!code-vb[Conceptual.Interop.Marshaling#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/outarrayofstructs.vb#20)]  
  
### Chiamata delle funzioni  
 [!code-cpp[Conceptual.Interop.Marshaling#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/outarrayofstructs.cpp#21)]
 [!code-csharp[Conceptual.Interop.Marshaling#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/outarrayofstructs.cs#21)]
 [!code-vb[Conceptual.Interop.Marshaling#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/outarrayofstructs.vb#21)]  
  
## Vedere anche  
 [Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)   
 [Platform Invoke Data Types](http://msdn.microsoft.com/it-it/16014d9f-d6bd-481e-83f0-df11377c550f)   
 [Marshaling Strings](../../../docs/framework/interop/marshaling-strings.md)   
 [Marshaling Arrays of Types](http://msdn.microsoft.com/it-it/049b1c1b-228f-4445-88ec-91bc7fd4b1e8)