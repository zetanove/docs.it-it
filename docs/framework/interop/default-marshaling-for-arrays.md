---
title: "Default Marshaling for Arrays | Microsoft Docs"
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
  - "interop marshaling, arrays"
  - "arrays, interop marshaling"
ms.assetid: 8a3cca8b-dd94-4e3d-ad9a-9ee7590654bc
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Default Marshaling for Arrays
In un'applicazione interamente costituita da codice gestito, i tipi di matrice sono passati come parametri In\/Out da Common Language Runtime.  Al contrario, per impostazione predefinita, una matrice viene passata come parametro In dal gestore di marshalling di interoperabilità.  
  
 Con l'[ottimizzazione del blocco](../../../docs/framework/interop/copying-and-pinning.md), può sembrare che una matrice copiabile funzioni come parametro In\/Out quando interagisce con gli oggetti nello stesso apartment.  Tuttavia, se il codice viene successivamente esportato in una libreria dei tipi utilizzata per generare il proxy su più computer e la libreria è utilizzata per eseguire il marshalling delle chiamate su più apartment, è possibile che le chiamate ripristinino l'impostazione del parametro In su true.  
  
 Le matrici hanno una natura complessa e le distinzioni tra matrici gestite e non gestite garantiscono più informazioni rispetto ad altri tipi non copiabili.  In questo argomento vengono fornite le seguenti informazioni sul marshalling delle matrici:  
  
