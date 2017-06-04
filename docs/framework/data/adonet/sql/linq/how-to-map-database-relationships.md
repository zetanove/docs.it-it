---
title: "Procedura: eseguire il mapping delle relazioni di database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 538def39-8399-46fb-b02d-60ede4e050af
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: eseguire il mapping delle relazioni di database
Qualsiasi relazione tra i dati, che rimane prevedibilmente sempre la stessa, può essere codificata come riferimenti alla proprietà nella classe di entità.  Nel database di esempio Northwind, ad esempio, poiché in genere i clienti effettuano ordini, nel modello è sempre presente una relazione tra clienti e ordini.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene definito un attributo <xref:System.Data.Linq.Mapping.AssociationAttribute> per consentire di rappresentare tali relazioni.  Questo attributo viene usato insieme ai tipi <xref:System.Data.Linq.EntitySet%601> e <xref:System.Data.Linq.EntityRef%601> per rappresentare quello che in un database sarebbe una relazione di chiave esterna. Per altre informazioni, vedere la sezione relativa all'attributo Association di [Mapping basato su attributi](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md).  
  
> [!NOTE]
>  I valori delle proprietà di archiviazione AssociationAttribute e ColumnAttribute rispettano la distinzione tra maiuscole e minuscole.  Verificare, ad esempio, che per i valori dell'attributo della proprietà AssociationAttribute.Storage venga usata la stessa combinazione di maiuscole e minuscole adoperata per i nomi di proprietà corrispondenti usati in altri punti del codice.  Ciò si applica a tutti i linguaggi di programmazione .NET, anche a quelli che in genere non distinguono tra maiuscole e minuscole, tra cui [!INCLUDE[vb_current_short](../../../../../../includes/vb-current-short-md.md)].  Per altre informazioni sulla proprietà di archiviazione, vedere <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=fullName>.  
  
 La maggior parte delle relazioni è di tipo uno\-a\-molti, come nell'esempio riportato più avanti in questo argomento.  È anche possibile rappresentare relazioni uno\-a\-uno e molti\-a\-molti come segue:  
  
-   Uno\-a\-uno: per rappresentare questo tipo di relazione includere <xref:System.Data.Linq.EntitySet%601> su entrambi i lati.  
  
     Ad esempio, si consideri una relazione `Customer`\-`SecurityCode` creata in modo che il codice di sicurezza del cliente non venga trovato nella tabella `Customer` e a cui solo le persone autorizzate possano accedere.  
  
-   Molti\-a\-molti: in questo tipo di relazioni la chiave primaria della tabella di *collegamento* è spesso formata da una combinazione di chiavi esterne delle altre due tabelle.  
  
     Ad esempio, si consideri una relazione molti\-a\-molti `Employee`\-`Project` creata usando la classe `EmployeeProject` della tabella di collegamento.  In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è necessario che tale relazione venga modellata usando tre classi:`Employee`, `Project` e `EmployeeProject`.  In questo caso la modifica della relazione tra `Employee` e `Project` può apparentemente richiedere un aggiornamento della chiave primaria di `EmployeeProject`.  In questa situazione, tuttavia, è preferibile modellare la relazione eliminando una classe `EmployeeProject` esistente e creando una nuova classe `EmployeeProject`.  
  
    > [!NOTE]
    >  Le relazioni nei database relazionali vengono in genere modellate come valori di chiave esterna che fanno riferimento a chiavi primarie in altre tabelle.  Per spostarsi tra di esse, associare in modo esplicito le due tabelle usando un'operazione di *join* relazionale.  
    >   
    >  Gli oggetti in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], d'altra parte, fanno riferimento reciproco usando riferimenti alle proprietà o raccolte di riferimenti in cui è possibile spostarsi usando la notazione del *punto*.  
  
## Esempio  
 Nell'esempio uno\-a\-molti seguente, alla classe `Customer` è associata una proprietà che dichiara la relazione tra clienti e ordini.  La proprietà `Orders` è di tipo <xref:System.Data.Linq.EntitySet%601>.  Questo tipo significa che si tratta di una relazione uno\-a\-molti \(un cliente a molti ordini\).  La proprietà <xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A> viene usata per descrivere come viene eseguita questa associazione, ovvero specificando il nome della proprietà nella classe correlata che dovrà essere confrontata con questa.  In questo esempio viene confrontata la proprietà `CustomerID`, esattamente come verrebbe confrontato il valore di tale colonna con un'operazione *join* in un database.  
  
> [!NOTE]
>  Se si usa [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], è possibile adoperare [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per creare un'associazione tra classi.  
  
 [!code-csharp[DlinqCustomize#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#3)]
 [!code-vb[DlinqCustomize#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#3)]  
  
## Esempio  
 È anche possibile invertire la situazione.  Anziché usare la classe `Customer` per descrivere l'associazione tra clienti e ordini, è possibile usare la classe `Order`.  La classe `Order` usa il tipo <xref:System.Data.Linq.EntityRef%601> per descrivere la relazione con la classe Customer, come nell'esempio di codice seguente.  
  
> [!NOTE]
>  La classe <xref:System.Data.Linq.EntityRef%601> supporta il *caricamento posticipato*.  Per altre informazioni, *vedere* [Caricamento rinviato e immediato](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md).  
  
 [!code-csharp[DLinqCustomize#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#5)]
 [!code-vb[DLinqCustomize#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#5)]  
  
## Vedere anche  
 [Procedura: personalizzare le classi di entità mediante l'editor di codice](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)   
 [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)