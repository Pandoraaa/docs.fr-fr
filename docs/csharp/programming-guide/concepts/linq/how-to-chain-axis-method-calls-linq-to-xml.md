---
title: Guide pratique pour chaîner des appels à des méthodes d’axe (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 067e6da2-ee32-486d-803c-e611b328e39a
ms.openlocfilehash: b486ef5cbf1f9752077cfa8d774184c7be90f6f2
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2018
ms.locfileid: "44212098"
---
# <a name="how-to-chain-axis-method-calls-linq-to-xml-c"></a>Guide pratique pour chaîner des appels à des méthodes d’axe (LINQ to XML) (C#)
Un schéma courant que vous utiliserez dans votre code consiste à appeler une méthode d’axe, puis à appeler l’un des axes de méthode d’extension.  
  
 Il existe deux axes avec le nom `Elements` qui retournent une collection d'éléments : la méthode <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> et la méthode <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType>. Vous pouvez combiner ces deux axes pour rechercher tous les éléments d’un nom spécifié à une profondeur donnée dans l’arborescence.  
  
## <a name="example"></a>Exemple  
 Cet exemple utilise <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> et <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> pour rechercher tous les éléments `Name` dans tous les éléments `Address` de tous les éléments `PurchaseOrder`.  
  
 Cet exemple utilise le document XML suivant : [Exemple de fichier XML : Plusieurs commandes fournisseur (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
```csharp  
XElement purchaseOrders = XElement.Load("PurchaseOrders.xml");  
IEnumerable<XElement> names =  
    from el in purchaseOrders  
        .Elements("PurchaseOrder")  
        .Elements("Address")  
        .Elements("Name")  
    select el;  
foreach (XElement e in names)  
    Console.WriteLine(e);  
```  
  
 Cet exemple génère la sortie suivante :  
  
```xml  
<Name>Ellen Adams</Name>  
<Name>Tai Yee</Name>  
<Name>Cristian Osorio</Name>  
<Name>Cristian Osorio</Name>  
<Name>Jessica Arnold</Name>  
<Name>Jessica Arnold</Name>  
```  
  
 Cela fonctionne car l'une des implémentations de l'axe `Elements` est en tant que méthode d'extension sur l'objet <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XContainer>. <xref:System.Xml.Linq.XElement> dérivant de <xref:System.Xml.Linq.XContainer>, vous pouvez appeler la méthode <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> sur les résultats d'un appel à la méthode <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>.  
  
## <a name="example"></a>Exemple  
 Quelquefois, vous souhaitez récupérer tous les éléments à une profondeur d'élément spécifique lorsqu'il peut y avoir ou ne pas y avoir d'ancêtres intermédiaires. Par exemple, dans le document suivant, vous pourriez souhaiter récupérer tous les éléments `ConfigParameter` qui sont des enfants de l'élément `Customer`, mais pas le `ConfigParameter` qui est un enfant de l'élément `Root`.  
  
```xml  
<Root>  
  <ConfigParameter>RootConfigParameter</ConfigParameter>  
  <Customer>  
    <Name>Frank</Name>  
    <Config>  
      <ConfigParameter>FirstConfigParameter</ConfigParameter>  
    </Config>  
  </Customer>  
  <Customer>  
    <Name>Bob</Name>  
    <!--This customer doesn't have a Config element-->  
  </Customer>  
  <Customer>  
    <Name>Bill</Name>  
    <Config>  
      <ConfigParameter>SecondConfigParameter</ConfigParameter>  
    </Config>  
  </Customer>  
</Root>  
```  
  
 Pour cela, vous pouvez utiliser l'axe <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> comme suit :  
  
```csharp  
XElement root = XElement.Load("Irregular.xml");  
IEnumerable<XElement> configParameters =   
    root.Elements("Customer").Elements("Config").  
    Elements("ConfigParameter");  
foreach (XElement cp in configParameters)  
    Console.WriteLine(cp);  
```  
  
 Cet exemple génère la sortie suivante :  
  
```xml  
<ConfigParameter>FirstConfigParameter</ConfigParameter>  
<ConfigParameter>SecondConfigParameter</ConfigParameter>  
```  
  
## <a name="example"></a>Exemple  
 L'exemple suivant illustre la même technique pour du code XML qui est dans un espace de noms. Pour plus d’informations, consultez [Utilisation des espaces de noms XML (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
 Cet exemple utilise le document XML suivant : [Exemple de fichier XML : Plusieurs commandes fournisseur dans un espace de noms](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-in-a-namespace.md).  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement purchaseOrders = XElement.Load("PurchaseOrdersInNamespace.xml");  
IEnumerable<XElement> names =  
    from el in purchaseOrders  
        .Elements(aw + "PurchaseOrder")  
        .Elements(aw + "Address")  
        .Elements(aw + "Name")  
    select el;  
foreach (XElement e in names)  
    Console.WriteLine(e);  
```  
  
 Cet exemple génère la sortie suivante :  
  
```xml  
<aw:Name xmlns:aw="http://www.adventure-works.com">Ellen Adams</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Tai Yee</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Cristian Osorio</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Cristian Osorio</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Jessica Arnold</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Jessica Arnold</aw:Name>  
```  
  
## <a name="see-also"></a>Voir aussi

- [Axes LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)
