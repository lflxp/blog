---
layout: post
title: Markdown字体颜色 
category: markdown
comments: true
tags:
- markdown
---

# markdown编辑器语法——字体、字号与颜色 

  **Markdown**是一种可以使用普通文本编辑器编写的标记语言，通过类似HTML的标记语法，它可以使普通文本内容具有一定的格式。但是它本身是不支持修改字体、字号与颜色等功能的！

  **CSDN-markdown**编辑器是其衍生版本，扩展了Markdown的功能（如表格、脚注、内嵌HTML等等）！对，就是**内嵌HTML**，接下来要讲的功能就需要使用**内嵌HTML**的方法来实现。

# 字体、字号与颜色

```
1. <font face="黑体">我是黑体字</font>
2. <font face="微软雅黑">我是微软雅黑</font>
3. <font face="STCAIYUN">我是华文彩云</font>
4. <font color=#0099ff size=7 face="黑体">color=#0099ff size=72 face="黑体"</font>
5. <font color=#00ffff size=72>color=#00ffff</font>
6. <font color=gray size=72>color=gray</font>
```
> Size：规定文本的尺寸大小。可能的值：从 1 到 7 的数字。浏览器默认值是 3。
呈现效果

- <font face="黑体">我是黑体字</font>
- <font face="微软雅黑">我是微软雅黑</font>
- <font face="STCAIYUN">我是华文彩云</font>
- <font color=#0099ff size=7 face="黑体">color=#0099ff size=72 face="黑体"</font>
- <font color=#00ffff size=72>color=#00ffff</font>
- <font color=gray size=72>color=gray</font>

```
color=#0099ff size=72 face=”黑体”
color=#00ffff 可以用十六位颜色值
color=gray 也可以用已知颜色名
```
# 颜色名列表
<table>
	<tr>
    <th>颜色名</th>
    <th>十六进制颜色值</th>
    <th>颜色</th>
  </tr>
  <tr><td>AliceBlue	</td><td><font color=#F0F8FF>我变</font></td><td>rgb(240, 248, 255)</td></tr>
