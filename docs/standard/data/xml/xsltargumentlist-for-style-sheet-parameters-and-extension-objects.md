---
title: "XsltArgumentList per i parametri dei fogli di stile e gli oggetti di estensione | Microsoft Docs"
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
ms.assetid: de2f0dce-6b98-4908-bba7-ed150cc50355
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XsltArgumentList per i parametri dei fogli di stile e gli oggetti di estensione
La classe <xref:System.Xml.Xsl.XsltArgumentList> contiene parametri Extensible Stylesheet Language for Transformations \(XSLT\) e oggetti di estensione XSLT.  Quando vengono passati al metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A>, questi parametri e oggetti di estensione possono essere richiamati dai fogli di stile.  
  
> [!NOTE]
>  Le classi <xref:System.Xml.Xsl.XslTransform> e <xref:System.Xml.Xsl.XsltArgumentList> sono obsolete in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  È possibile eseguire le trasformazioni XSLT usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 La classe <xref:System.Xml.Xsl.XsltArgumentList> contiene i parametri XSLT e gli oggetti di estensione XSLT.  Quando vengono passati al metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A>, questi parametri e oggetti di estensione possono essere richiamati dai fogli di stile.  
  
 I vantaggi del passaggio di un oggetto rispetto all'uso di uno script incorporato sono i seguenti:  
  
-   Migliore incapsulamento e riutilizzo delle classi.  
  
-   Fogli di stile di dimensioni minori e più gestibili.  
  
-   Supporto della chiamata ai metodi nelle classi appartenenti a spazi dei nomi diversi da quelli definiti nel set degli spazi dei nomi <xref:System> supportati.  
  
-   Possibilità di passare i frammenti di albero risultato al foglio di stile usando <xref:System.Xml.XPath.XPathNodeIterator>.  
  
## Parametri dei fogli di stile XSLT  
 I parametri XSLT vengono aggiunti all'elenco <xref:System.Xml.Xsl.XsltArgumentList> mediante il metodo <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>.  Un nome completo e un URI dello spazio dei nomi sono associati all'oggetto parametro in quel momento.  
  
 L'oggetto parameter deve corrispondere a un tipo W3C \(World Wide Web Consortium\).  Nella tabella seguente sono illustrati i tipi W3C corrispondenti e le classi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] equivalenti \(tipo\) e viene indicato se il tipo W3C è un tipo XPath o XSLT.  
  
|Tipo W3C|Classe .NET Framework equivalente \(tipo\)|Tipo XPath o tipo XSLT|  
|--------------|------------------------------------------------|----------------------------|  
|String|System.String|XPath|  
|Boolean|System.Boolean|XPath|  
|Numero|System.Double|XPath|  
|Frammento di albero risultato|System.Xml.XPath.XPathNavigator|XSLT|  
|Node set|System.Xml.XPath.XPathNodeIterator|XPath|  
  
 Se l'oggetto parameter non fa parte di una delle classi sopra elencate, è obbligato a essere Double o String, in base alle esigenze.  I tipi Int16, UInt16, Int32, UInt32, Int64, UInt64, Single e Decimal sono obbligati a essere Double.  Tutti gli altri tipi sono obbligati a essere uno String usando il metodo `ToString`.  
  
#### Per usare il parametro XSLT, è necessario:  
  
1.  Creare un <xref:System.Xml.Xsl.XsltArgumentList> e aggiungere gli oggetti usando <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>.  
  
2.  Richiamare i parametri dal foglio di stile.  
  
3.  Passare l'oggetto <xref:System.Xml.Xsl.XsltArgumentList> al metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A> .  
  
### Esempio  
 Nell'esempio seguente il metodo <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> viene usato per contenere una data di sconto calcolato.  La data di sconto è calcolata dopo 20 giorni dalla data dell'ordine.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public class Sample  
  
   Private Const filename As String = "order.xml"  
   Private Const stylesheet As String = "discount.xsl"  
  
   Public Shared Sub Main()  
  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XsltArgumentList.  
    Dim xslArg As XsltArgumentList = New XsltArgumentList  
  
    'Calculate the discount date.  
    Dim today As DateTime = DateTime.Now  
    Dim d As DateTime = today.AddDays(20)  
    xslArg.AddParam("discount", "", d.ToString())  
  
    'Create an XmlTextWriter to handle the output.  
    Dim writer As XmlTextWriter = New XmlTextWriter("orderout.xml", Nothing)  
  
    'Transform the file.  
    xslt.Transform(doc, xslArg, writer, Nothing)  
  
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
   private const String filename = "order.xml";  
   private const String stylesheet = "discount.xsl";  
  
   public static void Main() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XsltArgumentList.  
    XsltArgumentList xslArg = new XsltArgumentList();  
  
    //Calculate the discount date.  
    DateTime today = DateTime.Now;  
    DateTime d = today.AddDays(20);  
    xslArg.AddParam("discount", "", d.ToString());  
  
    //Create an XmlTextWriter to handle the output.  
    XmlTextWriter writer = new XmlTextWriter("orderout.xml", null);  
  
    //Transform the file.  
    xslt.Transform(doc, xslArg, writer, null);  
    writer.Close();  
  }  
}  
```  
  
### Input  
 order.xml  
  
```  
<!--Represents a customer order-->  
<order>  
  <book ISBN='10-861003-324'>  
    <title>The Handmaid's Tale</title>  
    <price>19.95</price>  
  </book>  
  <cd ISBN='2-3631-4'>  
    <title>Americana</title>  
    <price>16.95</price>  
  </cd>  
