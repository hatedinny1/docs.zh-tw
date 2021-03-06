---
title: "移除項目、 屬性和節點從 XML 樹狀結構 (Visual Basic) |Microsoft 文件"
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
ms.assetid: 5cf21919-4360-4b49-b29d-58ea3164ac72
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: eef13476733f7c883080923614683a41d7cb3b3a
ms.lasthandoff: 03/13/2017


---
# <a name="removing-elements-attributes-and-nodes-from-an-xml-tree-visual-basic"></a>移除項目、 屬性和節點從 XML 樹狀結構 (Visual Basic)
您可以修改 XML 樹狀以移除項目、屬性以及其他類型的節點。  
  
 從 XML 文件移除單一項目或單一屬性很直接。 不過，移除項目或屬性的集合時，您應該先將集合具體化到清單中，然後從清單中刪除項目或屬性。 最好的方法是使用<xref:System.Xml.Linq.Extensions.Remove%2A>擴充方法，將您執行此工作。</xref:System.Xml.Linq.Extensions.Remove%2A>  
  
 這麼做的主要原因是因為您從 XML 樹狀結構中擷取的大部分集合都是使用延後執行產生的。 如果您沒有先將這些集合具體化到清單中，或沒有使用擴充方法，則可能發生特定類別的 Bug。 如需詳細資訊，請參閱[混合宣告式程式碼/命令式程式碼 Bug (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/mixed-declarative-code-imperative-code-bugs-linq-to-xml.md)。  
  
 下列方法會從 XML 樹狀移除節點和屬性。  
  
|方法|描述|  
|------------|-----------------|  
|[XAttribute.Remove](https://msdn.microsoft.com/library/system.xml.linq.xattribute.remove\(v=vs.110\).aspx)|移除<xref:System.Xml.Linq.XAttribute>從其父代。</xref:System.Xml.Linq.XAttribute>|  
|[XContainer.RemoveNodes](https://msdn.microsoft.com/library/system.xml.linq.xcontainer.removenodes\(v=vs.110\).aspx)|從<xref:System.Xml.Linq.XContainer>.</xref:System.Xml.Linq.XContainer>移除子節點|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName>|從<xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>移除內容和屬性|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName>|移除<xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>屬性|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName>|如果您針對值傳遞 `null`，則會移除屬性。|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName>|如果您針對值傳遞 `null`，則會移除子項目。|  
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=fullName>|移除<xref:System.Xml.Linq.XNode>從其父代。</xref:System.Xml.Linq.XNode>|  
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=fullName></xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=fullName>|從其父項目移除來源集合中的每個屬性或項目。|  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 這個範例會示範三種移除項目的方法。 首先，它會移除單一項目。 第二，它會擷取項目的集合，具體化它們使用<xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>運算子，並將集合中移除。</xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName> 最後，它會擷取項目的集合，並將其移除使用<xref:System.Xml.Linq.Extensions.Remove%2A>擴充方法。</xref:System.Xml.Linq.Extensions.Remove%2A>  
  
 如需有關<xref:System.Linq.Enumerable.ToList%2A>運算子，請參閱[轉換資料類型 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)。</xref:System.Linq.Enumerable.ToList%2A>  
  
### <a name="code"></a>程式碼  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <Child1>  
            <GrandChild1/>  
            <GrandChild2/>  
            <GrandChild3/>  
        </Child1>  
        <Child2>  
            <GrandChild4/>  
            <GrandChild5/>  
            <GrandChild6/>  
        </Child2>  
        <Child3>  
            <GrandChild7/>  
            <GrandChild8/>  
            <GrandChild9/>  
        </Child3>  
    </Root>  
root.<Child1>.<GrandChild1>.Remove()  
root.<Child2>.Elements().ToList().Remove()  
root.<Child3>.Elements().Remove()  
Console.WriteLine(root)  
  
```  
  
### <a name="comments"></a>註解  
 此程式碼會產生下列輸出：  
  
```xml  
<Root>  
  <Child1>  
    <GrandChild2 />  
    <GrandChild3 />  
  </Child1>  
  <Child2 />  
  <Child3 />  
</Root>  
```  
  
 請注意，第一個後代子項目已從 `Child1` 移除。 所有後代子項目都已經從 `Child2` 和 `Child3` 移除。  
  
## <a name="see-also"></a>另請參閱  
 [修改 XML 樹狀結構 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
