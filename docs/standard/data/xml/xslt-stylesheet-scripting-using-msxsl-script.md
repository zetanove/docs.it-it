---
title: "Scripting dei fogli di stile XSLT utilizzando &lt;msxsl:script&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 60e2541b-0cea-4b2e-a4fa-85f4c50f1bef
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Scripting dei fogli di stile XSLT utilizzando &lt;msxsl:script&gt;
La classe <xref:System.Xml.Xsl.XslTransform> supporta lo scripting incorporato mediante l'elemento `script`.  
  
> [!NOTE]
>  La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  È possibile eseguire le trasformazioni XSLT \(Extensible Stylesheet Language for Transformations\) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 La classe <xref:System.Xml.Xsl.XslTransform> supporta lo scripting incorporato mediante l'elemento `script`.  Dal momento che, quando viene caricato il foglio di stile, le funzioni definite vengono compilate nel linguaggio MSIL \(Microsoft Intermediate Language\) mediante l'incapsulamento in una definizione della classe, non si verifica alcuna riduzione delle prestazioni.  
  
 L'elemento `<msxsl:script>` viene definito di seguito:  
  
```  
<msxsl:script language = "language-name" implements-prefix = "prefix of user namespace"> </msxsl:script>  
```  
  
 dove `msxsl` è un prefisso associato allo spazio dei nomi `urn:schemas-microsoft-com:xslt`.  
  
 L'attributo `language` non è obbligatorio. Tuttavia, se specificato, deve presentare uno dei seguenti valori: C\#, VB, JScript, JavaScript, VisualBasic o CSharp.  Se omesso, il linguaggio viene impostato su JScript.  Poiché nel `language-name` non viene fatta distinzione tra maiuscole e minuscole, "JavaScript" e "javascript" si equivalgono.  
  
 L'attributo `implements-prefix` è obbligatorio.  Questo attributo viene usato per dichiarare uno spazio dei nomi e associarlo al blocco di script.  Il valore di questo attributo è il prefisso che rappresenta lo spazio dei nomi.  È possibile definire lo spazio dei nomi in un punto qualsiasi di un foglio di stile.  
  
 Poiché l'elemento `msxsl:script` appartiene allo spazio dei nomi `urn:schemas-microsoft-com:xslt`, il foglio di stile deve includere la dichiarazione dello spazio dei nomi `xmlns:msxsl=urn:schemas-microsoft-com:xslt`.  
  
 Se il chiamante dello script non dispone dell'autorizzazione di accesso [UnmanagedCode](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic), lo script presente nel foglio di stile non verrà compilato e non sarà possibile eseguire la chiamata a <xref:System.Xml.Xsl.XslTransform.Load%2A>.  
  
 Se il chiamante dispone dell'autorizzazione `UnmanagedCode`, lo script verrà compilato, ma le operazioni consentite dipenderanno dall'evidenza fornita in fase di caricamento.  
  
 Se per il caricamento del foglio di stile si usa uno dei metodi <xref:System.Xml.Xsl.XslTransform.Load%2A> che accettano un tipo <xref:System.Xml.XmlReader> o <xref:System.Xml.XPath.XPathNavigator>, è necessario usare il metodo di overload <xref:System.Xml.Xsl.XslTransform.Load%2A> che accetta un parametro <xref:System.Security.Policy.Evidence> come argomento.  Per fornire l'evidenza, il chiamante deve disporre dell'autorizzazione [ControlEvidence](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic) per fornire il parametro `Evidence` per l'assembly dello script.  Se il chiamante non dispone di questa autorizzazione, il parametro `Evidence` può essere impostato su `null`.  In questo caso la funzione <xref:System.Xml.Xsl.XslTransform.Load%2A> non viene eseguita se vengono rilevati degli script.  L'autorizzazione `ControlEvidence` è molto efficace e deve essere concessa esclusivamente a codice completamente attendibile.  
  
 Per ottenere l'evidenza dall'assembly, usare `this.GetType().Assembly.Evidence`.  Per ottenere l'evidenza da un URI \(Uniform Resource Identifier\), usare `Evidence e = XmlSecureResolver.CreateEvidenceForUrl(stylesheetURI)`.  
  
 Se si usano i metodi <xref:System.Xml.Xsl.XslTransform.Load%2A> che accettano un tipo <xref:System.Xml.XmlResolver> e non dispongono del parametro `Evidence`, l'impostazione predefinita per l'area di sicurezza dell'assembly è Attendibilità totale.  Per altre informazioni, vedere <xref:System.Security.SecurityZone> e [Set di autorizzazioni denominati](http://msdn.microsoft.com/it-it/08250d67-c99d-4ab0-8d2b-b0e12019f6e3).  
  
 È possibile dichiarare le funzioni all'interno dell'elemento `msxsl:script`.  Nella tabella seguente sono illustrati gli spazi dei nomi supportati per impostazione predefinita.  È possibile usare classi che non sono comprese negli spazi dei nomi elencati.  Tuttavia, è necessario che tali classi siano complete.  
  
