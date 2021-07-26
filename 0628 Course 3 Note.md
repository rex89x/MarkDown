# 0628 Course 3 Note

View the Notes with HackMD.
https://ithelp.ithome.com.tw/articles/10203758

Kendo UI DropDownList
---

- dataTextField(傳遞data內部欄位)
- dataValueField(傳遞data內部欄位)
- dataSource()
let data = {
    {text:(name1), value:(value1)},
    {text:(name2), value:(value2)},
    {text:(name3), value:(value3)},
    .....
}
- index(指向第幾選項)
- change
var Index = document.querySelector("")

Kendo UI DatePicker
---

- componentType: "modern"(傳遞data內部欄位)
- format: "yyyy/MM/dd"(日期格式) EX: yyyy/MM/dd, dd/MM/yyyy
- value: new Date()(預設日期)

- index(指向第幾選項)
- change
var Index = document.querySelector("")

JS CHANGE HTML ATTRIBUTE
---

- var (name) = document.querySelector("id");
- (name).setAttribute(("attribute"), (WantToChange))

GET DropDownList VALUE
---

- var (name) = $("id").val();

JS Switch Case 
---

- switch (var) { case (condition): statement; break ..... }
switch (var) { case (condition): 
                    statement; 
                    break;
               case (condition):
                    statement;
                    break;
                    ..............
             }


KendoWindow
---

- SetKendoWindow()
{$("#dialog").kendoWindow({
        visible: false,
        height: "530px",
        modal: true,
        pinned: false,
        position: {
            top: 100,
            left: "33%",
            close: CloseKendoWindow,
        },
        resizable: false,
        title: "新增書籍",
        width: "500px"
    });

let dialog = $("#dialog").data("kendoWindow");
dialog.open();}

KendoGrid
---

- dataSource: 
'''
dataSource: {
    data: bookDataFromLocalStorage,
    schema: {
        model: {
            fields: {
                Field1: type:"type1"
                Field2: type:"type2"
                Field3: type:"type3"
                ..............
            }
        }
    },
    pageSize: 20, (每頁幾筆資料)
},
'''
- toolbar: 
'''
kendo.template("<div class='book-grid-toolbar'><input class='book-grid-search' placeholder='我想要找......' type='text'></input></div>"),
'''

- height: 550, (視窗大小)
- sortable: true, (是否排序)
- pageable: (如何分頁)
pageable: {
    input: true,
    numeric: false
},
- columns: 
[
            { field: "BookId", title: "書籍編號",width:"10%"},
            { field: "BookName", title: "書籍名稱", width: "50%" },
            { field: "BookCategory", title: "書籍種類", width: "10%" },
            { field: "BookAuthor", title: "作者", width: "15%" },
            { field: "BookBoughtDate", title: "購買日期", width: "15%" },
            { command: { text: "刪除", click: deleteBook }, title: " ", width: "120px" }
]


Button Click
---

- id在JS code 裡面寫 $("#name")
- class在 JS code 裡面寫 $(".name")
- click Function
$("#Insert-Button").click(function(){
    CreateBook();
});

Kendo Grid Dynamic Search
---

$(".book-grid-search").on("input", function(){
        let GetSearchName = $(this).val();

        $("#book_grid").data("kendoGrid").dataSource.filter({
    logic: "or",
    filters: [
        {field: "BookId", operator: "eq", value: GetSearchName},
        {field: "BookName", operator: "contains", value: GetSearchName},
        {field: "BookCategory", operator: "eq", value: GetSearchName},
        {field: "BookAuthor", operator: "eq", value: GetSearchName},
        {field: "BookBoughtDate", operator: "eq", value: GetSearchName},
        ]
    });
});

DropDownList onChange
---

- //find index
let Index = document.querySelector(".book-image")
- //get value
let GetOnChangeValue = $("#book_category").val()
- //set url
GetOnChangeValue = "image/" + GetOnChangeValue + ".jpg";
- //set html src url
Index.setAttribute("src", GetOnChangeValue)

Delete KendoGrid Item
---
	
// 防止滾動
index.preventDefault();
let Target = $("#book_grid").data("kendoGrid");
let GetRowDelete = $(index.currentTarget).closest("tr");
Target.removeRow(GetRowDelete);

let GetRowDeleteStorage = $("#book_grid").data("kendoGrid").dataSource.data();
deleteLocalStorageBook(GetRowDeleteStorage);

function deleteLocalStorageBook(GetRowDeleteStorage){
    // loadbookdata
    localStorage.setItem("bookData", JSON.stringify(GetRowDeleteStorage));
}

KendoDatePicker
---

{$("#bought_datepicker").kendoDatePicker({
        componentType: "modern",
        format: "yyyy/MM/dd",
        value: new Date(),
    });}

Kendo Confirm
---

{kendo.confirm("你確定要刪除嗎?")
        .done(function () {
            index.preventDefault();
            let Target = $("#book_grid").data("kendoGrid");
            let GetRowDelete = $(index.currentTarget).closest("tr");
            Target.removeRow(GetRowDelete);

let GetRowDeleteStorage = $("#book_grid").data("kendoGrid").dataSource.data();
DeleteLocalStorageBook(GetRowDeleteStorage);
kendo.alert("刪除完成");
        })
        .fail(function () {
            kendo.alert("取消刪除");
        });}

Kendo Alert
---

- kendo.alert("Message");
	
JavaScript getElementById
---

- document.getElementById("book_publisher").value = "";

JavaScript ChangeDateTime Format
---

{    var RightNow = new Date();
    var RightNowString = RightNow.toISOString().slice(0, 10).replace(/-/g, "/");
    document.getElementById("bought_datepicker").value = RightNowString;}
    
Get LocalStorage Json
---

{function GetMaxBookId() {
    let MaxNumber = 0;
    for (let i = 0; i < bookDataFromLocalStorage.length; i++) {
        if (parseInt(bookDataFromLocalStorage[i].BookId, 10) > MaxNumber) {
            MaxNumber = parseInt(bookDataFromLocalStorage[i].BookId, 10);
        }
    }
    return MaxNumber;
}}
    
Create Book Into Grid
---

{function CreateNewBookIntoGrid(NewBook) {
    let gridDataSource = $("#book_grid").data("kendoGrid").dataSource;
    gridDataSource.add(NewBook);
    gridDataSource.sync();
}}
    
Create Record to LocalStorage
---

{function WriteDataIntoLocalStorage(bookDataFromLocalStorage) {
    localStorage.setItem("bookData", JSON.stringify(bookDataFromLocalStorage));
}}


Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `JS`
