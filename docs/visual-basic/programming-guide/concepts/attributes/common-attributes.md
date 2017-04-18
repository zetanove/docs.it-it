---
title: Attributi comuni (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 11fe4894-1bf9-4525-a36b-cddcd3a5d22b
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
ms.openlocfilehash: f470e6ff3e316076d71a34346f741cc4504471a3
ms.lasthandoff: 03/13/2017

---
# <a name="common-attributes-visual-basic"></a>Attributi comuni (Visual Basic)
In questo argomento vengono descritti gli attributi più comunemente utilizzati nei programmi Visual Basic.  
  
-   [Attributi globali](#Global)  
  
-   [Attributo obsolete](#Obsolete)  
  
-   [Attributo condizionale](#Conditional)  
  
-   [Attributi informativi sul chiamante](#CallerInfo)  
  
-   [Visual Basic (attributi)](#VB)  
  
##  <a name="Global"></a>Attributi globali  
 Quasi tutti gli attributi vengono applicati agli elementi del linguaggio specifico, ad esempio classi o metodi. Tuttavia, alcuni attributi sono globali, si applicano a un intero assembly o un modulo. Ad esempio, il <xref:System.Reflection.AssemblyVersionAttribute>attributo può essere utilizzato per incorporare le informazioni sulla versione in un assembly, simile al seguente:</xref:System.Reflection.AssemblyVersionAttribute>  
  
```vb  
<Assembly: AssemblyVersion("1.0.0.0")>  
```  
  
 Gli attributi globali vengono visualizzati nel codice sorgente dopo eventuali principale`Imports` istruzioni e prima delle dichiarazioni di tipo, modulo o dello spazio dei nomi. Gli attributi globali possono essere visualizzati in più file di origine, ma i file devono essere compilati in un singolo passaggio. Per i progetti di Visual Basic, gli attributi globali vengono in genere inseriti nel file AssemblyInfo. vb (il file viene creato automaticamente quando si crea un progetto in Visual Studio).  
  
 Gli attributi dell'assembly sono valori che forniscono informazioni relative a un assembly. Rientrano nelle categorie seguenti:  
  
-   Attributi di identità dell'assembly  
  
-   Alcuni attributi informativi  
  
-   Attributi del manifesto dell'assembly  
  
### <a name="assembly-identity-attributes"></a>Attributi relativi all'identità dell'assembly  
 Tre attributi (con un nome sicuro, se applicabile) determinano l'identità di un assembly: nome, versione e delle impostazioni cultura. Questi attributi il nome completo dell'assembly e sono necessari quando si fa riferimento nel codice. È possibile impostare versione e le impostazioni cultura utilizzando gli attributi di un assembly. Tuttavia, il valore del nome viene impostato dal compilatore, l'IDE di Visual Studio nel [la finestra di dialogo informazioni Assembly](https://docs.microsoft.com/visualstudio/ide/reference/assembly-information-dialog-box), o Assembly Linker (Al.exe) quando viene creato l'assembly, in base al file che contiene il manifesto dell'assembly. Il <xref:System.Reflection.AssemblyFlagsAttribute>attributo specifica se è possano la coesistenza di più copie dell'assembly.</xref:System.Reflection.AssemblyFlagsAttribute>  
  
 Nella tabella seguente vengono illustrati gli attributi di identità.  
  
|Attributo|Scopo|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyName></xref:System.Reflection.AssemblyName>|Viene descritta l'identità di un assembly.|  
|<xref:System.Reflection.AssemblyVersionAttribute></xref:System.Reflection.AssemblyVersionAttribute>|Specifica la versione di un assembly.|  
|<xref:System.Reflection.AssemblyCultureAttribute></xref:System.Reflection.AssemblyCultureAttribute>|Specifica le impostazioni cultura supportate dall'assembly.|  
|<xref:System.Reflection.AssemblyFlagsAttribute></xref:System.Reflection.AssemblyFlagsAttribute>|Specifica se un assembly supporta l'esecuzione side-by-side nello stesso computer, nello stesso processo o nello stesso dominio applicazione.|  
  
### <a name="informational-attributes"></a>Attributi informativi  
 Gli attributi informativi consentono di fornire informazioni aggiuntive relative alla società o al prodotto per un assembly. Nella tabella seguente vengono illustrati gli attributi informativi definiti nel <xref:System.Reflection?displayProperty=fullName>dello spazio dei nomi.</xref:System.Reflection?displayProperty=fullName>  
  
|Attributo|Scopo|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyProductAttribute></xref:System.Reflection.AssemblyProductAttribute>|Definisce un attributo personalizzato che specifica un nome di prodotto per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyTrademarkAttribute></xref:System.Reflection.AssemblyTrademarkAttribute>|Definisce un attributo personalizzato che specifica un marchio registrato per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyInformationalVersionAttribute></xref:System.Reflection.AssemblyInformationalVersionAttribute>|Definisce un attributo personalizzato che specifica la versione informativa per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyCompanyAttribute></xref:System.Reflection.AssemblyCompanyAttribute>|Definisce un attributo personalizzato che specifica un nome della società per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyCopyrightAttribute></xref:System.Reflection.AssemblyCopyrightAttribute>|Definisce un attributo personalizzato che specifica informazioni sul copyright per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyFileVersionAttribute></xref:System.Reflection.AssemblyFileVersionAttribute>|Indica al compilatore di utilizzare un numero di versione specifici per la risorsa di versione del file Win32.|  
|<xref:System.CLSCompliantAttribute></xref:System.CLSCompliantAttribute>|Indica se l'assembly è compatibile con la specifica CLS (Common Language).|  
  
### <a name="assembly-manifest-attributes"></a>Attributi relativi al manifesto dell'assembly  
 È possibile utilizzare gli attributi del manifesto dell'assembly per fornire informazioni nel manifesto dell'assembly. Sono inclusi titolo, descrizione, alias predefinito e configurazione. Nella tabella seguente vengono definiscono gli attributi del manifesto dell'assembly nel <xref:System.Reflection?displayProperty=fullName>dello spazio dei nomi.</xref:System.Reflection?displayProperty=fullName>  
  
|Attributo|Scopo|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyTitleAttribute></xref:System.Reflection.AssemblyTitleAttribute>|Definisce un attributo personalizzato che specifica il titolo dell'assembly per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyDescriptionAttribute></xref:System.Reflection.AssemblyDescriptionAttribute>|Definisce un attributo personalizzato che specifica la descrizione dell'assembly per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyConfigurationAttribute></xref:System.Reflection.AssemblyConfigurationAttribute>|Definisce un attributo personalizzato che specifica la configurazione dell'assembly (ad esempio finale o di debug) per un manifesto dell'assembly.|  
|<xref:System.Reflection.AssemblyDefaultAliasAttribute></xref:System.Reflection.AssemblyDefaultAliasAttribute>|Definisce un alias predefinito descrittivo per un manifesto dell'assembly|  
  
##  <a name="Obsolete"></a>Attributo obsolete  
 Il `Obsolete` attributo contrassegna un'entità che non è più consigliato per l'utilizzo del programma. Ciascun utilizzo di un'entità contrassegnata successivamente genererà un avviso o errore, a seconda della configurazione dell'attributo. Ad esempio:  
  
```vb  
<System.Obsolete("use class B")>   
Class A  
    Sub Method()  
    End Sub  
End Class  
  
Class B  
    <System.Obsolete("use NewMethod", True)>   
    Sub OldMethod()  
    End Sub  
  
    Sub NewMethod()  
    End Sub  
End Class  
```  
  
 In questo esempio il `Obsolete` attributo viene applicato alla classe `A` e al metodo `B.OldMethod`. Poiché il secondo argomento del costruttore dell'attributo applicato a `B.OldMethod` è impostato su `true`, questo metodo genererà un errore del compilatore, mentre l'utilizzo di classe `A` produrrà semplicemente un avviso. La chiamata `B.NewMethod`, tuttavia, non produce alcun avviso o errore.  
  
 La stringa fornita come primo argomento al costruttore dell'attributo verrà visualizzata come parte dell'avviso o errore. Ad esempio, se utilizzato con le definizioni precedenti, il codice seguente genera un errore e due avvisi:  
  
```vb  
' Generates 2 warnings:  
' Dim a As New A  
' Generate no errors or warnings:  
  
Dim b As New B  
b.NewMethod()  
  
' Generates an error, terminating compilation:  
' b.OldMethod()  
```  
  
 Due avvisi per la classe `A` generati: uno per la dichiarazione del riferimento della classe e uno per il costruttore della classe.  
  
 Il `Obsolete` attributo può essere utilizzato senza argomenti, ma inclusi una spiegazione del motivo per cui l'elemento è obsoleto e gli elementi da utilizzare in alternativa è consigliata.  
  
 Il `Obsolete` è un attributo a utilizzo singolo e può essere applicato a qualsiasi entità che supporta gli attributi. `Obsolete`è un alias per <xref:System.ObsoleteAttribute>.</xref:System.ObsoleteAttribute>  
  
##  <a name="Conditional"></a>Attributo condizionale  
 Il `Conditional` attributo rende l'esecuzione di un metodo dipendente da un identificatore di pre-elaborazione. Il `Conditional` attributo è un alias per <xref:System.Diagnostics.ConditionalAttribute>e può essere applicato a un metodo o una classe di attributo.</xref:System.Diagnostics.ConditionalAttribute>  
  
 In questo esempio, `Conditional` viene applicato a un metodo per attivare o disattivare la visualizzazione delle informazioni di diagnostica specifici del programma:  
  
```vb  
#Const TRACE_ON = True  
Imports System  
Imports System.Diagnostics  
Module TestConditionalAttribute  
    Public Class Trace  
        <Conditional("TRACE_ON")>   
        Public Shared Sub Msg(ByVal msg As String)  
            Console.WriteLine(msg)  
        End Sub  
  
    End Class  
  
    Sub Main()  
        Trace.Msg("Now in Main...")  
        Console.WriteLine("Done.")  
    End Sub  
End Module  
```  
  
 Se il `TRACE_ON` identificatore non è definito, non verrà visualizzato alcun output di traccia.  
  
 Il `Conditional` attributo viene spesso utilizzato con il `DEBUG` identificatore per abilitare la traccia e funzioni di registrazione per le compilazioni di debug ma non in versioni finali, come segue:  
  
```vb  
<Conditional("DEBUG")>   
Shared Sub DebugMethod()  
  
End Sub  
```  
  
 Quando viene chiamato un metodo contrassegnato come condizionali, la presenza o l'assenza del simbolo di pre-elaborazione specificato determina se la chiamata è incluso o omesso. Se il simbolo è definito, la chiamata è inclusa; in caso contrario, viene omessa. Utilizzando `Conditional` è un'alternativa più semplice, più elegante e meno soggetto a errori rispetto all'inclusione di metodi all'interno di `#if…#endif` blocchi, simile al seguente:  
  
```vb  
#If DEBUG Then  
    Sub ConditionalMethod()  
    End Sub  
#End If  
```  
  
 Un metodo condizionale deve essere un metodo in una dichiarazione di classe o uno struct e non deve avere un valore restituito.  
  
### <a name="using-multiple-identifiers"></a>Utilizzo di più identificatori  
 Se un metodo ha più `Conditional` gli attributi, una chiamata al metodo è inclusa se almeno uno dei simboli condizionali sia definito (in altre parole, i simboli sono logicamente collegati tra loro mediante l'operatore OR). In questo esempio, la presenza di `A` o `B` determinerà una chiamata al metodo:  
  
```vb  
<Conditional("A"), Conditional("B")>   
Shared Sub DoIfAorB()  
  
End Sub  
```  
  
 Per ottenere l'effetto di collegamento logico di simboli tramite l'operatore AND, è possibile definire metodi condizionali seriali. Ad esempio, il secondo metodo riportato di seguito verrà eseguito solo se entrambi `A` e `B` vengono definiti:  
  
```vb  
<Conditional("A")>   
Shared Sub DoIfA()  
    DoIfAandB()  
End Sub  
  
<Conditional("B")>   
Shared Sub DoIfAandB()  
    ' Code to execute when both A and B are defined...  
End Sub  
```  
  
### <a name="using-conditional-with-attribute-classes"></a>Con le classi di attributi condizionali  
 Il `Conditional` attributo può anche essere applicato a una definizione di classe attribute. In questo esempio, l'attributo personalizzato `Documentation` aggiungerà le informazioni solo per i metadati se DEBUG è definito.  
  
```vb  
<Conditional("DEBUG")>   
Public Class Documentation  
    Inherits System.Attribute  
    Private text As String  
    Sub New(ByVal doc_text As String)  
        text = doc_text  
    End Sub  
End Class  
  
Class SampleClass  
    ' This attribute will only be included if DEBUG is defined.  
    <Documentation("This method displays an integer.")>   
    Shared Sub DoWork(ByVal i As Integer)  
        System.Console.WriteLine(i)  
    End Sub  
End Class  
```  
  
##  <a name="CallerInfo"></a>Attributi informativi sul chiamante  
 Gli attributi di informazioni sul chiamante consentono di ottenere informazioni sul chiamante di un metodo. È possibile ottenere il percorso del file del codice sorgente, il numero di riga nel codice sorgente e il nome del membro del chiamante.  
  
 Per ottenere informazioni sul chiamante, utilizzare gli attributi applicati ai parametri facoltativi. Ciascun parametro facoltativo specifica un valore predefinito. Nella tabella seguente vengono elencati gli attributi di informazioni sul chiamante definiti nel <xref:System.Runtime.CompilerServices?displayProperty=fullName>dello spazio dei nomi:</xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
|Attributo|Descrizione|Tipo|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute></xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|Percorso completo del file di origine contenente il chiamante. Si tratta del percorso in fase di compilazione.|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute></xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|Numero di riga nel file di origine da cui viene chiamato il metodo.|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute></xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|Nome di metodo o proprietà del chiamante. Per ulteriori informazioni, vedere [informazioni sul chiamante (Visual Basic)](../../../../visual-basic/programming-guide/concepts/caller-information.md).|`String`|  
  
 Per ulteriori informazioni sugli attributi di informazioni sul chiamante, vedere [informazioni sul chiamante (Visual Basic)](../../../../visual-basic/programming-guide/concepts/caller-information.md).  
  
##  <a name="VB"></a>Visual Basic (attributi)  
 Nella tabella seguente vengono elencati gli attributi specifici di Visual Basic.  
  
|Attributo|Scopo|  
|---------------|-------------|  
|<xref:Microsoft.VisualBasic.ComClassAttribute></xref:Microsoft.VisualBasic.ComClassAttribute>|Indica al compilatore che la classe deve essere esposto come un oggetto COM.|  
|<xref:Microsoft.VisualBasic.HideModuleNameAttribute></xref:Microsoft.VisualBasic.HideModuleNameAttribute>|Consente ai membri del modulo a cui accedere utilizzando solo la qualifica necessaria per il modulo.|  
|<xref:Microsoft.VisualBasic.VBFixedStringAttribute></xref:Microsoft.VisualBasic.VBFixedStringAttribute>|Specifica la dimensione di una stringa a lunghezza fissa in una struttura da utilizzare con file di input e output funzioni.|  
|<xref:Microsoft.VisualBasic.VBFixedArrayAttribute></xref:Microsoft.VisualBasic.VBFixedArrayAttribute>|Specifica la dimensione di una matrice fissa in una struttura da utilizzare con file di input e output funzioni.|  
  
### <a name="comclassattribute"></a>COMClassAttribute  
 Utilizzare `COMClassAttribute` per semplificare il processo di creazione di componenti COM da Visual Basic. Gli oggetti COM sono notevolmente diversi dagli assembly .NET Framework e senza `COMClassAttribute`, è necessario seguire una serie di passaggi per generare un oggetto COM da Visual Basic. Per le classi contrassegnate con `COMClassAttribute`, il compilatore esegue automaticamente molti di questi passaggi.  
  
### <a name="hidemodulenameattribute"></a>HideModuleNameAttribute  
 Utilizzare `HideModuleNameAttribute` per consentire l'accesso utilizzando solo la qualifica necessaria per il modulo ai membri del modulo.  
  
### <a name="vbfixedstringattribute"></a>VBFixedStringAttribute  
 Utilizzare `VBFixedStringAttribute` per forzare Visual Basic per creare una stringa a lunghezza fissa. Le stringhe sono di lunghezza variabile per impostazione predefinita, e questo attributo è utile quando si archiviano stringhe nei file. Il codice seguente illustra questo processo:  
  
```vb  
Structure Worker  
    ' The runtime uses VBFixedString to determine   
    ' if the field should be written out as a fixed size.  
    <VBFixedString(10)> Public LastName As String  
    <VBFixedString(7)> Public Title As String  
    <VBFixedString(2)> Public Rank As String  
End Structure  
```  
  
### <a name="vbfixedarrayattribute"></a>VBFixedArrayAttribute  
 Utilizzare `VBFixedArrayAttribute` per dichiarare matrici di dimensioni fisse. Le stringhe di Visual Basic, le matrici sono di lunghezza variabile per impostazione predefinita. Questo attributo è utile durante la serializzazione o la scrittura di dati nei file.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection></xref:System.Reflection>   
 <xref:System.Attribute></xref:System.Attribute>   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)   
 [Attributi](https://msdn.microsoft.com/library/5x6cd29c)   
 [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Accesso agli attributi tramite Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
