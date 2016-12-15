---
title: "Funzioni matematiche (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "funzioni matematiche, Visual Basic"
  - "operazioni aritmetiche, funzioni matematiche"
  - "routine matematiche"
  - "Atn (funzione)"
ms.assetid: 4d2d82e7-6924-42fe-a4a7-b4dd5bebbd0c
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Funzioni matematiche (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I metodi della classe di <xref:System.Math?displayProperty=fullName> forniscono funzioni matematiche trigonometriche, logaritmiche e altre comuni.  
  
## Note  
 I metodi seguenti elenchi della tabella di <xref:System.Math?displayProperty=fullName> classe.  È possibile utilizzare questi in un programma Visual Basic.  
  
|Metodo di .NET Framework|Descrizione|  
|------------------------------|-----------------|  
|<xref:System.Math.Abs%2A>|Restituisce il valore assoluto di un numero.|  
|<xref:System.Math.Acos%2A>|Restituisce l'angolo il cui coseno è il numero specificato.|  
|<xref:System.Math.Asin%2A>|Restituisce l'angolo il cui seno è il numero specificato.|  
|<xref:System.Math.Atan%2A>|Restituisce l'angolo la cui tangente è il numero specificato.|  
|<xref:System.Math.Atan2%2A>|Restituisce l'angolo la cui tangente è il quoziente di due numeri specificati.|  
|<xref:System.Math.BigMul%2A>|Restituisce il prodotto completo di due numeri a 32 bit.|  
|<xref:System.Math.Ceiling%2A>|Restituisce il valore integrale più piccolo che sia maggiore o uguale a `Decimal` specificato o `Double`.|  
|<xref:System.Math.Cos%2A>|Restituisce il coseno dell'angolo specificato.|  
|<xref:System.Math.Cosh%2A>|Restituisce il coseno iperbolico dell'angolo specificato.|  
|<xref:System.Math.DivRem%2A>|Restituisce il quoziente di due 32 bit o interi con segno a 64 bit e restituisce il resto in un parametro di output.|  
|<xref:System.Math.Exp%2A>|Restituisce e \(la base dei logaritmi naturali\) viene generato a potenza specificata.|  
|<xref:System.Math.Floor%2A>|Restituisce il numero intero massimo che sia minore o uguale a `Decimal` o il numero specificato di `Double`.|  
|<xref:System.Math.IEEERemainder%2A>|Restituisce il resto derivante dalla divisione di un numero specificato da un altro numero specificato.|  
|<xref:System.Math.Log%2A>|Restituisce il logaritmo naturale di edi base\) di un determinato numero o il logaritmo di un numero specificato di base specificato.|  
|<xref:System.Math.Log10%2A>|Restituisce il logaritmo di base 10 del numero specificato.|  
|<xref:System.Math.Max%2A>|Restituisce il maggiore di due numeri.|  
|<xref:System.Math.Min%2A>|Restituisce il meno elevato tra due numeri.|  
|<xref:System.Math.Pow%2A>|Restituisce il numero specificato elevato alla potenza specificata.|  
|<xref:System.Math.Round%2A>|Restituisce un valore di `Double` o di `Decimal` arrotondato al valore integrale o più vicino a un determinato numero di cifre frazionarie.|  
|<xref:System.Math.Sign%2A>|Restituisce un valore `Integer` che indica il segno di un numero.|  
|<xref:System.Math.Sin%2A>|Restituisce il seno dell'angolo specificato.|  
|<xref:System.Math.Sinh%2A>|Restituisce il seno iperbolico dell'angolo specificato.|  
|<xref:System.Math.Sqrt%2A>|Restituisce la radice quadrata del numero specificato.|  
|<xref:System.Math.Tan%2A>|Restituisce la tangente dell'angolo specificato.|  
|<xref:System.Math.Tanh%2A>|Restituisce la tangente iperbolica dell'angolo specificato.|  
|<xref:System.Math.Truncate%2A>|Calcola la parte integrante di `Decimal` o il numero specificato di `Double`.|  
  
 Per utilizzare queste funzioni senza qualifica, importare lo spazio dei nomi di <xref:System.Math?displayProperty=fullName> nel progetto aggiungendo il seguente codice all'inizio del file di origine:  
  
