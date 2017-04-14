---
title: "Propriet&#224; di dipendenza | Microsoft Docs"
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
ms.assetid: 212cfb1e-cec4-4047-94a6-47209b387f6f
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Propriet&#224; di dipendenza
Una proprietà di dipendenza \(DP\) è una proprietà normale che archivia il valore in un archivio di proprietà anziché archiviare i dati in una variabile di tipo \(campo\), ad esempio.  
  
 Una proprietà di dipendenza collegata è un tipo di proprietà di dipendenza modellate come metodi statici di Get e Set che rappresenta "proprietà" descrizione delle relazioni tra oggetti e i relativi contenitori \(ad esempio, la posizione di un `Button` dell'oggetto su un `Panel` contenitore\).  
  
 **✓ si** forniscono le proprietà di dipendenza, se occorre le proprietà per supportare le funzionalità WPF come stile, trigger, associazione dati, animazioni, le risorse dinamiche e l'ereditarietà.  
  
## Progettazione di proprietà di dipendenza  
 **✓ si** ereditare da <xref:System.Windows.DependencyObject>, o uno dei relativi sottotipi, quando si implementa le proprietà di dipendenza. Il tipo fornisce un'implementazione estremamente efficiente di un archivio di proprietà e l'associazione dati WPF sono automaticamente supportati.  
  
 **✓ si** forniscono una normale proprietà CLR e un campo statico pubblico di sola lettura e l'archiviazione di un'istanza di <xref:System.Windows.DependencyProperty?displayProperty=fullName> per ogni proprietà di dipendenza.  
  
 **✓ si** implementare le proprietà di dipendenza chiamando i metodi di istanza <xref:System.Windows.DependencyObject.GetValue%2A?displayProperty=fullName> e <xref:System.Windows.DependencyObject.SetValue%2A?displayProperty=fullName>.  
  
 **✓ si** nome di campo statico di proprietà di dipendenza aggiungendo il nome della proprietà con "Proprietà".  
  
 **X non** impostare i valori predefiniti delle proprietà di dipendenza in modo esplicito nel codice; impostarle nei metadati.  
  
 Se si imposta un valore predefinito di proprietà in modo esplicito, si potrebbe non tale proprietà viene impostata in modo implicito, ad esempio un'applicazione di stili.  
  
 **X non** inserire il codice nelle funzioni di proprietà accesso diverso da quello standard per accedere al campo statico.  
  
 Che il codice non eseguito se la proprietà è impostata in modo implicito, ad esempio un'applicazione di stili, poiché l'applicazione di stili, il campo statico viene utilizzato direttamente.  
  
 **X non** utilizzare le proprietà di dipendenza per memorizzare dati protetti. Le proprietà di dipendenza anche privati sono accessibili pubblicamente.  
  
## Progettazione di proprietà di dipendenza collegata  
 Le proprietà di dipendenza descritte nella sezione precedente rappresentano le proprietà intrinseche del tipo dichiarante. ad esempio, il `Text` è una proprietà del `TextButton`, che la dichiara. Un tipo speciale di proprietà di dipendenza è la proprietà di dipendenza associata.  
  
 Un esempio classico di una proprietà associata è la <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=fullName> proprietà. La proprietà rappresenta la posizione di colonna del pulsante \(non della griglia\), ma risulta rilevante solo se il pulsante è contenuto in una griglia, quindi è "connesso" a pulsanti da griglie.  
  
```  
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition />  
        <ColumnDefinition />  
    </Grid.ColumnDefinitions>  
  
    <Button Grid.Column="0">Click</Button>  
    <Button Grid.Column="1">Clack</Button>  
</Grid>  
```  
  
 La definizione di una proprietà associata è principalmente simile a quella di una proprietà di dipendenza normale, ad eccezione del fatto che le funzioni di accesso sono rappresentate dai metodi Get e Set statici:  
  
```  
public class Grid {  
  
    public static int GetColumn(DependencyObject obj) {  
        return (int)obj.GetValue(ColumnProperty);  
    }  
  
    public static void SetColumn(DependencyObject obj, int value) {  
        obj.SetValue(ColumnProperty,value);  
    }  
  
    public static readonly DependencyProperty ColumnProperty =  
        DependencyProperty.RegisterAttached(  
            "Column",  
            typeof(int),  
            typeof(Grid)  
    );  
}  
```  
  
## Convalida delle proprietà di dipendenza  
 Proprietà implementano spesso il cosiddetto convalida. La logica di convalida viene eseguita quando viene effettuato un tentativo di modificare il valore di una proprietà.  
  
 Purtroppo accesso della proprietà di dipendenza non può contenere codice di convalida arbitraria. Al contrario, logica di convalida di proprietà di dipendenza deve essere specificata durante la registrazione di proprietà.  
  
 **X non** inserire logica di convalida di proprietà di dipendenza in funzioni di accesso della proprietà. Al contrario, passare un callback di convalida per `DependencyProperty.Register` metodo.  
  
## Notifiche di modifica proprietà di dipendenza  
 **X non** implementare la logica di notifica di modifica nell'accesso della proprietà di dipendenza. Le proprietà di dipendenza sono una funzionalità di notifiche di modifica incorporate che deve essere utilizzata specificando un callback di notifica di modifica per il <xref:System.Windows.PropertyMetadata>.  
  
## Coercizione del valore di proprietà di dipendenza  
 Coercizione di proprietà viene eseguita quando il valore assegnato a un setter delle proprietà viene modificato da setter prima che venga effettivamente modificata l'archivio delle proprietà.  
  
 **X non** implementare la logica di coercizione nell'accesso della proprietà di dipendenza.  
  
 Le proprietà di dipendenza sono una funzionalità di coercizione incorporata e può essere utilizzato specificando un callback di coercizione di `PropertyMetadata`.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Modelli di progettazione comuni](../../../docs/standard/design-guidelines/common-design-patterns.md)