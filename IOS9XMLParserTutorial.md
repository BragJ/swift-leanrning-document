#IOS9XMLParserTutorial

##英文详见[here](https://developer.apple.com/reference/foundation/xmlparserdelegate)
```

func parserDidStartDocument(XMLParser)
Sent by the parser object to the delegate when it begins parsing a document.

```
这是起点，在这里执行初始化操作

```
func parserDidEndDocument(XMLParser)
Sent by the parser object to the delegate when it has successfully completed parsing.
```
这是终点，在这里处理数据

**fun1**

```
 func parser(_ parser: XMLParser, didStartElement elementName: String, namespaceURI: String?, qualifiedName qName: String?, attributes attributeDict: [String : String]) {
        eName = elementName
        if elementName == "book" {
            bookTitle = String()
            bookAuthor = String()
        }
    }
```

开始读区节点，一个<></>这种标示对就是一个节点
这个方法是开始获取一个节点的内容，
== 参数parser是携带需解码xml二进制数据的委托者

==参数elementName是当前解析xml的某个节点的键（键值对中的键）

==参数namespaceURI和qName返回的是当前xml所在的域名＋路径

==参数attributeDict返回的是当前节点的属性，写在第一个<>里的内容


**fuc2** 

    func parser(_ parser: XMLParser, didEndElement elementName: String, namespaceURI: String?, qualifiedName qName: String?) {
        if elementName == "book" {
            
            let book = Book()
            book.bookTitle = bookTitle
            book.bookAuthor = bookAuthor
            
            books.append(book)
        }
    }

这个方法是终点方法，此时，代理类中定义的资源成员已经被解析完毕，直接操作即可

**fuc3** 

    func parser(_ parser: XMLParser, foundCharacters string: String) {
        let data = string.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines)
        取出<> </> 中的值
         if (!data.isEmpty) {
            if eName == "title" {
                bookTitle += data
            } else if eName == "author" {
                bookAuthor += data
            }
        }
    }


这个方法是被循环调用的，作用是返回每一个节点的内容（键值对中的值）

## important
fuc1开始后，后fuc3，按顺序，取出一个节点的所有值，给fuc2. 

然后再从fuc1开始循坏下去
