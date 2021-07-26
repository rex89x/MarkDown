# 0628 Course 5 Note

View the .Net MVC Fronted End Notes with HackMD.

Ajax
---

- Asynchronous JavaScript and XML
- SPA(Single Page Application)
- HTTP Method
- Object and Array
var obj = {aaa: "1234"}
var list = {"123", "456"}
- Method:POST/GET
$.ajax({
    method: "POST",
    url: "",
    beforeSend: function (xhr){
        //送出前的行為
    }
}).done(function (data){
    //送出完成的結果
}).fail(function (XHR){
    //送出失敗
});

- 傳統的Web Site採取(Multi-page) 做法
- 現在的Web Site轉移到 SPA 的觀念
*源自AJAX技術
*只需要一個望頁即可回應使用者所需的各種體驗
*Backbone.js Angular.js ... etc

- Sample Ajax Code (Controller端)
[HttpPost]
public JsonResult GetTestData(string testString){
    return Json(testString + "call Ajax success!!");
}

- Sample Ajax Code (cshtml端)
<h2 id="demo_input" type="text" name="name" value="" />
<input id="demo_input" type="text" name="name" value="" />
<button id="btn_call_ajax">CALL AJAX</button>

- Sample Ajax Code (JavaScript端)
$("#btn_call_ajax").click(function() {
    $.ajax({
        url: "GetTestData",
        dataType: "json",
        data: { "testString": $("#demo_input").val() },
        type: "post"
    }).done(function(data){
        $("#demo_result").text(data);
    })
});

- Sample DropDownList Ajax Code (controller端)
public JsonResult GetDropDownListData(){
    List<string> tempData = new List<string>();
    tempData.Add("項目一");
    tempData.Add("項目二");
    return Json(tempData);
}

- Sample DropDownList Ajax Code (cshtml端)
<select id="demo_select"></select>
<button id="btn_demo_select"></button>

- Sample DropDownList Ajax Code (JavaScript端) 
$("#btn_demo_select").click(function (){
    $("#demo_select").kendoDropDownList({
        dataSource: {
            transport: {
                read: {
                    url: "GetDropDownListData",
                    type: "Post",
                    dataType: "json"
                }
            }
        }
    })
})

- Data Binding (Model端)
namespace BookMaintenance.Models{
    public DemoModel(string id, string name){
        this.Id = id;
        this.Name = name;
    }
    public class DemoModel{
        public string Id { get; set; }
        public string Name { get; set; }
    }
}

- Data Binding (Controller端)
public JsonResult GetGridData(){
    List<DemoModel> tempData = new List<DemoModel>();
    tempData.Add(new DemoModel("1", "資料庫設計"));
    tempData.Add(new DemoModel("2", "資料庫設計2"));
    tempData.Add(new DemoModel("3", "資料庫設計3"));
    return Json(tempData);
}

- Data Binding (cshtml端)
<div id="demo_grid"></div>
<button id="btn_get_grid_data">GET GRID DATA</button>

<script>
    $("#btn_get_grid_data").click(function (){
        $("#demo_grid").kendoGrid({
            dataSource:{
                transport: {
                    read: {
                        url: "GetGridData",
                        type: "post",
                        dataType: "json"
                    }
                }
            },
            height: 500,
            columns: [
                {field:"Id", title: "編號", width: "50%" },
                {field:"Name", title: "名稱", width: "50%"}
            ]
        })
    });
</script>

- auto_complete_input (cshtml端)
<input id="demo_auto_complete_input", type="text", name="name" value="" />
<button id="btn_demo_auto_complete">Get AutoComplete Data</button>

- auto_complete_input (Controller端)
[HttpPost]
public JsonResult GetAutoCompleteData(){
    List<string> tempData = new List <string> ();
    tempData.Add("資料庫設計");
    tempData.Add("項目一");
    tempData.Add("SQL三天速成");
    tempData.Add("JavaScript");
    return Json(tempData);
}

- auto_complete_input (JavaScript端)
$("#btn_demo_auto_complete").click(function () {
    $("#demo_auto_complete_input").kendoAutoComplete({
        dataSource: {
            transport: {
                read: {
                    url: "GetAutoCompleteData",
                    dataType: "json",
                    type: "post"
                }
            }
        }
    });
});

 





Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `Dot Net`
