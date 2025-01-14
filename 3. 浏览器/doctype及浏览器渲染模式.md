
# Doctype
- DOCTYPE,或者称为 Document Type declaration（文档类型声明，DTD）
- 通常情况下，Document位于一个文档最前面,位于根元素Html的起始标签前
- 因为浏览器必须在解析HTML文档正文之前就确定文档的类型,以决定其需要的渲染模式
- 不同的渲染模式会影响到浏览器对于css代码甚至JavaScript脚本的解析
```
<!DOCTYPE html>
```
在这个doctype下，均会采用标准模式对html页面进行渲染

# 浏览器渲染模式
当页面没有！doctype声明 或者 doctype声明中没有HTML4以上的DTD声明，则页面以**怪异模式**渲染，其他为**标准模式**

## 检测渲染模式 document.compatMode 
最初由微软IE创造出来，这是一个只读的属性，返回一个字符串，只存在两种可能的返回值
- Backcompat：标准兼容模式未开启（怪异模式）
- CSS1compat：标准兼容模式已开启（标准模式）

## 区别
1. 
- 在IE9以上的浏览器中，渲染模式方面几乎没有差别
- 在Ie6 7 8 中,理论上存在怪异模式，实际上是标准模式
- 在IE6中，标准模式和怪异模式的差别最大

2. 盒模型
- 怪异模式
```
 盒模型的宽度=margin-left  + width  + margin-right
```
- 标准模式
```
盒模型的宽度=margin-left  +  border-left  +  padding-left  +  width +  padding-right  +  border-right  +  margin-right
```
3. 获取页面高度和宽度
- 怪异模式
```
cWidth=document.body.scrollWidth;
cHeight=document.body.scrollHeight;
```
- 标准模式
```
cWidth=document.documentElement.scrollWidth;
cHeight=document.documentElement.scrollHeight;
```
