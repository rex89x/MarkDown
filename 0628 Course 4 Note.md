# 0628 Course 4 Note

View the .Net MVC Notes with HackMD.
https://www.itread01.com/content/1545319159.html

Visual Studio Tip
---

- 選取註解 Ctrl K+C 
- 取消註解 Ctrl K+U
- Coding列數 左邊按下去可以新增中斷點
- 變數按右鍵 加入監看式 可以在底下的console查看變數傳遞或存取值
- 滑鼠HOVER變數 可以查看變數內容

MVC BASIC
---

- Model: 商業邏輯、提供資料
- View: 使用者看到的資料
- Controller: Model And Views' Communicator

型別
---

- 弱型別: String
- 強型別: 有實際的屬性、Instance (改Compiler就會錯誤)

Create Model In Visual Studio
---

- Model資料夾按右鍵加入類別 (名字自己取)
- 類別裡面可以寫一個方法 
model範例
{
    public class HelloWorldBusiness
    {
        public string GetLabelText()
        {
            return "Hello World";
        }
    }
}
- 在controller裡面 ActionResult Index() 引用你要用的model
Controller內部程式引用model 範例
{
public class DefalutController : Controller
    {
        public ActionResult Index()
        {
            Model.HelloWorldBusiness business = new Models.HelloWorldBusiness();
            ViewBag.Label = "Hello MVC";
            ViewBag.Label = business.GetLabelText(); 
            return View();
        }
    }
}

{
// 提供員工資料增刪改查的服務
public class EmployeeService
{
    public int InsertEmployee(Models.Employee employee)  // 一個完整的Model也可以做為參數 (類似 String arg)
    {
        emplyee.Age; // 可以取到Model的內容
        return 0;
    }
    public class EmployeeSearchArg
    {
        [DisplayName("員工編號")]
        public string EmployeeId { get; set; }
        [DisplayName("員工姓名")]
        public string EmployeeName { get; set; }
        ...以此類推
    }
    public List<Models.Employees> GetEmployeeByCondition(Models.EmplyeeSearchArg arg)
    {
        List<Models.Employee> result = new List <Employee>(); //陣列寫法
        result.Add(new Employee() { EmployeeId = 1, EmployeeLastName = "123", Address = "中山北路" });
        result.Add(new Employee() { EmployeeId = 2, EmployeeLastName = "456", Address = "中山北路" });
        return result;
    }
}


- Controller呼叫 Model
public ActionResult Index()
{
    Models.EmployeeService employeeService = new Models.EmployeeService();
    var employees = employeeService.GetEmployeeByCondition(new Models.EmployeeSearchArg () // String INT都可以作為Function的參數 、 一個Object Function 也可以作為一個參數
    {
        EmployeeId = "1",
        EmployeeName = "aaa",
        ...
    });
    
    ViewBag.EmpAdd = employees[1].Address;
    
    return View();
}
}


View 顯示ViewBag方式
---

{
@ViewBag.EmpAdd
}

- 開發操作人員的Model
TIP: MS SQL Server 選取資料表按 ALT+F1 可以看到欄位型態
TIP: Visual Studio加上註解 按三個///
*增刪改查
*以強型別裝載資料
*先不實作資料庫存取

Views Folder
---

- 包含 Shared 資料夾
- Shared 資料夾 預設 View 檔名稱: _LayoutPage
- 在Controler的 index上 按右鍵->新增檢視
- 引用主板頁面: 使用版面配置頁 按下... -> View -> share 點選主板頁面 
- CSS、JS 的引入: 引入主板頁面

Controller & View 's Data Pass
---
若看不懂時 打開HTML按右鍵 查看原始碼 查看.NET轉換的CODE

- ViewDate: Controller to View
- ViewBag: Controller to View(MVC3)
從Server端包到前端:在controller設定ViewBag.Message 前端
- Model Binding: C2V、V2C

View Engine
---

- Controller: *Action *At Server Side
- View Engine: *Render Html *At Server Side (*.cshtml) (看到cs 運算在server端 運算完成傳送到User端)
- Html: *Pure Html *At Client Side

- 在cshtml 主板裡面 帶有@符號的 稱為 Razor
- 將資料寫在Controller  

Razor
---
cshtml
- @ViewBag.Label
- @foreach (var item in ViewBag.listData)  (tip:按完foreach 按兩下tab會有範例foreach跳出來)
- <span>@item</span>

cshtml 引用 jQuery
---

- <script type="text/javascript"> 打jqClick 按兩下TAB會生出Click function </script>
- jqDocReady 按下下TAB 生出 $(document).ready(function())
- 



Routing
---

