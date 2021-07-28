# 0628 Course 1 Note Version Control

View the Notes with HackMD.

註解範例
---

/// desciption 1
///	desciption 2
///	desciption 3
///	desciption 4
///	desciption 5

執行程式時養成 Error Handle
---

使用Try Catch 處理例外狀況

try
{
	// do something...
}

///	不要在catch中吃掉錯誤
///	盡量不要在 catch 中在使用 try catch
/// catch 中 re-throw exception 時，注意寫法，避免 stack trace 被吃掉

catch (Exception ex)		
{
	// 出錯、發上異常
}
finally
{
	// try catch 結束後，會進到Finally
}

避免
---

Magic Number/String
- 日後改變就要重新調整的程式變數
- 別人無法理解程式碼中數字含意的程式碼

如何避免
- 定義為常數、Enum
- 統一寫在設定檔案、資料庫、使用時再取用

版本控制
---

- 能追蹤工程藍圖從誕生到定案的過程
- 確保不同人所編輯的同一檔案都能夠同步

常見的版本控管模型
---

- 集中式:只有一個版本庫、簡易操作、方便管理		(Subversion)
- 分散式:遠端一個版本庫、本地端亦可控管版本		(Git)

版本控管實作
---

共通
- Repository
		>>版本庫、Repo
		>>SVN : 只有 Server 版本庫
		>>Git : 可分 Server 跟 Client 端
- Working Dictionary
		>>Working Folder，工作區，本機上的工作目錄
- Branch
		>>針對不同目的或不同版本開出各別版本庫
- Tag
		>>針對特定版本做記號
- Merge
		>>合併兩個不同分支或版本的程式碼
- Conflict
		>>Merge 過程版本不一致造成的衝突

Subversion
- Checkout
		>>把版本庫程式拉到本機
- Update
		>>從版本庫更新程式到本機
- Commit
		>>將程式上傳到版本庫

Git
- Clone
		>>把 Server 版本庫程式拉到本機
- Pull
		>>從 Server 版本庫更新程式到本機
- Commit
		>>將程式上傳到本機端版本庫
- Push
		>>將程式上傳到本機版本庫

Subversion-工作流程
---

GET程式碼 		 -> 	 Check Out
修改程式碼		->		Working Folder
上船程式碼		->		Commit

Subversion 第一次上傳
---

- 空白處按右鍵 SVN CheckOut (事先準備好 gsssvn) 檢查網址與工作目錄
- 上傳寫好的程式碼	  ->  空白處按右鍵 git commit  ->  輸入Memo  ->  點選 ALL 按 OK
- 修改完成上傳程式碼  ->  修改好的檔案按右鍵 git commit  ->  輸入Memo  ->  點選OK
- 確定版本數		  ->  空白處按右鍵 TortoiseSVN 按 Repo-Browser
- 若有發現不同版本    ->  在Repo-Browser上 指定檔案按右鍵 show log 
- 比較兩版本不同      ->  在show log 中點選不同版本後按右鍵 Compare revisions
- 有修改過的commit    ->  ICON會呈現紅色
- 若有衝突版本		  ->  ICON會呈現黃色  ->  右鍵按notepad++ 可以觀看不同版本差異
- 解衝突  			  ->  衝突檔案按右鍵  ->  Conflict Edit  ->  選擇需要的版本  ->  Use text block from 'mine' before 'theirs'  ->  坐上角 Save File
- 更新本機端版本      ->  空白處按右鍵    ->  Update
養成好習慣 先UPDATE確保版本 降低衝突發生 

Git-工作流程
---

- 每次開工前先Pull更新
- 寫到一個段落或功能完成就 Commit ， 不要整個專案都完成了 commit 數量才一兩次
- Commit 完要記得 Push
- Commit 訊息不要亂打 讓人能夠快速理解

GET程式碼		->		Clone
修改程式碼		->		Working Folder
提交程式碼		-> 		Commit
上傳程式碼		->		Push

Git 常用操作指令
- init, clone, add, commit, push, pull, log, status, branch, checkout

建立Repo
- Git Init

取得Repo
- Git Clone
	
改好程式加入版本紀錄
- Git Commit
	
把本地的Repo推送到遠端
- Git Push
	
將遠端的 Repo 更新到本地
- Git Pull

Git實作
---
	
- Unstaged Files 按加號 變成 Staged Files  >>  輸入Commit指令 按下Commit  >>  按上面 Push
- GitLab 與 Source Tree 的 History 可以看到 Commit Log 跟修改內容

- Commit 前有人Push新的東西到遠端  >>  上面按鈕 Pull 更新

遇到衝突
---

- 反白檔案按右鍵  >>  點 Resolve Conficts  >>  選 Resolve Using (取用版本)  {不是所有狀況都能夠直接選擇某一邊版本}

建立分支
---
- Branch  >>  設定 Branch 名稱
- (Working Copy Parent) 從 master 的頂端生出分支
- (Specified Commit) 從特定的分支生出節點

合併分支
---
- 自己的分支按右鍵 Merge [Branch Name] into current branch
	
- 不適合或不需要上版控的東西
含有密碼或是金鑰的設定檔
程式編譯產生的檔案
透過套件管理工具管理的第三方套件
	
	
- 若今天實際需要 commit 的只有一個檔案	打開 SourceTree卻發現待處理的檔案清單非常多 沒辦法輕易找到要commit的檔案
在 Folder 中加入 .gitignore			即可解決問題
	

- .gitignore Template
github/gitignore		gitignore.io


Rex Tsou 2021/06/28

###### tags: `Work` `Sample`
