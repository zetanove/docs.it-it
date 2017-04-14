---
title: "Conversione delle stringhe in tipi di dati di .NET Framework | Microsoft Docs"
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
ms.assetid: 65455ef3-9120-412c-819b-d0f59f88ac09
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Conversione delle stringhe in tipi di dati di .NET Framework
Per convertire una stringa in un tipo di dati di .NET Framework, usare il metodo **XmlConvert** che soddisfa i requisiti dell'applicazione.  Per un elenco di tutti i metodi di conversione disponibili nella classe **XmlConvert**, vedere [Membri XmlConvert](frlrfSystemXmlXmlConvertMembersTopic).  
  
 La stringa restituita dal metodo **ToString** è una versione in formato stringa dei dati passati.  Esistono inoltre diversi tipi .NET Framework che consentono di eseguire la conversione usando la classe **XmlConvert**, ma che non consentono l'uso dei metodi della classe **System.Convert**.  La classe **XmlConvert** è conforme alla specifica dei tipi di dati XML Schema \(XSD\) e dispone di un tipo di dati su cui è possibile eseguire il mapping di **XmlConvert**.  
  
 Nella tabella seguente sono elencati i tipi di dati di .NET Framework e i tipi di stringa che vengono restituiti dal mapping dei tipi di dati XML Schema \(XSD\).  I tipi di .NET Framework non possono essere elaborati con **System.Convert**.  
  
|Tipo .NET Framework|Stringa restituita|  
|-------------------------|------------------------|  
|Boolean|"true", "false"|  
|Single.PositiveInfinity|"INF"|  
|Single.NegativeInfinity|"\-INF"|  
|Double.PositiveInfinity|"INF"|  
|Double.NegativeInfinity|"\-INF"|  
|DateTime|Il formato è "yyyy\-MM\-ddTHH:mm:sszzzzzz" e i relativi subset.|  
|TimeSpan|Il formato è PnYnMnTnHnMnS, ovvero `P2Y10M15DT10H30M20S` corrisponde a una durata di 2 anni, 10 mesi, 15 giorni, 10 ore, 30 minuti e 20 secondi.|  
  
> [!NOTE]
>  Se viene eseguita la conversione in una stringa di uno dei tipi di .NET Framework elencati nella tabella usando il metodo **ToString**, la stringa restituita non corrisponderà al tipo di base, ma al tipo di stringa XML Schema \(XSD\).  
  
 I tipi di valore **DateTime** e **TimeSpan** sono diversi in quanto **DateTime** rappresenta un istante nel tempo, mentre **TimeSpan** rappresenta un intervallo di tempo.  I formati **DateTime** e **TimeSpan** sono definiti nella specifica dei tipi di dati di XML Schema \(XSD\).  Ad esempio:  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim [date] As New DateTime(2001, 8, 4)  
writer.WriteElementString("Date", XmlConvert.ToString([date]))  
  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
DateTime date = new DateTime (2001, 08, 04);  
writer.WriteElementString("Date", XmlConvert.ToString(date));  
```  
  
 **Output**  
  
 `<Date>2001-08-04T00:00:00</Date>`.  
  
 Il codice seguente converte un numero intero in una stringa:  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim value As Int32 = 200  
writer.WriteElementString("Number", XmlConvert.ToString(value))  
  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
Int32 value = 200;  
writer.WriteElementString("Number", XmlConvert.ToString(value));  
```  
  
 **Output**  
  
 `<Number>200</Number>`  
  
 Tuttavia, se si converte una stringa in **Boolean**, **Single** o **Double**, il tipo di .NET Framework restituito non corrisponde al tipo restituito quando si usa la classe **System.Convert**.  
  
## Stringa in Boolean  
 Nella tabella seguente viene illustrato quale tipo viene generato per le stringhe di input fornite, quando si converte una stringa in **Boolean** usando il metodo **ToBoolean**.  
  
|Parametro di input della stringa valido|Tipo di output di .NET Framework|  
|---------------------------------------------|--------------------------------------|  
|"true"|Boolean.True|  
|"1"|Boolean.True|  
|"false"|Boolean.False|  
|"0"|Boolean.False|  
  
 Si consideri, ad esempio, il codice XML seguente:  
  
 **Input**  
  
```  
<Boolean>true</Boolean>  
<Boolean>1</Boolean>   
```  
  
 Entrambi possono essere interpretati correttamente dal codice seguente e **bvalue** corrisponde a **System.Boolean.True**:  
  
```vb  
Dim bvalue As Boolean = _  
   XmlConvert.ToBoolean(reader.ReadElementString())  
Console.WriteLine(bvalue)  
  
```  
  
```csharp  
Boolean bvalue = XmlConvert.ToBoolean(reader.ReadElementString());  
Console.WriteLine(bvalue);  
```  
  
## Stringa in Single  
 Nella tabella seguente viene illustrato quale tipo viene generato per le stringhe di input fornite, quando si converte una stringa in **Single** usando il metodo **ToSingle**.  
  
|Parametro di input della stringa valido|Tipo di output di .NET Framework|  
|---------------------------------------------|--------------------------------------|  
|"INF"|Single.PositiveInfinity|  
|"\-INF"|Single.NegativeInfinity|  
  
## Stringa in Double  
 Nella tabella seguente viene illustrato quale tipo viene generato per le stringhe di input fornite, quando si converte una stringa in **Single** usando il metodo **ToDouble**.  
  
|Parametro di input della stringa valido|Tipo di output di .NET Framework|  
|---------------------------------------------|--------------------------------------|  
|"INF"|Double.PositiveInfinity|  
|"\-INF"|Double.NegativeInfinity|  
  
 Il codice seguente scrive `<Infinity>INF</Infinity>`:  
  
```vb  
Dim value As Double = Double.PositiveInfinity  
writer.WriteElementString("Infinity", XmlConvert.ToString(value))  
  
```  
  
```csharp  
Double value = Double.PositiveInfinity;  
writer.WriteElementString("Infinity", XmlConvert.ToString(value));  
```  
  
## Vedere anche  
 [Conversione dei tipi di dati XML](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)   
 [Conversione dei tipi di .NET Framework in stringhe](../../../../docs/standard/data/xml/converting-dotnet-types-to-strings.md)