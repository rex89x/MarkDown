# VB DotNet MVC Code Note

ASPX Label Code
---

### aspx

```html
<Label id="Labelid">Label Name<Label>
```

### aspx.vb

```vb
Public Class (Project Name)
    Protected WithEvents Labelid As Label
```
    
ASPX Textbox Code
---

### aspx

```html
<Textbox id="Textboxid" required="True" MaxLength="3" Readonly="True">TextBox Name<Textbox>
```

### aspx.vb

```
Public Class (Project Name)
    Protected WithEvents Textboxid As Textbox
```
    
ASPX Button Code
---

### aspx

```html
<button id="buttonid"></button>
```

### aspx.vb

```vb
Public Class (Project Name)
    Protected WithEvents buttonid As button
    
Private Sub Name (ByVal sender As System.Object, ByVal e As System.Web.UI.ImageClickEventArgs) Handles buttonid.Click
    //Description......
End Sub
```

VB.NET Dynamic Search on Oracle Database
---

### aspx.vb

```
Private Sub SaveAction()
    Dim strSQL As String
    Dim objDV As DataView
    Dim result As String
    Dim objParam As Object() = {Me.id.Text}
    
    strSQL = "SELECT COUNT(*) AS Name FROM Table " _
           & " WHERE Column = \?S "
    strSQL = Me.objADODB.ConvertSQL(strSQL, objParam)
    objDV = Me.objADODB.OpenDataTable(strSQL).DefaultView
    result = objDV.Item(0)("Column")
```

VB.NET TABLE Code
---

### Table
```
<TABLE style="TABLE-LAYOUT: fixed" cellSpacing="0" cellPadding="0" width="100%" border="0">
    <TR>
        <TD align="left">
            <DataGrid>
                <ColumnDataTypes>
                    <DataType DataField="id" StringType="String" ReadOnly="False"></DataType>
                </ColumnDataTypes>
            </DataGrid>
            <Columns>
                <asp:BoundColumn DataField="id" HeaderText="Column Name"></asp:BoundColumn>
            </Columns>
        </TD>
    </TR>
</TABLE>&nbsp

// &nbsp 半形的不換行空格, 就是一班在鍵盤上的空白鍵產生空格
```

HTML 字元符號
---

### &nbsp
半形的不換行空格, 就是一班在鍵盤上的空白鍵產生空格

### &ensp
半形的空格, 特性為寬度是1/2個中文字寬度

### &emsp
全形的空格, 特性為寬度為1個中文字寬度

### Sample Code
```
<div>
    // 額外補充寫法 <span class="emsp"></span>
    <ul>
        <li>標 &emsp; &emsp; 題 &emsp;:</li>         //標　　題：
        <li>填 &ensp; 寫 &ensp; 人 &nbsp;:</li>      //填 寫 人：
        <li>連絡電話 &nbsp;:</li>                    //聯絡電話：
    </ul>
</div>
```

VB.NET 模糊查詢
---

### Sample Code
```sql
AND Trim(CUST_ID) = '%' || \?S || '%'
```








Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `Dot Net`