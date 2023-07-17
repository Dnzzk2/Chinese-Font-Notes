**网页中文字体取目标子集并压缩**
>优点：大幅度压缩字体文件大小，提升渲染速度。
>缺点：牺牲部分字的渲染

静态网站，内容固定，建议使用font-spider

1.fonttools
>下载python fonttools工具包
```
pip install fonttools
```
2.生成一行一字的子集txt，源文本内容可以加入3500 common words.text中的汉字等
```
// 引入fs模块来读写文件
const fs = require('fs')

// 源文本内容
const sourceText = ''

// 生成文字数组
const chars = sourceText.split('')

// 写入文件函数
function writeToFile(chars) {
  const content = chars.join('\n')

  fs.writeFile('output.txt', content, (err) => {
    if (err) throw err
    console.log('文件写入成功!')
  })
}

writeToFile(chars)
```
3.生成含目标子集的tff文件
```
pyftsubset 阿里妈妈刀隶体.ttf --text-file=output.txt --output-file=output.ttf
```
4.ttf2woff2将ttf格式转为woff2格式,继续压缩文件大小
https://cloudconvert.com/ttf-to-woff2  
5.将生成的woff2文件运用于字体
