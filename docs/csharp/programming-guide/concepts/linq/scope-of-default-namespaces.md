---
title: "C# 中的預設命名空間範圍1 | Microsoft Docs"
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
ms.assetid: fe826236-830f-457a-9027-7ad62c909fae
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 760716dc81f5cd946ae014ed22b6c5a7df64a5dd
ms.lasthandoff: 03/13/2017

---
# <a name="scope-of-default-namespaces-in-c"></a>C 中的預設命名空間範圍#
在 XML 樹狀結構中表示的預設命名空間不在查詢的範圍內。 如果您擁有的 XML 位於預設命名空間中，則仍然必須宣告 <xref:System.Xml.Linq.XNamespace> 變數，然後將它與區域名稱結合，讓限定名稱得以用於查詢中。  
  
 查詢 XML 時所遇到的其中一個最常見的問題是，如果 XML 樹狀結構有預設的命名空間，即使 XML 不在命名空間中，開發人員有時候還是會撰寫查詢。  
  
 本主題中的第一組範例會顯示載入預設命名空間中的 XML 但查詢錯誤的常見方式。  
  
 第二組範例顯示所需的修正，讓您可以在命名空間中查詢 XML。  
  
## <a name="example"></a>範例  
 此範例顯示在命名空間中建立 XML，以及傳回空結果集的查詢。  
  
### <a name="code"></a>程式碼  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements("Child")  
    select el;  
Console.WriteLine("Result set follows:");  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
Console.WriteLine("End of result set");  
```  
  
### <a name="comments"></a>註解  
 此範例會產生下列結果：  
  
```  
Result set follows:  
End of result set  
```  
  
## <a name="example"></a>範例  
 此範例顯示在命名空間中建立 XML，以及編碼正確的查詢。  
  
 相較於上述編碼錯誤的範例，使用 C# 時的正確方法為宣告與初始化 <xref:System.Xml.Linq.XNamespace> 物件，並在指定 <xref:System.Xml.Linq.XName> 物件時使用它。 在本例中，<xref:System.Xml.Linq.XElement.Elements%2A> 的引數是 <xref:System.Xml.Linq.XName> 物件。  
  
### <a name="code"></a>程式碼  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
XNamespace aw = "http://www.adventure-works.com";  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
Console.WriteLine("Result set follows:");  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
Console.WriteLine("End of result set");  
```  
  
### <a name="comments"></a>註解  
 此範例會產生下列結果：  
  
```  
Result set follows:  
1  
2  
3  
End of result set  
```  
  
## <a name="see-also"></a>另請參閱  
 [處理 XML 命名空間 (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)
