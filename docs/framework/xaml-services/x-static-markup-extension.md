---
title: "x:Static Markup Extension | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "StaticExtension"
  - "xStatic"
  - "x:Static"
helpviewer_keywords: 
  - "x:Static markup extension [XAML Services]"
  - "Static markup extension in XAML [XAML Services]"
  - "XAML [XAML Services], x:Static markup extension"
ms.assetid: 056aee79-7cdd-434f-8174-dfc856cad343
caps.latest.revision: 25
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 25
---
# x:Static Markup Extension
Fa riferimento a qualsiasi entità statica del codice per valore definita in una modalità conforme [!INCLUDE[TLA#tla_cls](../../../includes/tlasharptla-cls-md.md)].  La proprietà statica a cui viene fatto riferimento può essere utilizzata per fornire il valore di una proprietà in XAML.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{x:Static prefix:typeName.staticMemberName}" .../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`prefix`|Parametro facoltativo.  Prefisso che fa riferimento a uno spazio dei nomi XAML non predefinito e mappato.  `prefix` viene mostrato in modo esplicito nell'utilizzo perché raramente si fa riferimento a proprietà statiche che vengono da uno spazio dei nomi XAML predefinito.  Vedere la sezione Osservazioni.|  
|`typeName`|Obbligatorio.  Il nome del tipo che definisce il membro statico desiderato.|  
|`staticMemberName`|Obbligatorio.  Nome del membro del valore statico desiderato \(una costante, una proprietà statica, un campo o un valore di enumerazione\).|  
  
## Note  
 L'entità di codice a cui viene fatto riferimento deve essere uno degli elementi seguenti:  
  
-   Una costante  
  
-   Proprietà statica  
  
-   Campo  
  
-   Valore di enumerazione  
  
 Specificando qualsiasi altra entità del codice, quale una proprietà non statica, si provoca un errore della fase di compilazione se in XAML è avvenuta la compilazione di markup, o un'eccezione di analisi del tempo di caricamento di XAML.  
  
 È possibile stabilire riferimenti `x:Static` a proprietà o campi statici non inclusi nello spazio dei nomi XAML predefinito per il documento XAML corrente; tuttavia, questa operazione richiede un mapping di prefisso.  Gli spazi dei nomi XAML sono quasi sempre definiti sull'elemento radice del documento XAML.  
  
 Le operazioni di ricerca per le proprietà statiche possono essere eseguite dai servizi XAML di .NET Framework, dai lettori XAML e dai writer XAML, quando sono in esecuzione con il contesto dello schema XAML predefinito.  Questo contesto dello schema XAML può utilizzare reflection CLR per fornire i valori statici necessari per la costruzione dell'oggetto grafico.  L'elemento `typeName` specificato è in realtà un nome di tipo XAML, non un nome di tipo CLR, anche se questi sono essenzialmente lo stesso nome quando si utilizza il contesto dello schema XAML predefinito o quando si utilizzano tutti i framework esistenti che implementano XAML in base a CLR.  
  
 Fare attenzione quando si creano riferimenti `x:Static` che non sono direttamente il tipo di valore di una proprietà.  Nella sequenza dell'elaborazione XAML, i valori forniti da un'estensione di markup non richiamano un'ulteriore conversione di valori.  Questo è vero anche se il riferimento `x:Static` crea una stringa di testo e in genere si verifica una conversione di valori per valori dell'attributo basati su stringa di testo per quel membro specifico o per qualsiasi valore del membro del tipo restituito.  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Il token di stringa fornito dopo la stringa dell'identificatore `x:Static` viene assegnato come valore <xref:System.Windows.Markup.StaticExtension.Member%2A> della classe dell'estensione <xref:System.Windows.Markup.StaticExtension> sottostante.  
  
 Ci sono due altri utilizzi di XAML tecnicamente possibili.  Tuttavia, questi utilizzi sono meno comuni perché inutilmente dettagliati:  
  
 **Sintassi per elementi oggetto:** `<x:Static Member="``prefix``:``typeName``.``staticMemberName``" .../>`  
  
 **Sintassi degli attributi con proprietà del membro esplicita per stringa di inizializzazione:** `<``object````property``="{x:Static Member=``prefix``:``typeName``.``staticMemberName``}" .../>`  
  
 Nell'implementazione dei servizi XAML di .NET Framework la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.Markup.StaticExtension>.  
  
 `x:Static` è un'estensione di markup.  Tutte le estensioni di markup in XAML utilizzano i caratteri `{` e `}` nella relativa sintassi per attributi. Si tratta della convenzione che consente al processore XAML di determinare che un'estensione di markup deve fornire un valore.  Per ulteriori informazioni sulle estensioni di markup, vedere [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md).  
  
## Note sull'utilizzo di WPF  
 Lo spazio dei nomi XAML predefinito utilizzato per la programmazione WPF non contiene molte proprietà statiche utili e la maggior parte delle proprietà statiche utili dispongono di supporto, come ad esempio convertitori di tipi che facilitano l'utilizzo senza richiedere `{x:Static}`.  Per le proprietà statiche, è necessario eseguire il mapping di un prefisso per uno spazio dei nomi XAML se uno degli elementi seguenti è vero:  
  
-   Si fa riferimento a un tipo che esiste in WPF, ma che non appartiene allo spazio dei nomi XAML predefinito per WPF \([!INCLUDE[TLA#tla_wpfxmlnsv1](../../../includes/tlasharptla-wpfxmlnsv1-md.md)]\).  Si tratta di uno scenario abbastanza comune per l'utilizzo di `x:Static`.  Ad esempio, è possibile utilizzare un riferimento `x:Static` con un mapping di spazio dei nomi XAML allo spazio dei nomi CLR e assembly mscorlib <xref:System> per fare riferimento alle proprietà statiche della classe <xref:System.Environment>.  
  
-   Si fa riferimento a un tipo da un assembly personalizzato.  
  
-   Si fa riferimento a un tipo presente in un assembly WPF, ma questo tipo è incluso in uno spazio dei nomi CLR non mappato allo scopo di includerlo nello spazio dei nomi XAML predefinito WPF.  Il mapping degli spazi dei nomi CLR nello spazio dei nomi XAML predefinito per WPF viene eseguito dalle definizioni nei vari assembly WPF \(per ulteriori informazioni su questo concetto, vedere [Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF](../../../ocs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)\).  Spazi dei nomi CLR non mappati possono essere presenti se il nome dello spazio CLR è composto per lo più da definizioni di classi non destinate a XAML, come ad esempio <xref:System.Windows.Threading>.  
  
 Per ulteriori informazioni su come utilizzare i prefissi e gli spazi dei nomi XAML per WPF, vedere [Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF](../../../ocs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md).  
  
## Vedere anche  
 [x:Type Markup Extension](../../../docs/framework/xaml-services/x-type-markup-extension.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)