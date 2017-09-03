页面有些元素是 AJAX 动态添加的，要给这些元素绑定事件，可以使用 jQuery 中的 on(events,[selector],[data],fn)。

- **events**:一个或多个用空格分隔的事件类型和可选的命名空间，如"click"或"keydown.myPlugin" 。
- **selector**:一个选择器字符串用于过滤器的触发事件的选择器元素的后代。如果选择的< null或省略，当它到达选定的元素，事件总是触发。
- **data**:当一个事件被触发时要传递event.data给事件处理函数。
- **fn**:该事件被触发时执行的函数。 false 值也可以做一个函数的简写，返回false。

简单示例：
AJAX 请求数据后，在表格中添加相应数据，并给它们绑定 click 事件。
#### html:
```
<table>
	<thead>
		<th>id</th>
		<th>value</th>
	</thead>
	<tbody id="tbody">
		
	</tbody>
</table>
```
#### js:
```
/*response = {
	code: 1,
	data: [
		{ id: 1, value: 1},
		{ id: 2, value: 2},
		{ id: 3, value: 3}
	]
} // 后台传回的数据 */

// 添加数据到 table 中
$.post('请求 url', function (response) { // response: 后台返回的数据
	$(response.data).each(function () {
		$('#tbody').append('<tr>'+ this.id +'<td></td><td>'+ this.value +'</td></tr>');
	});
})

// 给按每条记录定 click 事件：点击 tr 时，会在控制台打印出 tr 内容。
$('#tbody').on('click', 'tr', function () {
	console.log(this);
});
```