- 目錄檔案在哪裡 ASP.NET URL呈現:localhost:XXXX/folder/file
- URL命名方式 (以下範例)  URL呈現:localhost:XXXX/Default/Index
範例
public class DefaultController : Controller
{
    public ActionResult Index()
    {
        ViewBag.Label = "Hello Routing";
        return View();
    }
}
- 在App_Start資料夾裡面的 RouteConfig.cs 命名規則
routes.MapRoute(
    name: "Default",
    url: "{controller}/{action}/{id}",
    defualts: new { controller = "Home", action = "Index", id = UrlParameter.Optional }
);

- 命名範例 URL: localhost:XXXX/Default/Index2
public class DefaultController : Controller
{
    public ActionResult Index2()
    {
        ViewBag.Label = "Hello Routing";
        return View();
    }
}

- id命名範例 URL: localhost:XXXX/About/Index/Rex
public class AboutController : Controller
{
    public ActionResult Index(string id)
    {
        ViewBag.Label = "Hello Routing" + id;
        return View();
    }
}


Area
--- 

- Area 按右鍵 新增區域 
在新增Area資料夾裡眠 DemoAreaRegistration.cs 裡面有 MapRoute() 定義URL


Controller
---

- Controller裡面的 Index 反白 按右鍵 新增檢視(View)
- Controller裡面的 Index 可以分 GET(預設) POST 若要使用POST則在相對應的index上 加上 [HttpPost()]
FORM範例程式碼
public ActionResult Index(FormCollection form) //Collection 陣列物件
{
    return View("index");
}

- Action Result 常用的
ViewResult 呈現指定或是預設的View      Controller Helper Methods : View
JsonResult 將.net物件序列化成Json格式並回傳   Controller Helper Methods : Json
範例程式碼:
public JsonResult TestJsonResult()  URL: localhost:XXXX/order/TestJsonResult
{
    Models.OrderService service = new Models.OrderService();
    return this.Json(service.GetOrderById(), JsonRequestBehavior.AllowGet);
}

Models 引入參考
---

- using System.ComponentModel.DataAnnotations;
- using System.ComponentModel;
- 定義驗證屬性
public class Order
{
    [DisplayName("訂單編號")]
    [Required()]
    public int OrderId (get;set;)
    
    [MaxLength(3)]
    [DisplayName("客戶代號")]
    public string CustId (get;set;)
}


Controller ActionResult
---

- Index反白 新增檢視 可以挑選你需要的範本 EX:INSERT 選擇 Create範本 模型類別: 你需要用到的Model 按下加入完成
- 如果要新增東西的FORM    INDEX沒有加上 [HttpPost()] 的話有可能新增會出現問題
	
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

View
---

- Html.EditorFor
EditFor
*可依照對應的屬性類別生成控制項
*String => text
*bool   => checkbox

@Html.EditorFor(model => model.JobTitleName, new { htmlAttributes = new { @class = "form-control" } })

- Html.TextBoxFor   // 盡量使用這個   // WorkShop將 EditorFor換成 TextBoxFor
TextBoxFor
*生成到Html型態為Input
*可以指定Type(date, datetime)
*不能使用 htmlAttributes

@Html.TextBoxFor(model => model.JobTitleName, new { @class = "form-control"})

Html Helper
---
- Html.XXX
*協助產生Html語法
*若要Mapping Action的參數，要自行指定DOM Name

- Html.XXXFor
*可直接繫結Model(強型別)
*送出後直接Mapping Action的參數

- Model寫某一欄位是必須要的值
namespace ViewHtmlHelper.Models
{
    public class Employee
    {
        [Required()]  // 欄位為必填
        public string EmployeeNo { get; set; }
    }
}
- 在Controller裡面判斷欄位是否合法
if (ModelState.IsValid){}

