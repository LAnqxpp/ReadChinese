# ReadChinese
读取某个目录中的所有中文，并且将这些中文按照多语言(.string)格式写入文件中，可以直接拿来实现国际化


###操作示例图如下
![操作示例图](https://github.com/Ashen-Zhao/ReadChinese/blob/master/ReadChinese/screenshot.png)  


###使用说明
&emsp;本项目中，只是识别了.m和.h文件中的中文字符串，如果想要识别.swift等，请在`ViewController.m` 中的 `- (void)readFiles:(NSString *)str ` 方法中的`extension` 数组中，加入相应的后缀名即可。  
&emsp;该导出的文件，默认以`chinese.txt` 的形式存在于你选择的导出路径，想要修改导出文件名，请进入`- (IBAction)OpenFile:(NSButton *)sender` 方法中进行修改即可。

下面这个正则可以匹配到所有符合OC字符串格式的包含有中文的字符串。如果你用Swift，请去掉@。
@"[^"]*[\u4E00-\u9FA5]+[^"\n]*?"
然后，重点来了。Command+Shift+F，进入全局搜索引擎，切换为Replace模式，并把匹配模式改为Regular Expression。
在搜索条件里输入(@"[^"]*[\u4E00-\u9FA5]+[^"\n]*?")，在下面替换内容里输入NSLocalizedString($1, nil)。此处正则表达式两边加括号的目的是为了能够在替换时用$1获取原有字符串的值，在替换时把原有值放入宏定义内key的位置。然后，搜索，可以看到搜索结果，点击Replace All，即可完成替换。


1.按我说的，整个项目用正则找到所有的中文，然后加上系统的宏。
2.用我发的git项目，生成所有的需要国际化的key值。
3.在你项目的lLocalizable.strings文件中，添加上第2步中，得到的需要的key，然后你自己手动填写好对应的英文。如果你可以的话，可以用python或者任何一种脚本语言，找有道或者google翻译的接口。自动生成对应的英文。不过一般都不准，还是手动写把。


之后你面临几个问题：
1.推送国际化
2.网络请求错误提示国际化
3.系统权限提示国际化
4.系统原生国际化：如复制，粘贴
5 label 适配
