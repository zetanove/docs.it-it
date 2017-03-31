---
title: 'Procedura: Controllare il tipo di una proiezione (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: e4db6b7e-4cc9-4c8f-af85-94acf32aa348
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 465a04338de0a092bf60e15ce07a9aace160bbe3
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-control-the-type-of-a-projection-c"></a>Procedura: Controllare il tipo di una proiezione (C#)
Per proiezione si intende il processo in cui un unico set di dati viene accettato e filtrato, ne viene cambiata la forma e persino il tipo. Le proiezioni vengono eseguite nella maggior parte delle espressioni di query. Quasi tutte le espressioni di query illustrate in questa sezione restituiscono <xref:System.Collections.Generic.IEnumerable%601> di <xref:System.Xml.Linq.XElement>. Tuttavia è possibile controllare il tipo della proiezione per creare raccolte di altri tipi. In questo argomento viene illustrato come eseguire questa operazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene definito un nuovo tipo `Customer`. L'espressione di query crea quindi un'istanza per nuovi oggetti `Customer` nella clausola `Select`. In questo modo il tipo dell'espressione di query sarà <xref:System.Collections.Generic.IEnumerable%601> di `Customer`.  
  
 Questo esempio usa il documento XML seguente: [File XML di esempio: clienti e ordini (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
```csharp  
public class Customer  
{  
    private string customerID;  
    public string CustomerID{ get{return customerID;} set{customerID = value;}}  
  
    private string companyName;  
    public string CompanyName{ get{return companyName;} set{companyName = value;}}  
  
    private string contactName;  
    public string ContactName { get{return contactName;} set{contactName = value;}}  
  
    public Customer(string customerID, string companyName, string contactName)  
    {  
        CustomerID = customerID;  
        CompanyName = companyName;  
        ContactName = contactName;  
    }  
  
    public override string ToString()  
    {  
        return String.Format("{0}:{1}:{2}", this.customerID, this.companyName, this.contactName);  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        XElement custOrd = XElement.Load("CustomersOrders.xml");  
        IEnumerable<Customer> custList =  
            from el in custOrd.Element("Customers").Elements("Customer")  
            select new Customer(  
                (string)el.Attribute("CustomerID"),  
                (string)el.Element("CompanyName"),  
                (string)el.Element("ContactName")  
            );  
        foreach (Customer cust in custList)  
            Console.WriteLine(cust);  
    }  
}  
```  
  
 L'output del codice è il seguente:  
  
```  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable.Select%2A>   
 [Projections and Transformations (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md) (Proiezioni e trasformazioni (LINQ to XML) (C#))
