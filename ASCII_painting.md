# ASCII画图 | ASCII_painting.md
#技术栈/兴趣爱好/奇巧淫技
## Textik
- [Textik - ASCII diagrams editor](https://textik.com/)
- 创建初始图，可以贴中文
	- 中文会造成这行后续字码无法对齐，粘出来后要自己修改
- 支持移动方框，且已有线跟随
- 支持选中，拉动变换大小
- 技巧：
	- 对以创建文字的修改，是选中后修改，点击A图标代表创建新文字
	- 拉出线后，箭头要和目标方框触碰出现红色，即线与方框绑定
	- 创建完copy出来后，再贴进去就没有上述功能了，因此图的修改使用另一个工具
- #技术栈/兴趣爱好/Lisp
## ASCIIFlow
- [ASCIIFlow](https://asciiflow.com/)
- 修改已有图
- 无法自由贴中文
- 支持任意选中移动
- 导出ASCII Basic类型，就能和Textik兼容
- 导出选定Comment type可以包装成注释
## 工作流 - 图
```
+--------+        
|Textik  |        
+--------+        
  |初始图            
  |               
  |               
+-v------+        
|Notes   |        
+----^---+        
  |  |            
  |  |            
  \  |可以多次修改      
   | |            
+--v------+       
|ASCIIFlow|       
+---------+       
                 
```