|Spazi dei nomi predefiniti|Descrizione|  
|--------------------------------|-----------------|  
|Sistema|Classe di sistema.|  
|System.Collection|Classi di raccolte.|  
|System.Text|Classi di testo.|  
|System.Text.RegularExpressions|Classi di espressioni regolari.|  
|System.Xml|Classi XML di base.|  
|System.Xml.Xsl|Classi XSLT.|  
|System.Xml.XPath|Classi XPath \(XML Path Language\).|  
|Microsoft.VisualBasic|Classi per gli script Microsoft Visual Basic.|  
  
 Quando si dichiara una funzione, questa è contenuta in un blocco di script.  I fogli di stile possono contenere più blocchi di script con funzionamento indipendente l'uno dall'altro.  Ciò significa che, all'interno di un blocco di script, non è possibile chiamare una funzione definita in un altro blocco di script a meno che per quest'ultimo non sia dichiarato lo stesso spazio dei nomi e lo stesso linguaggio di script.  Poiché ogni blocco di script può essere scritto nel proprio linguaggio e il blocco viene analizzato in base alle regole grammaticali del parser di quel linguaggio, è necessario usare la sintassi corretta per il linguaggio in uso.  Ad esempio, in un blocco di script C\# è un errore usare un nodo Comment XML `<!-- an XML comment -->` nel blocco.  
  
 È necessario che gli argomenti forniti e i valori restituiti definiti dalle funzioni di script siano di tipo W3C \(World Wide Web Consortium\) XPath o XSLT.  Nella tabella seguente vengono mostrati i tipi W3C corrispondenti, le classi .NET Framework equivalenti \(tipo\) e se il tipo W3C è un tipo XPath o XSLT.  
  
|Tipo|Classe .NET Framework equivalente \(tipo\)|Tipo XPath o tipo XSLT|  
|----------|------------------------------------------------|----------------------------|  
|String|System.String|XPath|  
|Boolean|System.Boolean|XPath|  
|Numero|System.Double|XPath|  
|Frammento di albero risultato|System.Xml.XPath.XPathNavigator|XSLT|  
|Node set|System.Xml.XPath.XPathNodeIterator|XPath|  
  
 Se la funzione di script usa un tipo numerico quale Int16, UInt16, Int32, UInt32, Int64, UInt64, Single o Decimal, questo verrà convertito in Double, che corrisponde al numero del tipo W3C XPath.  Tutti gli altri tipi verranno convertiti in stringhe usando il metodo `ToString`.  
  
 Se la funzione di script usa un tipo diverso da quelli specificati in precedenza o se la funzione non viene compilata quando il foglio di stile viene caricato nell'oggetto <xref:System.Xml.Xsl.XslTransform>, verrà generata un'eccezione.  
  
 Quando si usa l'elemento  `msxsl:script`, si consiglia che tale script, indipendentemente dal linguaggio, venga inserito all'interno di una sezione CDATA.  Nel codice XML seguente, ad esempio, viene illustrato il modello della sezione CDATA in cui è inserito il codice.  
  
```  
<msxsl:script implements-prefix='yourprefix' language='CSharp'>  
    <![CDATA[  
    ... your code here ...  
    ]]>  
</msxsl:script>  
```  
  
 Si consiglia di inserire tutto il contenuto dello script in una sezione CDATA, poiché è possibile che gli operatori, gli identificatori o i delimitatori per un determinato linguaggio vengano erroneamente interpretati come XML.  Nell'esempio seguente viene illustrato l'uso dell'operatore logico AND nello script.  
  
```  
<msxsl:script implements-prefix='yourprefix' language='CSharp>  
    public string book(string abc, string xyz)  
    {  if ((abc== abc)&&(abc== xyz)) return bar+xyz;  
        else return null;  
    }  
</msxsl:script>  
```  
  
 In questo esempio viene generata un'eccezione in quanto le e commerciali non sono in sequenza di escape.  Il documento viene caricato come XML e non viene applicato alcun trattamento speciale al testo compreso tra i tag dell'elemento  `msxsl:script`.  
  
## Esempio  
 Nell'esempio seguente viene usato uno script incorporato per calcolare la circonferenza di un cerchio di cui viene fornito il raggio.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public Class Sample  
  
   Private Const filename As String = "number.xml"  
   Private Const stylesheet As String = "calc.xsl"  
  
   Public Shared Sub Main()  
  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XmlTextWriter to output to the console.               
    Dim writer As XmlTextWriter = New XmlTextWriter(Console.Out)  
    writer.Formatting = Formatting.Indented  
  
    'Transform the file.  
    xslt.Transform(doc, Nothing, writer, Nothing)  
    writer.Close()  
  End Sub   
End Class  
  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.XPath;  
using System.Xml.Xsl;  
  
public class Sample  
{  
   private const String filename = "number.xml";  
   private const String stylesheet = "calc.xsl";  
  
   public static void Main() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XmlTextWriter to output to the console.               
    XmlTextWriter writer = new XmlTextWriter(Console.Out);  
    writer.Formatting = Formatting.Indented;  
  
    //Transform the file.  
    xslt.Transform(doc, null, writer, null);  
    writer.Close();  
  }   
}  
```  
  
## Input  
 number.xml  
  
```  
<?xml version='1.0'?>  
<data>  
  <circle>  
    <radius>12</radius>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
  </circle>  
</data>  
```  
  
 calc.xsl  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
    xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
    xmlns:user="urn:my-scripts">  
  
  <msxsl:script language="C#" implements-prefix="user">  
     <![CDATA[  
     public double circumference(double radius){  
       double pi = 3.14;  
       double circ = pi*radius*2;  
       return circ;  
     }  
      ]]>  
   </msxsl:script>  
  
  <xsl:template match="data">    
  <circles>  
  
  <xsl:for-each select="circle">  
    <circle>  
    <xsl:copy-of select="node()"/>  
       <circumference>  
          <xsl:value-of select="user:circumference(radius)"/>   
       </circumference>  
    </circle>  
  </xsl:for-each>  
  </circles>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
## Output  
  
```  
<circles xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="urn:my-scripts">  
  <circle>  
    <radius>12</radius>  
    <circumference>75.36</circumference>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
    <circumference>235.5</circumference>  
  </circle>  
</circles>    
```  
  
## Vedere anche  
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)