<tr><td>AntiqueWhite	</td><td><font color=#FAEBD7>我变</font></td><td>rgb(250, 235, 215)</td></tr>
<tr><td>Aqua	</td><td><font color=#00FFFF>我变</font></td><td>rgb(0, 255, 255)</td></tr>
<tr><td>Aquamarine	</td><td><font color=#7FFFD4>我变</font></td><td>rgb(127, 255, 212)</td></tr>
<tr><td>Azure	</td><td><font color=#F0FFFF>我变</font></td><td>rgb(240, 255, 255)</td></tr>
<tr><td>Beige	</td><td><font color=#F5F5DC>我变</font></td><td>rgb(245, 245, 220)</td></tr>
<tr><td>Bisque	</td><td><font color=#FFE4C4>我变</font></td><td>rgb(255, 228, 196)</td></tr>
<tr><td>Black	</td><td><font color=#000000>我变</font></td><td>rgb(0, 0, 0)</td></tr>
<tr><td>BlanchedAlmond	</td><td><font color=#FFEBCD>我变</font></td><td>rgb(255, 235, 205)</td></tr>
<tr><td>Blue	</td><td><font color=#0000FF>我变</font></td><td>rgb(0, 0, 255)</td></tr>
<tr><td>BlueViolet	</td><td><font color=#8A2BE2>我变</font></td><td>rgb(138, 43, 226)</td></tr>
<tr><td>Brown	</td><td><font color=#A52A2A>我变</font></td><td>rgb(165, 42, 42)</td></tr>
<tr><td>BurlyWood	</td><td><font color=#DEB887>我变</font></td><td>rgb(222, 184, 135)</td></tr>
<tr><td>CadetBlue	</td><td><font color=#5F9EA0>我变</font></td><td>rgb(95, 158, 160)</td></tr>
<tr><td>Chartreuse	</td><td><font color=#7FFF00>我变</font></td><td>rgb(127, 255, 0)</td></tr>
<tr><td>Chocolate	</td><td><font color=#D2691E>我变</font></td><td>rgb(210, 105, 30)</td></tr>
<tr><td>Coral	</td><td><font color=#FF7F50>我变</font></td><td>rgb(255, 127, 80)</td></tr>
<tr><td>CornflowerBlue	</td><td><font color=#6495ED>我变</font></td><td>rgb(100, 149, 237)</td></tr>
<tr><td>Cornsilk	</td><td><font color=#FFF8DC>我变</font></td><td>rgb(255, 248, 220)</td></tr>
<tr><td>Crimson	</td><td><font color=#DC143C>我变</font></td><td>rgb(220, 20, 60)</td></tr>
<tr><td>Cyan	</td><td><font color=#00FFFF>我变</font></td><td>rgb(0, 255, 255)</td></tr>
<tr><td>DarkBlue	</td><td><font color=#00008B>我变</font></td><td>rgb(0, 0, 139)</td></tr>
<tr><td>DarkCyan	</td><td><font color=#008B8B>我变</font></td><td>rgb(0, 139, 139)</td></tr>
<tr><td>DarkGoldenRod	</td><td><font color=#B8860B>我变</font></td><td>rgb(184, 134, 11)</td></tr>
<tr><td>DarkGray	</td><td><font color=#A9A9A9>我变</font></td><td>rgb(169, 169, 169)</td></tr>
<tr><td>DarkGreen	</td><td><font color=#006400>我变</font></td><td>rgb(0, 100, 0)</td></tr>
<tr><td>DarkKhaki	</td><td><font color=#BDB76B>我变</font></td><td>rgb(189, 183, 107)</td></tr>
<tr><td>DarkMagenta	</td><td><font color=#8B008B>我变</font></td><td>rgb(139, 0, 139)</td></tr>
<tr><td>DarkOliveGreen	</td><td><font color=#556B2F>我变</font></td><td>rgb(85, 107, 47)</td></tr>
<tr><td>Darkorange	</td><td><font color=#FF8C00>我变</font></td><td>rgb(255, 140, 0)</td></tr>
<tr><td>DarkOrchid	</td><td><font color=#9932CC>我变</font></td><td>rgb(153, 50, 204)</td></tr>
<tr><td>DarkRed	</td><td><font color=#8B0000>我变</font></td><td>rgb(139, 0, 0)</td></tr>
<tr><td>DarkSalmon	</td><td><font color=#E9967A>我变</font></td><td>rgb(233, 150, 122)</td></tr>
<tr><td>DarkSeaGreen	</td><td><font color=#8FBC8F>我变</font></td><td>rgb(143, 188, 143)</td></tr>
<tr><td>DarkSlateBlue	</td><td><font color=#483D8B>我变</font></td><td>rgb(72, 61, 139)</td></tr>
<tr><td>DarkSlateGray	</td><td><font color=#2F4F4F>我变</font></td><td>rgb(47, 79, 79)</td></tr>
<tr><td>DarkTurquoise	</td><td><font color=#00CED1>我变</font></td><td>rgb(0, 206, 209)</td></tr>
<tr><td>DarkViolet	</td><td><font color=#9400D3>我变</font></td><td>rgb(148, 0, 211)</td></tr>
<tr><td>DeepPink	</td><td><font color=#FF1493>我变</font></td><td>rgb(255, 20, 147)</td></tr>
<tr><td>DeepSkyBlue	</td><td><font color=#00BFFF>我变</font></td><td>rgb(0, 191, 255)</td></tr>
<tr><td>DimGray	</td><td><font color=#696969>我变</font></td><td>rgb(105, 105, 105)</td></tr>
<tr><td>DodgerBlue	</td><td><font color=#1E90FF>我变</font></td><td>rgb(30, 144, 255)</td></tr>
<tr><td>Feldspar	</td><td><font color=#D19275>我变</font></td><td>rgb(209, 146, 117)</td></tr>
<tr><td>FireBrick	</td><td><font color=#B22222>我变</font></td><td>rgb(178, 34, 34)</td></tr>
<tr><td>FloralWhite	</td><td><font color=#FFFAF0>我变</font></td><td>rgb(255, 250, 240)</td></tr>
<tr><td>ForestGreen	</td><td><font color=#228B22>我变</font></td><td>rgb(34, 139, 34)</td></tr>
<tr><td>Fuchsia	</td><td><font color=#FF00FF>我变</font></td><td>rgb(255, 0, 255)</td></tr>
<tr><td>Gainsboro	</td><td><font color=#DCDCDC>我变</font></td><td>rgb(220, 220, 220)</td></tr>
<tr><td>GhostWhite	</td><td><font color=#F8F8FF>我变</font></td><td>rgb(248, 248, 255)</td></tr>
<tr><td>Gold	</td><td><font color=#FFD700>我变</font></td><td>rgb(255, 215, 0)</td></tr>
<tr><td>GoldenRod	</td><td><font color=#DAA520>我变</font></td><td>rgb(218, 165, 32)</td></tr>
<tr><td>Gray	</td><td><font color=#808080>我变</font></td><td>rgb(128, 128, 128)</td></tr>
<tr><td>Green	</td><td><font color=#008000>我变</font></td><td>rgb(0, 128, 0)</td></tr>
<tr><td>GreenYellow	</td><td><font color=#ADFF2F>我变</font></td><td>rgb(173, 255, 47)</td></tr>
<tr><td>HoneyDew	</td><td><font color=#F0FFF0>我变</font></td><td>rgb(240, 255, 240)</td></tr>
<tr><td>HotPink	</td><td><font color=#FF69B4>我变</font></td><td>rgb(255, 105, 180)</td></tr>
<tr><td>IndianRed	</td><td><font color=#CD5C5C>我变</font></td><td>rgb(205, 92, 92)</td></tr>
<tr><td>Indigo	</td><td><font color=#4B0082>我变</font></td><td>rgb(75, 0, 130)</td></tr>
<tr><td>Ivory	</td><td><font color=#FFFFF0>我变</font></td><td>rgb(255, 255, 240)</td></tr>
<tr><td>Khaki	</td><td><font color=#F0E68C>我变</font></td><td>rgb(240, 230, 140)</td></tr>
<tr><td>Lavender	</td><td><font color=#E6E6FA>我变</font></td><td>rgb(230, 230, 250)</td></tr>
<tr><td>LavenderBlush	</td><td><font color=#FFF0F5>我变</font></td><td>rgb(255, 240, 245)</td></tr>
<tr><td>LawnGreen	</td><td><font color=#7CFC00>我变</font></td><td>rgb(124, 252, 0)</td></tr>
<tr><td>LemonChiffon	</td><td><font color=#FFFACD>我变</font></td><td>rgb(255, 250, 205)</td></tr>
<tr><td>LightBlue	</td><td><font color=#ADD8E6>我变</font></td><td>rgb(173, 216, 230)</td></tr>
<tr><td>LightCoral	</td><td><font color=#F08080>我变</font></td><td>rgb(240, 128, 128)</td></tr>
<tr><td>LightCyan	</td><td><font color=#E0FFFF>我变</font></td><td>rgb(224, 255, 255)</td></tr>
<tr><td>LightGoldenRodYellow	</td><td><font color=#FAFAD2>我变</font></td><td>rgb(250, 250, 210)</td></tr>
<tr><td>LightGrey	</td><td><font color=#D3D3D3>我变</font></td><td>rgb(211, 211, 211)</td></tr>
<tr><td>LightGreen	</td><td><font color=#90EE90>我变</font></td><td>rgb(144, 238, 144)</td></tr>
<tr><td>LightPink	</td><td><font color=#FFB6C1>我变</font></td><td>rgb(255, 182, 193)</td></tr>
<tr><td>LightSalmon	</td><td><font color=#FFA07A>我变</font></td><td>rgb(255, 160, 122)</td></tr>
<tr><td>LightSeaGreen	</td><td><font color=#20B2AA>我变</font></td><td>rgb(32, 178, 170)</td></tr>
<tr><td>LightSkyBlue	</td><td><font color=#87CEFA>我变</font></td><td>rgb(135, 206, 250)</td></tr>
<tr><td>LightSlateBlue	</td><td><font color=#8470FF>我变</font></td><td>rgb(132, 112, 255)</td></tr>
<tr><td>LightSlateGray	</td><td><font color=#778899>我变</font></td><td>rgb(119, 136, 153)</td></tr>
<tr><td>LightSteelBlue	</td><td><font color=#B0C4DE>我变</font></td><td>rgb(176, 196, 222)</td></tr>
<tr><td>LightYellow	</td><td><font color=#FFFFE0>我变</font></td><td>rgb(255, 255, 224)</td></tr>
<tr><td>Lime	</td><td><font color=#00FF00>我变</font></td><td>rgb(0, 255, 0)</td></tr>
<tr><td>LimeGreen	</td><td><font color=#32CD32>我变</font></td><td>rgb(50, 205, 50)</td></tr>
<tr><td>Linen	</td><td><font color=#FAF0E6>我变</font></td><td>rgb(250, 240, 230)</td></tr>
<tr><td>Magenta	</td><td><font color=#FF00FF>我变</font></td><td>rgb(255, 0, 255)</td></tr>
<tr><td>Maroon	</td><td><font color=#800000>我变</font></td><td>rgb(128, 0, 0)</td></tr>
<tr><td>MediumAquaMarine	</td><td><font color=#66CDAA>我变</font></td><td>rgb(102, 205, 170)</td></tr>
<tr><td>MediumBlue	</td><td><font color=#0000CD>我变</font></td><td>rgb(0, 0, 205)</td></tr>
<tr><td>MediumOrchid	</td><td><font color=#BA55D3>我变</font></td><td>rgb(186, 85, 211)</td></tr>
<tr><td>MediumPurple	</td><td><font color=#9370D8>我变</font></td><td>rgb(147, 112, 216)</td></tr>
<tr><td>MediumSeaGreen	</td><td><font color=#3CB371>我变</font></td><td>rgb(60, 179, 113)</td></tr>
<tr><td>MediumSlateBlue	</td><td><font color=#7B68EE>我变</font></td><td>rgb(123, 104, 238)</td></tr>
<tr><td>MediumSpringGreen	</td><td><font color=#00FA9A>我变</font></td><td>rgb(0, 250, 154)</td></tr>
<tr><td>MediumTurquoise	</td><td><font color=#48D1CC>我变</font></td><td>rgb(72, 209, 204)</td></tr>
<tr><td>MediumVioletRed	</td><td><font color=#C71585>我变</font></td><td>rgb(199, 21, 133)</td></tr>
<tr><td>MidnightBlue	</td><td><font color=#191970>我变</font></td><td>rgb(25, 25, 112)</td></tr>
<tr><td>MintCream	</td><td><font color=#F5FFFA>我变</font></td><td>rgb(245, 255, 250)</td></tr>
<tr><td>MistyRose	</td><td><font color=#FFE4E1>我变</font></td><td>rgb(255, 228, 225)</td></tr>
<tr><td>Moccasin	</td><td><font color=#FFE4B5>我变</font></td><td>rgb(255, 228, 181)</td></tr>
<tr><td>NavajoWhite	</td><td><font color=#FFDEAD>我变</font></td><td>rgb(255, 222, 173)</td></tr>
<tr><td>Navy	</td><td><font color=#000080>我变</font></td><td>rgb(0, 0, 128)</td></tr>
<tr><td>OldLace	</td><td><font color=#FDF5E6>我变</font></td><td>rgb(253, 245, 230)</td></tr>
<tr><td>Olive	</td><td><font color=#808000>我变</font></td><td>rgb(128, 128, 0)</td></tr>
<tr><td>OliveDrab	</td><td><font color=#6B8E23>我变</font></td><td>rgb(107, 142, 35)</td></tr>
<tr><td>Orange	</td><td><font color=#FFA500>我变</font></td><td>rgb(255, 165, 0)</td></tr>
<tr><td>OrangeRed	</td><td><font color=#FF4500>我变</font></td><td>rgb(255, 69, 0)</td></tr>
<tr><td>Orchid	</td><td><font color=#DA70D6>我变</font></td><td>rgb(218, 112, 214)</td></tr>
<tr><td>PaleGoldenRod	</td><td><font color=#EEE8AA>我变</font></td><td>rgb(238, 232, 170)</td></tr>
<tr><td>PaleGreen	</td><td><font color=#98FB98>我变</font></td><td>rgb(152, 251, 152)</td></tr>
<tr><td>PaleTurquoise	</td><td><font color=#AFEEEE>我变</font></td><td>rgb(175, 238, 238)</td></tr>
<tr><td>PaleVioletRed	</td><td><font color=#D87093>我变</font></td><td>rgb(216, 112, 147)</td></tr>
<tr><td>PapayaWhip	</td><td><font color=#FFEFD5>我变</font></td><td>rgb(255, 239, 213)</td></tr>
<tr><td>PeachPuff	</td><td><font color=#FFDAB9>我变</font></td><td>rgb(255, 218, 185)</td></tr>
<tr><td>Peru	</td><td><font color=#CD853F>我变</font></td><td>rgb(205, 133, 63)</td></tr>
<tr><td>Pink	</td><td><font color=#FFC0CB>我变</font></td><td>rgb(255, 192, 203)</td></tr>
<tr><td>Plum	</td><td><font color=#DDA0DD>我变</font></td><td>rgb(221, 160, 221)</td></tr>
<tr><td>PowderBlue	</td><td><font color=#B0E0E6>我变</font></td><td>rgb(176, 224, 230)</td></tr>
<tr><td>Purple	</td><td><font color=#800080>我变</font></td><td>rgb(128, 0, 128)</td></tr>
<tr><td>Red	</td><td><font color=#FF0000>我变</font></td><td>rgb(255, 0, 0)</td></tr>
<tr><td>RosyBrown	</td><td><font color=#BC8F8F>我变</font></td><td>rgb(188, 143, 143)</td></tr>
<tr><td>RoyalBlue	</td><td><font color=#4169E1>我变</font></td><td>rgb(65, 105, 225)</td></tr>
<tr><td>SaddleBrown	</td><td><font color=#8B4513>我变</font></td><td>rgb(139, 69, 19)</td></tr>
<tr><td>Salmon	</td><td><font color=#FA8072>我变</font></td><td>rgb(250, 128, 114)</td></tr>
<tr><td>SandyBrown	</td><td><font color=#F4A460>我变</font></td><td>rgb(244, 164, 96)</td></tr>
<tr><td>SeaGreen	</td><td><font color=#2E8B57>我变</font></td><td>rgb(46, 139, 87)</td></tr>
<tr><td>SeaShell	</td><td><font color=#FFF5EE>我变</font></td><td>rgb(255, 245, 238)</td></tr>
<tr><td>Sienna	</td><td><font color=#A0522D>我变</font></td><td>rgb(160, 82, 45)</td></tr>
<tr><td>Silver	</td><td><font color=#C0C0C0>我变</font></td><td>rgb(192, 192, 192)</td></tr>
<tr><td>SkyBlue	</td><td><font color=#87CEEB>我变</font></td><td>rgb(135, 206, 235)</td></tr>
<tr><td>SlateBlue	</td><td><font color=#6A5ACD>我变</font></td><td>rgb(106, 90, 205)</td></tr>
<tr><td>SlateGray	</td><td><font color=#708090>我变</font></td><td>rgb(112, 128, 144)</td></tr>
<tr><td>Snow	</td><td><font color=#FFFAFA>我变</font></td><td>rgb(255, 250, 250)</td></tr>
<tr><td>SpringGreen	</td><td><font color=#00FF7F>我变</font></td><td>rgb(0, 255, 127)</td></tr>
<tr><td>SteelBlue	</td><td><font color=#4682B4>我变</font></td><td>rgb(70, 130, 180)</td></tr>
<tr><td>Tan	</td><td><font color=#D2B48C>我变</font></td><td>rgb(210, 180, 140)</td></tr>
<tr><td>Teal	</td><td><font color=#008080>我变</font></td><td>rgb(0, 128, 128)</td></tr>
<tr><td>Thistle	</td><td><font color=#D8BFD8>我变</font></td><td>rgb(216, 191, 216)</td></tr>
<tr><td>Tomato	</td><td><font color=#FF6347>我变</font></td><td>rgb(255, 99, 71)</td></tr>
<tr><td>Turquoise	</td><td><font color=#40E0D0>我变</font></td><td>rgb(64, 224, 208)</td></tr>
<tr><td>Violet	</td><td><font color=#EE82EE>我变</font></td><td>rgb(238, 130, 238)</td></tr>
<tr><td>VioletRed	</td><td><font color=#D02090>我变</font></td><td>rgb(208, 32, 144)</td></tr>
<tr><td>Wheat	</td><td><font color=#F5DEB3>我变</font></td><td>rgb(245, 222, 179)</td></tr>
<tr><td>White	</td><td><font color=#FFFFFF>我变</font></td><td>rgb(255, 255, 255)</td></tr>
<tr><td>WhiteSmoke	</td><td><font color=#F5F5F5>我变</font></td><td>rgb(245, 245, 245)</td></tr>
<tr><td>Yellow	</td><td><font color=#FFFF00>我变</font></td><td>rgb(255, 255, 0)</td></tr>
<tr><td>YellowGreen	</td><td><font color=#9ACD32>我变</font></td><td>rgb(154, 205, 50)</td></tr>
</table>
