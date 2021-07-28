# 0628 Course 6 Note

View the .Net MVC Fronted End Notes with HackMD.

Backend Basic
---

- 好的系統也要可以好維護
- 程式要夠彈性，程式碼要方便抽換
不要過度設計
透過黑箱的封裝把醜陋的Code包起來也是一種方式

Layer
---

- 缺點
*程式數目變多
*開發時不夠直覺
捨棄事件式的開發模式

*沒有良好的規劃溝通可能導致程式出現在不對的地方
例如在Service寫SQL

*沒規劃好，最後索性照著UI需求寫每一層的程式

- 優點
*各司其職
程式數目變多但是每支程式都專注在他該做的事

*強迫開發人員做思考每一層該做甚麼事
*開發期間不用等到實作完就可以給使用者使用
*方便抽換
*讓程式更具備可測試性

Log4Net
---

- 詳細參閱:
https://www.dotblogs.com.tw/yuanlin/archive/2012/05/30/72479.aspx
- Logger
以後專案實作發生問題時包在Try、Catch 能夠在Log檔找到程式的問題

Project.Dao
---

- Dao留下與資料庫有關的程式碼
- 可以在Dao裡面創建TestDao來測試資料庫令前端人員可以繼續實作
- Test結束後可以快速更改 TestDao 到原本的 Dao 檔案

IOC DI
---

- 在(Name)Dao的程式碼裡面將public class (Name)Dao 選起來
點選快速控制項目及重構 -> 會生出一個 I開頭的Dao(I代表 Interface)
之後能夠在public class TestDao 後面加上:I(Name)Dao 繼承Interface
毛毛蟲按自動補上實作內容 (擷取介面)
將Service 裡面 (專案名稱).Dao.(Name)Dao -> (專案名稱).Dao.I(Name)Dao 後面new = 你要使用的Dao 

工廠模式
---
- 工廠模式:
https://www.dotblogs.com.tw/joysdw12/archive/2013/06/23/design-pattern-simple-factory-pattern.aspx
- 在Service裡面加入(Name)Factory
- 在Factory裡面
Common.ConfigTool.GetAppsetting("DaoInTest")
- 在MVC專案中的 Web.config中appSetting 新增 key
(<add key="DaoInTest" value="Y" />)

Spring .NET
---
- 參考網站
http://springframework.net/
http://www.dotblogs.com.tw/hatelove/archive/2009/09/17/10686.aspx

- 使用Spring都需要將 Service & Dao 抽出Interface
- 工具 -> Nuget封裝管理員 -> 管理方案的Nuget套件 -> 在Nuget安裝 Spring.Core (Spring.NET) 勾選 MVC專案、Service、Dao
- 同以上方式 安裝 Spring.Web.MVC5 勾選 (MVC專案)
- 修改Global.asax.cs 以後使用時輸入 原本是 System.Web.(應用程式名稱) Spring.Web.Mvc.(應用程式名稱)
- 調整Web.config 加入 Spring區段

```html
<configSections>
<sectionGroup name="spring">
  <section name="context" type="Spring.Context.Support.MvcContextHandler, Spring.Web.Mvc5" />
  <section name="objects" type="Spring.Context.Support.DefaultSectionHandler, Spring.Core" />
  <section name="parsers" type="Spring.Context.Support.NamespaceParsersSectionHandler, Spring.Core" />
</sectionGroup>
</configSections>
```
  
- 調整Web.config 加入

```
<spring>
<context>
  <resource uri="file://~/spring-config\objects.xml" />
</context>
</spring>
```
  
- 撰寫Spring設定檔 在MVC專案新增資料夾 spring-config (裡面新增檔名objects.xml)

```
<?xml version="1.0" encoding="utf-8" ?>
<objects xmlns="http://www.springframework.net">

  <object id="EmployeeController"  type="NewHR.Controllers.EmployeeController,NewHR" singleton="false">
    <property name="codeService" ref="CodeService" />
    <property name="employeeService" ref="EmployeeService" />
  </object>

  <object id="CodeService" type="eHR.Service.CodeService,eHR.Service">
    <property name="codeDao" ref="CodeDao" />
  </object>

  <object id="EmployeeService" type="eHR.Service.EmployeeService,eHR.Service">
    <property name="employeeDao" ref="EmployeeDao" />
  </object>  
  
  <object id="CodeDao" type="eHR.Dao.CodeDao,eHR.Dao"/>
  <object id="EmployeeDao" type="eHR.Dao.EmployeeTestDao,eHR.Dao"/>

</objects>
```

- 之後設定object.xml時 透過專案點右鍵 -> 屬性 -> 應用程式 可以查看名稱 命名空間
- MVC專案 Nuget安裝 Microsoft.AspNet.WebApi 套件








Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `Dot Net`
