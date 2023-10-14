> *小游戏过审被拒? 你想对代码做混淆但是发现包体变化巨大, 而且运行起来明显卡顿, 然后你想手动调整代码但是又无从下手, 因为你根本不知道你的修改是否有用, 最后能否过审还是只凭运气, 那么这个工具或许可以帮你解决问题.*
> 
> #### 关于JS和过审
> * 可以抓取侵权包或者高度相似的包反编, 使用本工具对比他们的结构, 你将很容易把他们变得不同.
> * 在JS中加密图片的正向意义并不大, 与其赛进去一堆垃圾不如加个 [**隐形水印**](https://store.cocos.com/app/detail/5318) , 既能起到保护作用又能改变文件的MD5值.
> * 目前的JS环境根本不存在加密保护/不可逆混淆等手段, 都是在偷换概念, 因为JS代码最终是被直接运行的.
> * 混淆确实可以提高代码的理解难度, 但却使代码臃肿运行卡顿, 随着混淆力度的加深, 卡顿和代码体积将变得更糟糕.

## 它是什么
* 它是一个JS结构自动修改工具, 可使代码结构焕然一新.
* 它支持的格式: .js | .jsx , 支持的平台: macos | windows.
* 它不是单纯的变量名(字符串)替换工具, 语法树结构对比并不关心变量名, 类名, 函数名等.
* 它不是混淆工具, 可在代码结构处理后进行混淆, 参考: [javascript-obfuscator](https://obfuscator.io).
* 它采用AST语法树对JS代码进行修改, 可以帮你**改变80%以上的结构**, 而且对运行速度的影响**极其微小**.
* 它提供语法结构对比, 让你看到结构相似的代码位置, 即使手动修改也能做到**有的放矢**, 可帮助你进一步提升**审核通过率**.

## 如何使用
* 支持的命令: rts | mov | sim | dec | upg , 处理编辑器导出的重要文件, 如: `assets/main/index.xxxxx.js`.
* 每次处理结果会有差别, 可多次运行得到不同的马甲代码, 并使用sim命令对比从而做出选择.
* 如果两个处理后的文件相似度仍旧比较高则可以使用mov命令对其中一个文件再次处理.
* 可使用dec命令还原部分被混淆的代码, 耗时较长且存在破坏代码可能, 但在与侵权代码对比中将非常有用.
* 可使用rts命令批量修改TS脚本(文件名/类名/成员变量/成员方法), 原脚本中**类名与文件名**必须相同.
* 可使用upg命令解包**小游戏**, 从而对比侵权代码结构, 网上有很多关于如何得到**wxapkg**包的信息.
* mov命令支持按模块修改代码结构, 这样效果更好, 但文件体积会增加, 模块依赖于建时的**模块擦除**选项.
```
    // 修改input.js代码结构
    > .\mov-win-x64.exe mov input.js

    // 对比两个js文件的代码结构
    > .\mov-win-x64.exe sim input_a.js input_b.js

    // 还原被混淆的代码
    > .\mov-win-x64.exe dec input_ob.js

    // 修改script文件夹内的TS脚本
    > .\mov-win-x64.exe rts assets/script

    // 解包wxapkg
    > .\mov-win-x64.exe upg wxd1234567890abcdef/25
```

### [[MakeOver]小游戏过审助手](https://store.cocos.com/app/detail/5337)

*注意解包与解密不同, 如果解包失败, 应该先对包进行解密.*
1. PC端: [decrypt.exe](./decrypt.exe)
```
// -wxid 	微信Appid
// -in		输入文件路径
// -out     输出文件路径

.\decrypt.exe -wxid [wxAppid] -in [filePath] -out [savePath]
```
wxapkg包位置:
```
C:\Users\xxx\Documents\WeChat Files\Applet\wxbxxxxxxxxxxxxxxd0\xx
```

2. Mac端: (未加密)
wxapkg包位置:
```
/Users/xxx/Library/Containers/com.tencent.xinWeChat/Data/.wxapplet/packages/wx18ded455ed95f695/15
```

3. Android端: (包含模拟器) 自行谷哥吧, 很多.
