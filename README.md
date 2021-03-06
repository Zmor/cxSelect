#jQuery cxSelect

cxSelect 是基于 jQuery 的多级联动菜单插件，适用于省市、商品分类等联动菜单。

列表数据通过 AJAX 获取（需要在服务器环境运行），也可以使用变量自定义，数据内容使用 JSON 格式。

提供国内省市县数据（数据来源：<a href="https://github.com/basecss/cityData" target="_blank">basecss/cityData</a> Date: 2014.03.31）

**版本：**
* jQuery v1.7+
* jQuery cxSelect v1.3

文档：http://code.ciaoca.com/jquery/cxselect/

示例：http://code.ciaoca.com/jquery/cxselect/demo/

##【options 参数说明】
<table>
    <tr>
        <th width="120">名称</th>
        <th width="120">默认值</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>selects</td>
        <td>[]</td>
        <td>下拉选框组。输入 select 的 className</td>
    </tr>
    <tr>
        <td>url</td>
        <td>null</td>
        <td>列表数据文件路径（URL） | 变量（值为 JSON 的结构）</td>
    </tr>
    <tr>
        <td>nodata</td>
        <td>null</td>
        <td>子集无数据时 select 的状态。可设置为："none"(display:none) | "hidden"(visibility:hidden)</td>
    </tr>
    <tr>
        <td>required</td>
        <td>false</td>
        <td>是否为必选。设为 flase 时，会在列表头部添加 &lt;option value="0"&gt;请选择&lt;/option&gt。</td>
    </tr>
    <tr>
        <td>firstTitle</td>
        <td>"请选择"</td>
        <td>选框首选项的标题。如果要定义每个选框的首选项标题，可以通过属性 data-first-title 来设置。（仅在参数 required 为 false 时有效）</td>
    </tr>
    <tr>
        <td>firstValue</td>
        <td>"0"</td>
        <td>选框首选项的值。如果要定义每个选框的首选项值，可以通过属性 data-first-value 来设置。（仅在参数 required 为 false 时有效）</td>
    </tr>
</table>

##【data 属性参数】
<table>
    <tr>
        <th width="160">名称</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>data-value</td>
        <td>默认值</td>
    </tr>
	<tr>
		<td>data-first-title</td>
		<td>第一个 option 的标题（仅在参数 required 为 false 时有效）</td>
	</tr>
	<tr>
		<td>data-first-value</td>
		<td>第一个 option 的值（仅在参数 required 为 false 时有效）</td>
	</tr>
</table>

##【数据 JSON 结构】
<table>
    <thead>
        <tr>
            <th width="120">名称</th>
            <th width="180">类型</th>
            <th>说明</th>
        </tr>
    </thead>
    <tr>
        <td>v</td>
        <td>string | number</td>
        <td>设置 option 的值（可选项，未设置则使用 n）</td>
    </tr>
    <tr>
        <td>n</td>
        <td>string</td>
        <td>设置 option 的文本</td>
    </tr>
    <tr>
        <td>s</td>
        <td>array</td>
        <td>当前选项的子集</td>
    </tr>
</table>

##【使用方法】
###载入 JavaScript 文件
```html
<script src="jquery.js"></script> 
<script src="jquery.cxselect.js"></script>
```

###DOM 结构
```html
<!--
select 必须放在元素 id="element_id" 的内部，不限层级 
select 的 class 任意取值，也可以附加多个 class，如 class="province otherclass"，在调用时只需要输入其中一个即可，但是不能重复
如需设置 select 默认值，加上 data-value 属性，例：<select class="province" data-value="浙江省"></select>
-->
<div id="element_id">
    <select class="province"></select>
    <select class="city"></select>
    <select class="area"></select>
</div>
```

###调用 cxSelect
``` javascript
// selects 为数组形式，请注意顺序 
$("#element_id").cxSelect({
    selects : ["province", "city", "area"],
    nodata : "none"
});

// 设置全局默认值，需在引入 <script src="jquery.cxselect.js"></script> 之后，调用之前设置
$.cxSelect.defaults.url = "cityData.min.json"; // 提示：如果服务器不支持 .json 类型文件，请将文件改为 .js 文件
$.cxSelect.defaults.nodata = "none";
```


##【自定义数据结构】
``` javascript
/* 使用 JSON 格式
 * v : 设置 option 的值（可选项，未设置则使用 n）
 * n : 设置 option 的文本
 * s : 当前选项的子集
 */
[
    {"v" : "1", "n" : "A"},
    {"v" : "2", "n" : "B", "s" : [
        {"v" : "3", "n" : "Banana"},
        {"v" : "4", "n" : "Blue"},
        {"v" : "5", "n" : "Bus"}
    ]},
    {"v" : "6", "n" : "C"},
    {"v" : "7", "n" : "D", "s" : [
        {"v": "8", "n" : "day"},
        {"v": "9", "n" : "del"}
    ]}
]
```
