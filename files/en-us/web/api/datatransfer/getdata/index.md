---
title: "DataTransfer: getData() method"
short-title: getData()
slug: Web/API/DataTransfer/getData
page-type: web-api-instance-method
browser-compat: api.DataTransfer.getData
---

{{APIRef("HTML DOM")}}

The **`DataTransfer.getData()`**
method retrieves drag data (as a string) for the specified type.
If the drag operation does not include data, this method returns an empty
string.

Example data types are `text/plain` and `text/uri-list`.

## Syntax

```js-nolint
getData(format)
```

### Parameters

- `format`
  - : A string representing the type of data to retrieve.

### Return value

A string representing the drag data for the specified `format`. If the drag operation has no data or the operation has no data for the specified `format`, this method returns an empty string.

Note that `DataTransfer.getData()` may not return an expected value, because it only allows reading and writing data for specified events. During the `dragstart` and `drop` events, it is safe to access the data. For all other events, the data should be considered unavailable. Despite this, the items and their formats can still be enumerated.

## Examples

This example shows the use of the {{domxref("DataTransfer")}} object's
`getData()` and
{{domxref("DataTransfer.setData()","setData()")}} methods.

### HTML

```html
<div id="div1">
  <span id="drag" draggable="true">drag me to the other box</span>
</div>
<div id="div2"></div>
```

### CSS

```css
#div1,
#div2 {
  width: 100px;
  height: 50px;
  padding: 10px;
  border: 1px solid #aaaaaa;
}
```

### JavaScript

```js
const div1 = document.getElementById("div1");
const div2 = document.getElementById("div2");
const dragElement = document.getElementById("drag");

dragElement.addEventListener("dragstart", drag);
div1.addEventListener("dragover", allowDrop);
div2.addEventListener("dragover", allowDrop);
div1.addEventListener("drop", drop);
div2.addEventListener("drop", drop);

function allowDrop(allowDropEvent) {
  allowDropEvent.target.style.color = "blue";
  allowDropEvent.preventDefault();
}

function drag(dragEvent) {
  dragEvent.dataTransfer.setData("text", dragEvent.target.id);
  dragEvent.target.style.color = "green";
}

function drop(dropEvent) {
  dropEvent.preventDefault();
  const data = dropEvent.dataTransfer.getData("text");
  dropEvent.target.appendChild(document.getElementById(data));
  dragElement.style.color = "black";
}
```

### Result

{{EmbedLiveSample('Examples', 600) }}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Drag and drop](/en-US/docs/Web/API/HTML_Drag_and_Drop_API)
- [Drag Operations](/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations)
- [Recommended Drag Types](/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Recommended_drag_types)