-   [Matrici gestite](#cpcondefaultmarshalingforarraysanchor1)  
  
-   [Matrici non gestite](#cpcondefaultmarshalingforarraysanchor2)  
  
-   [Passaggio di parametri di matrice al codice .NET](#cpcondefaultmarshalingforarraysanchor3)  
  
-   [Passaggio di matrici a COM](#cpcondefaultmarshalingforarraysanchor4)  
  
<a name="cpcondefaultmarshalingforarraysanchor1"></a>   
## Matrici gestite  
 I tipi di matrici gestite possono variare, ma <xref:System.Array?displayProperty=fullName> rimane comunque la classe base di tutti i tipi di matrice.  La classe **System.Array** ha le proprietà per la determinazione del numero di dimensioni, della lunghezza e del limite superiore e inferiore di una matrice, nonché i metodi per accedere, ordinare, cercare, copiare e creare le matrici.  
  
 Questi tipi di matrice sono dinamici e non hanno un tipo statico corrispondente definito nella libreria della classe base.  È utile pensare a ogni combinazione di numero di dimensioni e tipo di elemento come a un tipo distinto di matrice.  Una matrice unidimensionale di interi appartiene quindi a un tipo diverso rispetto a una matrice unidimensionale di tipi double.  Allo stesso modo, una matrice bidimensionale di interi è diversa da una unidimensionale con lo stesso tipo di valori.  I limiti della matrice non sono considerati nel confronto di tipi.  
  
 Come illustrato nella tabella riportata di seguito, qualsiasi istanza di matrice gestita deve avere un determinato numero di dimensioni, limite inferiore e tipo di elemento.  
  
|Tipo di matrice gestito|Tipo di elemento|Classifica|Limite inferiore|Notazione della firma|  
|-----------------------------|----------------------|----------------|----------------------|---------------------------|  
|**ELEMENT\_TYPE\_ARRAY**|Specificato mediante il tipo.|Specificato mediante il numero di dimensioni.|Specificato in modo facoltativo mediante i limiti.|*tipo* **\[** *n*,*m* **\]**|  
|**ELEMENT\_TYPE\_CLASS**|Sconosciuto|Sconosciuto|Sconosciuto|**System.Array**|  
|**ELEMENT\_TYPE\_SZARRAY**|Specificato mediante il tipo.|1|0|*tipo* **\[** *n* **\]**|  
  
<a name="cpcondefaultmarshalingforarraysanchor2"></a>   
## Matrici non gestite  
 Le matrici non gestite sono matrici protette di tipo COM o di tipo C con lunghezza fissa o variabile.  Le matrici protette sono autodescrittive e contengono il tipo, il numero di dimensioni e i limiti dei dati di matrice associati.  Le matrici di tipo C sono matrici unidimensionali tipizzate con un limite inferiore fisso di 0.  Il servizio di marshalling offre supporto limitato per entrambi i tipi di matrici.  
  
<a name="cpcondefaultmarshalingforarraysanchor3"></a>   
## Passaggio di parametri di matrice al codice .NET  
 Sia le matrici di tipo C che quelle protette possono essere passate al codice .NET dal codice non gestito come matrice protetta o matrice di tipo C.  Nella tabella che segue vengono indicati il tipo non gestito e il corrispondente tipo importato.  
  
|Tipo non gestito|Tipo importato|  
|----------------------|--------------------|  
|**SafeArray\(** *Tipo* **\)**|**ELEMENT\_TYPE\_SZARRAY** **\<** *ConvertedType* **\>**<br /><br /> Numero di dimensioni \= 1, limite inferiore \= 0.  Il numero di dimensioni è noto solo se viene fornito nella firma gestita.  Per le matrici protette che non hanno numero di dimensioni \= 1 o limite inferiore \= 0 non è possibile eseguire il marshalling come **SZARRAY**.|  
|*Tipo*  **\[\]**|**ELEMENT\_TYPE\_SZARRAY** **\<** *ConvertedType* **\>**<br /><br /> Numero di dimensioni \= 1, limite inferiore \= 0.  Il numero di dimensioni è noto solo se viene fornito nella firma gestita.|  
  
### Matrici protette  
 Quando si importa una matrice protetta da una libreria dei tipi in un assembly .NET, la matrice viene convertita in una matrice unidimensionale di tipo noto, ad esempio **int**.  Le stesse regole di conversione dei tipi che si applicano ai parametri sono valide anche per gli elementi delle matrici.  Una matrice protetta di tipi **BSTR** diventa ad esempio una matrice gestita di stringhe, mentre una matrice protetta di variant diventa una matrice gestita di oggetti.  Il tipo di elemento **SAFEARRAY** viene catturato dalla libreria dei tipi e salvato nel valore **SAFEARRAY** dell'enumerazione <xref:System.Runtime.InteropServices.UnmanagedType>.  
  
 Poiché il numero di dimensioni e i limiti della matrice sicura non possono essere determinati dalla libreria dei tipi, si presuppone che il numero di dimensioni corrisponda a 1 e che il limite inferiore sia pari a 0.  Il numero di dimensioni e i limiti devono essere definiti nella firma gestita prodotta da [Type Library Importer \(Tlbimp.exe\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md).  Se il numero di dimensioni passato al metodo in fase di esecuzione è diverso, viene generato un oggetto <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException>.  Se il tipo della matrice passato in fase di esecuzione è diverso, viene generato un oggetto <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException>.  Nell'esempio riportato di seguito sono mostrate matrici protette in codice gestito e non gestito.  
  
 **Firma non gestita**  
  
```  
HRESULT New1([in] SAFEARRAY( int ) ar);  
HRESULT New2([in] SAFEARRAY( DATE ) ar);  
HRESULT New3([in, out] SAFEARRAY( BSTR ) *ar);  
```  
  
 **Firma gestita**  
  
```vb  
Sub New1(<MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_I4)> _  
   ar() As Integer)  
Sub New2(<MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_DATE)> _   
   ar() As DateTime)  
Sub New3(ByRef <MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_BSTR)> _   
   ar() As String)  
  
```  
  
```csharp  
void New1([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_I4)] int[] ar) ;  
void New2([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_DATE)]   
   DateTime[] ar);  
void New3([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_BSTR)]   
   ref String[] ar);  
```  
  
 Per le matrici protette multidimensionali o con limite diverso da zero è possibile eseguire il marshalling nel codice gestito se la firma del metodo prodotta da Tlbimp.exe viene modificata per indicare un tipo di elemento **ELEMENT\_TYPE\_ARRAY** anziché **ELEMENT\_TYPE\_SZARRAY**.  In alternativa, è possibile utilizzare l'opzione **\/sysarray** con Tlbimp.exe per importare tutte le matrici come oggetti <xref:System.Array?displayProperty=fullName>.  Nei casi in cui è noto che la matrice passata è multidimensionale, è possibile modificare il codice MSIL \(Microsoft Intermediate Language\) prodotto da Tlbimp.exe, quindi ricompilarlo.  Per informazioni dettagliate su come modificare il codice MSIL, vedere [Personalizzazione dei wrapper di runtime disponibili per la chiamata](http://msdn.microsoft.com/it-it/4652beaf-77d0-4f37-9687-ca193288c0be).  
  
### Matrici di tipo C  
 Quando si importa una matrice di tipo C da una libreria dei tipi in un'istruzione assembly di .NET, la matrice viene convertita in **ELEMENT\_TYPE\_SZARRAY**.  
  
 Il tipo di elemento della matrice è determinato dalla libreria dei tipi e mantenuto nel corso dell'importazione.  Le stesse regole di conversione che si applicano ai parametri sono valide anche per gli elementi delle matrici.  Una matrice di tipi **LPStr** diventa ad esempio una matrice di tipi **String**.  Il tipo di elemento della matrice viene catturato da Tlbimp.exe e l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> viene applicato al parametro.  
  
 Si presuppone che il numero di dimensioni della matrice corrisponda a 1.  Se è maggiore di 1, viene effettuato il marshalling della matrice come matrice unidimensionale per lunghezza di colonna.  Il limite inferiore è sempre uguale a 0.  
  
 Le librerie dei tipi possono contenere matrici a lunghezza fissa o variabile.  Tlbimp.exe può importare solo matrici a lunghezza fissa dalle librerie dei tipi, in quanto tali librerie non contengono informazioni necessarie per eseguire il marshalling di matrici a lunghezza variabile.  Con le matrici a lunghezza fissa, la dimensione è importata dalla libreria dei tipi e catturata in **MarshalAsAttribute**, che viene applicato al parametro.  
  
 È necessario definire manualmente le librerie dei tipi contenenti le matrici a lunghezza variabile, come indicato nell'esempio seguente.  
  
 **Firma non gestita**  
  
```  
HRESULT New1(int ar[10]);  
HRESULT New2(double ar[10][20]);  
HRESULT New3(LPWStr ar[10]);  
```  
  
 **Firma gestita**  
  
```vb  
Sub New1(<MarshalAs(UnmanagedType.LPArray, SizeConst=10)> _  
   ar() As Integer)  
Sub New2(<MarshalAs(UnmanagedType.LPArray, SizeConst=200)> _  
   ar() As Double)  
Sub New2(<MarshalAs(UnmanagedType.LPArray, _  
   ArraySubType=UnmanagedType.LPWStr, SizeConst=10)> _  
   ar() As String)  
  
```  
  
```csharp  
void New1([MarshalAs(UnmanagedType.LPArray, SizeConst=10)] int[] ar);  
void New2([MarshalAs(UnmanagedType.LPArray, SizeConst=200)] double[] ar);  
void New2([MarshalAs(UnmanagedType.LPArray,   
   ArraySubType=UnmanagedType.LPWStr, SizeConst=10)] String[] ar);  
```  
  
 Sebbene sia possibile applicare gli attributi **size\_is** o **length\_is** a una matrice nell'origine IDL \(Interface Definition Language\) per comunicare la dimensione a un client, tale informazione non viene comunicata alla libreria dei tipi dal compilatore MIDL \(Microsoft Interface Definition Language\).  Senza sapere la dimensione, il servizio di marshalling di interoperabilità non può eseguire il marshalling degli elementi della matrice.  Di conseguenza, le matrici a lunghezza variabile sono importate come argomenti di riferimento.  Di seguito è riportato un esempio:  
  
 **Firma non gestita**  
  
```  
HRESULT New1(int ar[]);  
HRESULT New2(int ArSize, [size_is(ArSize)] double ar[]);  
HRESULT New3(int ElemCnt, [length_is(ElemCnt)] LPStr ar[]);  
```  
  
 **Firma gestita**  
  
```vb  
Sub New1(ByRef ar As Integer)  
Sub New2(ByRef ar As Double)  
Sub New3(ByRef ar As String)  
  
```  
  
```csharp  
void New1(ref int ar);    
void New2(ref double ar);    
void New3(ref String ar);   
```  
  
 È possibile fornire la dimensione della matrice al gestore di marshalling modificando il codice MSIL prodotto da Tlbimp.exe, quindi ricompilandolo.  Per informazioni dettagliate su come modificare il codice MSIL, vedere [Personalizzazione dei wrapper di runtime disponibili per la chiamata](http://msdn.microsoft.com/it-it/4652beaf-77d0-4f37-9687-ca193288c0be).  Per indicare il numero di elementi contenuti nella matrice, applicare il tipo <xref:System.Runtime.InteropServices.MarshalAsAttribute> al parametro di matrice della definizione del metodo gestito in uno dei modi indicati di seguito:  
  
-   Identificare un altro parametro contenente il numero di elementi presenti nella matrice.  I parametri vengono identificati in base alla posizione, a partire dal primo parametro indicato dal numero 0.  \[Visual Basic\]  
  
    ```vb  
    Sub [New](ElemCnt As Integer, _  
       <MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
       ar() As Integer)  
  
    ```  
  
    ```csharp  
    void New(  
       int ElemCnt,   
       [MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)] int[] ar );  
    ```  
  
-   Definire la dimensione della matrice come costante.  Di seguito è riportato un esempio:  
  
    ```vb  
    Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeConst:=128)> _  
       ar() As Integer)  
  
    ```  
  
    ```csharp  
    void New(  
       [MarshalAs(UnmanagedType.LPArray, SizeConst=128)] int[] ar );  
    ```  
  
 Quando si esegue il marshalling delle matrici dal codice non gestito al codice gestito, il gestore di marshalling controlla l'attributo **MarshalAsAttribute** associato al parametro per determinare la dimensione della matrice.  Se la dimensione della matrice non è specificata, viene eseguito il marshalling di un solo elemento.  
  
> [!NOTE]
>  **MarshalAsAttribute** non influisce sul marshalling delle matrici gestite sul codice non gestito.  In tale direzione, la dimensione della matrice viene determinata tramite l'esame.  Non è possibile eseguire il marshalling di un sottoinsieme di una matrice gestita.  
  
 I metodi **CoTaskMemAlloc** e **CoTaskMemFree** vengono utilizzati dal gestore di marshalling di interoperabilità per l'allocazione e il recupero della memoria.  Anche l'allocazione di memoria eseguita dal codice non gestito deve utilizzare questi metodi.  
  
<a name="cpcondefaultmarshalingforarraysanchor4"></a>   
## Passaggio di matrici a COM  
 Tutti i tipi di matrici gestite possono essere passati dal codice gestito al codice non gestito.  In base al tipo gestito e agli attributi a esso applicati, è possibile accedere alla matrice come matrice protetta o di tipo C, come illustrato nella tabella riportata di seguito.  
  
|Tipo di matrice gestito|Esportato come|  
|-----------------------------|--------------------|  
|**ELEMENT\_TYPE\_SZARRAY** **\<** *type* **\>**|<xref:System.Runtime.InteropServices.UnmanagedType> **.SafeArray\(** *tipo* **\)**<br /><br /> **UnmanagedType.LPArray**<br /><br /> Il tipo viene fornito nella firma.  Il numero di dimensioni è sempre 1, il limite inferiore è sempre 0.  La dimensione è sempre nota in fase di esecuzione.|  
|**ELEMENT\_TYPE\_ARRAY** **\<** *type* **\>** **\<** *rank* **\>**\[**\<** *bounds* **\>**\]|**UnmanagedType.SafeArray\(** *tipo* **\)**<br /><br /> **UnmanagedType.LPArray**<br /><br /> Tipo, numero di dimensioni e limiti sono forniti nella firma.  La dimensione è sempre nota in fase di esecuzione.|  
|**ELEMENT\_TYPE\_CLASS** **\<**<xref:System.Array?displayProperty=fullName>**\>**|**UT\_Interface**<br /><br /> **UnmanagedType.SafeArray\(** *tipo* **\)**<br /><br /> Tipo, numero di dimensioni, limiti e dimensione sono sempre noti in fase di esecuzione.|  
  
 Nell'automazione OLE è prevista una limitazione per le matrici di strutture contenenti LPSTR o LPWSTR.  Di conseguenza, per i campi di tipo **stringa** è necessario effettuare il marshalling come **UnmanagedType.BSTR**.  In caso contrario, verrà generata un'eccezione.  
  
### ELEMENT\_TYPE\_SZARRAY  
 Quando un metodo contenente un parametro **ELEMENT\_TYPE\_SZARRAY** \(matrice unidimensionale\) viene esportato da un assembly di .NET in una libreria dei tipi, il parametro di matrice viene convertito in un **SAFEARRAY** di un determinato tipo.  Le stesse regole di conversione valgono per i tipi di elementi matrice.  Il contenuto della matrice gestita viene copiato automaticamente dalla memoria gestita in **SAFEARRAY**.  Di seguito è riportato un esempio:  
  
#### Firma gestita  
  
```vb  
Sub [New](ar() As Long)  
Sub [New](ar() As String)  
  
```  
  
```csharp  
void New(long[] ar );  
void New(String[] ar );  
```  
  
#### Firma non gestita  
  
```  
HRESULT New([in] SAFEARRAY( long ) ar);   
HRESULT New([in] SAFEARRAY( BSTR ) ar);  
```  
  
 Il numero di dimensioni delle matrici sicure è sempre 1 e il limite inferiore è sempre 0.  La dimensione è determinata in fase di esecuzione dalla dimensione della matrice gestita passata.  
  
 È inoltre possibile eseguire il marshalling della matrice come matrice di tipo C mediante l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute>.  Di seguito è riportato un esempio:  
  
#### Firma gestita  
  
```vb  
Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
   ar() As Long, size as Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
   ar() As String, size as Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPArray, _  
   ArraySubType= UnmanagedType.LPStr, SizeParamIndex:=1)> _  
   ar() As String, size as Integer)  
  
```  
  
```csharp  
void New([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]   
   long [] ar, int size );  
void New([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]   
   String [] ar, int size );  
void New([MarshalAs(UnmanagedType.LPArray, ArraySubType=   
   UnmanagedType.LPStr, SizeParamIndex=1)]   
   String [] ar, int size );  
```  
  
#### Firma non gestita  
  
```  
HRESULT New(long ar[]);   
HRESULT New(BSTR ar[]);   
HRESULT New(LPStr ar[]);  
```  
  
 Sebbene il gestore di marshalling disponga delle informazioni sulla lunghezza necessarie per l'esecuzione del marshalling della matrice, la lunghezza della matrice viene in genere passata come argomento separato per comunicare la lunghezza al chiamato.  
  
### ELEMENT\_TYPE\_ARRAY  
 Quando un metodo contenente un parametro **ELEMENT\_TYPE\_ARRAY** viene esportato da un assembly di .NET in una libreria dei tipi, il parametro di matrice viene convertito in un **SAFEARRAY** di un determinato tipo.  Il contenuto della matrice gestita viene copiato automaticamente dalla memoria gestita in **SAFEARRAY**.  Di seguito è riportato un esempio:  
  
#### Firma gestita  
  
```vb  
Sub [New](ar(,) As Long)  
Sub [New](ar(,) As String)  
  
```  
  
```csharp  
void New( long [,] ar );  
void New( String [,] ar );  
```  
  
#### Firma non gestita  
  
```  
HRESULT New([in] SAFEARRAY( long ) ar);   
HRESULT New([in] SAFEARRAY( BSTR ) ar);  
```  
  
 Il numero di dimensioni, la dimensione e i limiti delle matrici protette sono determinati in fase di esecuzione dalle caratteristiche della matrice gestita.  
  
 È inoltre possibile eseguire il marshalling della matrice come matrice di tipo C mediante l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute>.  Di seguito è riportato un esempio:  
  
#### Firma gestita  
  
```vb  
Sub [New](<MarshalAs(UnmanagedType.LPARRAY, SizeParamIndex:=1)> _  
   ar(,) As Long, size As Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPARRAY, _  
   ArraySubType:=UnmanagedType.LPStr, SizeParamIndex:=1)> _  
   ar(,) As String, size As Integer)  
  
```  
  
```csharp  
void New([MarshalAs(UnmanagedType.LPARRAY, SizeParamIndex=1)]   
   long [,] ar, int size );  
void New([MarshalAs(UnmanagedType.LPARRAY,   
   ArraySubType= UnmanagedType.LPStr, SizeParamIndex=1)]   
   String [,] ar, int size );  
```  
  
#### Firma non gestita  
  
```  
HRESULT New(long ar[]);   
HRESULT New(LPStr ar[]);  
```  
  
 Non è possibile eseguire il marshalling delle matrici annidate.  Ad esempio, la firma seguente genera un errore nell'esportazione con l'[utilità di esportazione della libreria dei tipi \(Tlbexp.exe\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md).  
  
#### Firma gestita  
  
```vb  
Sub [New](ar()()() As Long)  
  
```  
  
```csharp  
void New(long [][][] ar );  
```  
  
### ELEMENT\_TYPE\_CLASS \<System.Array\>  
 Quando un metodo contenente un parametro <xref:System.Array?displayProperty=fullName> viene esportato da un assembly di .NET in una libreria dei tipi, il parametro di matrice viene convertito in un'interfaccia **\_Array**.  Il contenuto della matrice gestita è accessibile solo mediante i metodi e le proprietà dell'interfaccia **\_Array**.  È anche possibile eseguire il marshalling di **System.Array** come **SAFEARRAY** mediante l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute>.  Quando si esegue il marshalling come matrice protetta, il marshalling degli elementi della matrice viene eseguito come variant.  Di seguito è riportato un esempio:  
  
#### Firma gestita  
  
```vb  
Sub New1( ar As System.Array )  
Sub New2( <MarshalAs(UnmanagedType.Safe array)> ar As System.Array )  
  
```  
  
```csharp  
void New1( System.Array ar );  
void New2( [MarshalAs(UnmanagedType.Safe array)] System.Array ar );  
```  
  
#### Firma non gestita  
  
```  
HRESULT New([in] _Array *ar);   
HRESULT New([in] SAFEARRAY(VARIANT) ar);  
```  
  
### Matrici all'interno di strutture  
 Le strutture non gestite possono contenere matrici incorporate.  Per impostazione predefinita, per questi campi di matrici incorporate viene effettuato il marshalling come SAFEARRAY.  Nell'esempio seguente, `s1` è una matrice incorporata allocata direttamente all'interno della struttura stessa.  
  
#### Rappresentazione non gestita  
  
```  
struct MyStruct {  
    short s1[128];  
}  
```  
  
 È possibile eseguire il marshalling delle matrici come [UnmanagedType.ByValArray](frlrfSystemRuntimeInteropServicesUnmanagedTypeClassTopic), il che richiede di impostare il campo [MarshalAsAttribute.SizeConst](frlrfSystemRuntimeInteropServicesMarshalAsAttributeClassTopic).  La dimensione può essere impostata solo come una costante.  Nel codice riportato di seguito viene illustrata la definizione gestita corrispondente di  `MyStruct`.  
  
```vb  
Public Structure <StructLayout(LayoutKind.Sequential)> MyStruct  
   Public <MarshalAs(UnmanagedType.ByValArray, SizeConst := 128)> _  
     s1() As Short  
End Structure  
  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public struct MyStruct {  
   [MarshalAs(UnmanagedType.ByValArray, SizeConst=128)] public short[] s1;  
}  
```  
  
## Vedere anche  
 [Default Marshaling Behavior](../../../docs/framework/interop/default-marshaling-behavior.md)   
 [Blittable and Non\-Blittable Types](../../../docs/framework/interop/blittable-and-non-blittable-types.md)   
 [Directional Attributes](http://msdn.microsoft.com/it-it/241ac5b5-928e-4969-8f58-1dbc048f9ea2)   
 [Copying and Pinning](../../../docs/framework/interop/copying-and-pinning.md)