# Kendo UI JavaScript Note

Use Kendo UI package
---
- JavaScript
*jquery-2.1.4.min.js
*kendo.all.min.js
*uikit.min.js

- CSS
*kendo.common-material.min.css
*kendo.material.min.css
*kendo.materialblack.min.css
*style.css
*uikit.min.css

* KendoUI Package In Folder KendoUI_Package

KendoUI Use Sample
--- 

- Button

$(".class").kendoButton();
$("#id").kendoButton();

- kendoWindow

$("#id").kendoWindow({
    visible: false,
    height: "xxxpx",
    modal: true,
    pinned: false,
    position: {
        top: xxx,
        left: "xx%",
        close: closefunction.
    },
    draggable: false,
    resizable: false,
    title: "name of grid",
    width: "xxxpx"
});

$("#button").click(function(){
    $("#id").data("kendoWindow").open();
});

- DropDownList

var dropDownListData = [
    { text: "1", value: "1" },
    { text: "2", value: "2" },
    { text: "3", value: "3" },
    { text: "4", value: "4" }
]

$("#id").kendoDropDownList({
    dataTextField: "text",
    dataValueField: "value",
    dataSource: dropDownListData,
    index: 0,
    change: changeFunction
});

- DatePicker

$("#id").kendoDatePicker({
    componentType: "modern",
    format: "yyyy/MM/dd",     // 日期格式
    value: new Date()         // 現在日期
});

- kendoGrid

$("#id").kendoGrid({
    sort: { field: "column", dir: "asc" },
    dataSource: {
        data: data,
        schema: {
            model: {
                fields: {
                    column1: { type: "string"},
                    column2: { type: "string"},
                    column3: { type: "string"},
                    column4: { type: "string"}
                }
            }
        },
        pageSize: every column per page,
    },
    height: xxx,
    sortable: true,
    pageable: {
        input: true,
        numeric: false
    },
    // columns 要用中括號
    columns: {
        { field: "col1", title: "col1", width: "25%" },
        { field: "col2", title: "col2", width: "25%" },
        { field: "col3", title: "col3", width: "25%" },
        { field: "col4", title: "col4", width: "25%" }
    }
});

- kendoValidator

$("#id").click(function(){
    $("#id").kendoValidator().data("kendoValidator").validate();
    // if correct return true, if incorrect return false
    
})




Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `JavaScript`