```  
Imports System.Math  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Abs%2A> della classe <xref:System.Math> viene utilizzato per calcolare il valore assoluto di un numero:  
  
```  
' Returns 50.3.  
Dim MyNumber1 As Double = Math.Abs(50.3)  
' Returns 50.3.  
Dim MyNumber2 As Double = Math.Abs(-50.3)  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Atan%2A> della classe <xref:System.Math> viene utilizzato per calcolare il valore di pi:  
  
```  
Public Function GetPi() As Double  
    ' Calculate the value of pi.  
    Return 4.0 * Math.Atan(1.0)  
End Function  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Cos%2A> della classe <xref:System.Math> viene utilizzato per la restituzione del coseno di un angolo:  
  
```  
Public Function Sec(ByVal angle As Double) As Double  
    ' Calculate the secant of angle, in radians.  
    Return 1.0 / Math.Cos(angle)  
End Function  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Exp%2A> della classe <xref:System.Math> viene utilizzato per la restituzione di e elevato a potenza:  
  
```  
Public Function Sinh(ByVal angle As Double) As Double  
    ' Calculate hyperbolic sine of an angle, in radians.  
    Return (Math.Exp(angle) - Math.Exp(-angle)) / 2.0  
End Function  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Log%2A> della classe <xref:System.Math> viene utilizzato per la restituzione del logaritmo naturale di un numero:  
  
```  
Public Function Asinh(ByVal value As Double) As Double  
    ' Calculate inverse hyperbolic sine, in radians.  
    Return Math.Log(value + Math.Sqrt(value * value + 1.0))  
End Function  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Round%2A> della classe <xref:System.Math> viene utilizzato per arrotondare un numero al valore integer più vicino:  
  
```  
' Returns 3.  
Dim MyVar2 As Double = Math.Round(2.8)  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Sign%2A> della classe <xref:System.Math> viene utilizzato per determinare il segno di un numero:  
  
```  
' Returns 1.  
Dim MySign1 As Integer = Math.Sign(12)  
' Returns -1.  
Dim MySign2 As Integer = Math.Sign(-2.4)  
' Returns 0.  
Dim MySign3 As Integer = Math.Sign(0)  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Sin%2A> della classe <xref:System.Math> viene utilizzato per la restituzione del seno di un angolo:  
  
```  
Public Function Csc(ByVal angle As Double) As Double  
    ' Calculate cosecant of an angle, in radians.  
    Return 1.0 / Math.Sin(angle)  
End Function  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Sqrt%2A> della classe <xref:System.Math> viene utilizzato per calcolare la radice quadrata di un numero:  
  
```  
' Returns 2.  
Dim MySqr1 As Double = Math.Sqrt(4)  
' Returns 4.79583152331272.  
Dim MySqr2 As Double = Math.Sqrt(23)  
' Returns 0.  
Dim MySqr3 As Double = Math.Sqrt(0)  
' Returns NaN (not a number).  
Dim MySqr4 As Double = Math.Sqrt(-4)  
```  
  
## Esempio  
 Nell'esempio riportato di seguito il metodo <xref:System.Math.Tan%2A> della classe <xref:System.Math> viene utilizzato per la restituzione della tangente di un angolo:  
  
```  
Public Function Ctan(ByVal angle As Double) As Double  
    ' Calculate cotangent of an angle, in radians.  
    Return 1.0 / Math.Tan(angle)  
End Function  
```  
  
## Requisiti  
 **Classe:** <xref:System.Math>  
  
 **Spazio dei nomi:** <xref:System>  
  
 **Assembly:** mscorlib \(in mscorlib.dll\)  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.VBMath.Rnd%2A>   
 <xref:Microsoft.VisualBasic.VBMath.Randomize%2A>   
 <xref:System.Double.NaN>   
 [Derived Math Functions](../../../visual-basic/language-reference/keywords/derived-math-functions.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)