DropDownList
---
- DropDownList程式範例 (在Controller)
List<SelectListItem> (name) = new List<SelectListItem>();
jobTitleData.Add(new SelectListItem()
{
    Value = "PG",
    Text = "程式設計師"
});
jobTitleData.Add(new SelectListItem()
{
    Value = "SA",
    Text = "系統分析師"
});
- View (cshtml檔案)
<div class="form-group">
    @Html.LabelFor(model => model.JobTitleName, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        @Html.DropDownListFor(model => model.JobTitleCode, (List<SelectListItem>) ViewBag.JobTitleData, "請選擇...")
        @Html.LabelFor(model => model.JobTitleCode, "", new { @class = "text-danger" })
    </div>
</div>

ViewBag.JobTitleData = jobTitleData;
return View(employee);


Ajax
---

- Ajax Get
$("#btnAjaxGet").click(function (e)) {
    e.preventDefault();
    $.ajax({
        type: "GET",
        url: "/Default/AjaxGet?arg=1234",
        dataType: "json",
        success: function (response) {
            console.log(response);
        },
        error: function (error) {
            alert("some thing error");
            console.log(error);
        }
    });
}

- JsonResult
[HttpGet()]
public JsonResult AjaxGet(string arg)
{
    List<SelectListItem> result = new List<SelectListItem>();
    result.Add(new SelectListItem() { Value = "PG", Text = "程式設計師" });
    result.Add(new SelectListItem() { Value = "SA", Text = "系統分析師" });
    
    return this.Json(result, JsonRequestBehavior.AllowGet);
}

- Ajax POST
$("#btnAjaxPost").click(function (e)) {
    e.preventDefault();
    var postBody = {
        "Arg1": "1234",
        "Arg2": "abcd"
    }
    $.ajax({
        type: "POST",
        url: "/Default/AjaxPost",
        data: postBody,
        dataType: "json",
        success: function (response) {
            console.log(response);
        },
        error: function (error) {
            console.log(error);
        }
    });
}

- JsonResult
[HttpPost()]
public JsonResult AjaxPost(Models.AjaxPostArg arg)
{
    List<SelectListItem> result = new List<SelectListItem>();
    result.Add(new SelectListItem() { Value = "PG", Text = "程式設計師" });
    result.Add(new SelectListItem() { Value = "SA", Text = "系統分析師" });
    
    return this.Json(result);
}


ADO.NET
---

- MS SQL (連線字串)
Data Source = dc-training;  // DB Server 名稱(IP)
Initial Catalog = TSQL2012; // 資料庫名稱
User ID = sa;                // 帳號
PassWord = tds655;          // 密碼

- 建立連線
//連線字串
string connStr = @"Data Source = (PC-SQLexpress); Initial Catalog = TSQL2012; User ID = sa; Password = gss";
//建立Connection物件
SqlConnection conn = new SqlConnection(connStr);
//撰寫SQL語法
string sql = "SELECT * FROM [HR].[Employees]";    // 嚴禁使用串接字串連接SQL
//宣告一個SqlDataAdapter 並將Connection及SQL語法傳入
SqlDataAdapter dataAdapter = new SqlDataAdapter(sql, conn);
//宣告DataSet物件
Dataset ds = new DataSet();
//填入資料
dataAdapter.Fill(ds);

- 正確應該選用
string sql = "SELECT * FROM [HR].[Employees] WHERE EmployeeID = @EmployeeID";
SqlCommand cmd = new SqlCommand(sql, conn);
cmd.Parameters.Add(new SqlParameter("@EmployeeID", this.textBox.Text));

- DataTable
DataTable dtEmp = ds.Tables[0];
DataTable dtCustomer = ds.Tables[1];

- INSERT SQL 語法
string sql = @"INSERT INTO [Sales].[Shippers] (CompanyName, Phone) Values(@CompanyName, @Phone) SELECT SCOPE_IDENTITY()";

SqlCommand cmd = new SqlCommand(sql, conn);
cmd.Parameters.Add(new SqlParameter("@CompanyName", "GSS"));
cmd.Parameters.Add(new SqlParameter("@Phone", "25867890"));

conn.Open();

int newId = Convert.ToInt32(cmd.ExecuteScalar());

conn.Close();

- TRANSACTION SQL 語法
string sql = @"DELETE FROM [Sales].[Shippers] WHERE ShipperID = @ShipperID";

SqlCommand cmd = new SqlCommand(sql, conn);
cmd.Parameters.Add(new SqlParameter("@ShipperID", "4"));
cmd.Parameters.Add(new SqlParameter("@CompanyName", "叡揚資訊"));

conn.Open();
//從Conn物件啟用Transaction
SqlTransaction tran = conn.BeginTransaction();
//把Transation指定給Command物件
cmd.Transaction = tran;

try
{
    cmd.ExecuteNonQuery();
    //成功Commit
    tran.Commit();
}
catch (Exception)
{
    //若失敗則恢復
    tran.Rollback();
    throw;
}
finally
{
    //最後把連線關閉
    conn.Close();
}


實作注意
---

-將連線字串抽到Config
方案總管的參考 按右鍵 將SystemConfiguration加入參考

-在App.config/Web.config 設定連線字串

<connectionStrings>
    <add name="Default" connectionString="Data Source = (PC-SQLexpress); Initial Catalog = TSQL2012; User ID = sa; Password = gss" />
</connectionStrings>

-在程式內取得連線字串
private string GetConnStr()
{
    return System.Configuration.ConfigurationManager.ConnectionStrings["Default"].ConnectionString;
}


SQL 連線 額外參考網站
---
https://msdn.microsoft.com/zh-tw/library/system.data.sqlclient.sqlcommand.executescalar(v=vs.110).aspx
https://msdn.microsoft.com/zh-tw/library/system.data.sqlclient.sqlcommand.executenonquery(v=vs.110).aspx



Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `Dot Net`