</order>  
```  
  
 discount.xsl  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
  <xsl:param name="discount"/>  
  <xsl:template match="/">  
    <order>  
      <xsl:variable name="sub-total" select="sum(//price)"/>  
      <total><xsl:value-of select="$sub-total"/></total>  
      15% discount if paid by: <xsl:value-of select="$discount"/>  
    </order>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
### Output  
  
```  
<order>  
   <total>36.9</total>   
   15% discount if paid by: 5/6/2001 5:01:15 PM   
</order>  
```  
  
## Oggetti di estensione XSLT  
 Gli oggetti di estensione XSLT vengono aggiunti all'elenco <xref:System.Xml.Xsl.XsltArgumentList> usando il metodo <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>.  Un nome completo e un URI dello spazio dei nomi sono associati all'oggetto di estensione in quel momento.  
  
 Quando un oggetto viene aggiunto, il chiamante del metodo <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> deve essere completamente attendibile secondo il criterio di sicurezza.  Se il chiamante è di tipo semi\-trusted, l'aggiunta avrà esito negativo.  
  
 Anche se un oggetto viene aggiunto correttamente, questo non significa che l'esecuzione avverrà correttamente.  Quando viene chiamato il metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A>, le autorizzazioni vengono calcolate in base all'evidenza fornita nella fase <xref:System.Xml.Xsl.XslTransform.Load%2A> e il set di autorizzazioni viene assegnato all'intero processo di trasformazione.  Se un oggetto di estensione tenta di avviare un'azione che necessita di autorizzazioni non presenti nel set, viene generata un'eccezione.  
  
 Dagli oggetti di estensione vengono restituiti dati appartenenti a uno dei quattro tipi di dati XPath principali, e cioè number, string, boolean o node set.  
  
#### Per usare l'oggetto di estensione XSLT, è necessario:  
  
1.  Creare un <xref:System.Xml.Xsl.XsltArgumentList> e aggiungere l'oggetto di estensione usando <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A>.  
  
2.  Richiamare l'oggetto di estensione dal foglio di stile.  
  
3.  Passare l'oggetto <xref:System.Xml.Xsl.XsltArgumentList> al metodo <xref:System.Xml.Xsl.XslTransform.Transform%2A> .  
  
### Esempio  
 Nell'esempio seguente viene calcolata la circonferenza di un cerchio di cui viene fornito il raggio.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public Class Sample  
   Private Const filename As String = "number.xml"  
   Private Const stylesheet As String = "circle.xsl"  
  
   Public Shared Sub Main()  
        Dim test As Sample = New Sample  
   End Sub  
  
  Public Sub New()  
    'Create the XslTransform and load the style sheet.  
    Dim xslt As XslTransform = New XslTransform  
    xslt.Load(stylesheet)  
  
    'Load the XML data file.  
    Dim doc As XPathDocument = New XPathDocument(filename)  
  
    'Create an XsltArgumentList.  
    Dim xslArg As XsltArgumentList = New XsltArgumentList  
  
    'Add an object to calculate the circumference of the circle.  
    Dim obj As Calculate = New Calculate  
    xslArg.AddExtensionObject("urn:myObj", obj)  
  
    'Create an XmlTextWriter to output to the console.  
    Dim writer As XmlTextWriter = New XmlTextWriter(Console.Out)  
  
    'Transform the file.  
    xslt.Transform(doc, xslArg, writer, Nothing)  
    writer.Close()  
  
  End Sub  
  
  'Calculates the circumference of a circle given the radius.  
  Public Class Calculate  
  
    Private circ As double = 0  
  
    Public Function Circumference(radius As Double) As Double  
       circ = Math.PI*2*radius  
       Return circ  
    End Function  
  End Class  
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
   private const String stylesheet = "circle.xsl";  
  
   public static void Main() {  
  
        Sample test = new Sample();  
    }  
  
  public Sample() {  
  
    //Create the XslTransform and load the style sheet.  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
  
    //Load the XML data file.  
    XPathDocument doc = new XPathDocument(filename);  
  
    //Create an XsltArgumentList.  
    XsltArgumentList xslArg = new XsltArgumentList();  
  
    //Add an object to calculate the circumference of the circle.  
    Calculate obj = new Calculate();  
    xslArg.AddExtensionObject("urn:myObj", obj);  
  
    //Create an XmlTextWriter to output to the console.  
    XmlTextWriter writer = new XmlTextWriter(Console.Out);  
  
    //Transform the file.  
    xslt.Transform(doc, xslArg, writer, null);  
    writer.Close();  
  
  }  
  
  //Calculates the circumference of a circle given the radius.  
  public class Calculate{  
  
    private double circ = 0;  
  
    public double Circumference(double radius){  
       circ = Math.PI*2*radius;  
       return circ;  
    }  
  }  
}  
```  
  
### Input  
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
  
 circle.xsl  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
    xmlns:myObj="urn:myObj">  
  
  <xsl:template match="data">  
  <circles>  
  <xsl:for-each select="circle">  
    <circle>  
    <xsl:copy-of select="node()"/>  
       <circumference>  
          <xsl:value-of select="myObj:Circumference(radius)"/>          
       </circumference>  
    </circle>  
  </xsl:for-each>  
  </circles>  
  </xsl:template>  
</xsl:stylesheet>  
```  
  
### Output  
 `<circles xmlns:myObj="urn:myObj">`  
  
 `<circle>`  
  
 `<radius>12</radius>`  
  
 `<circumference>75.398223686155</circumference>`  
  
 `</circle>`  
  
 `<circle>`  
  
 `<radius>37.5</radius>`  
  
 `<circumference>235.61944901923448</circumference>`  
  
 `</circle>`  
  
 `</circles>`  
  
## Vedere anche  
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)