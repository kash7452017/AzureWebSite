## 將ASP.NET網站發佈至Azure

> 以下操作將說明如何將完成的網站以及SQL Server資料庫成功佈署到Azure，初次佈署有遇到一些狀況，因此在此紀錄每個動作，希望可以幫助到有需要的人，也可避免日後忘記可查看，在此附上我的[簡易購物網站鏈結](https://shoppingwebsite.azurewebsites.net/)
> 
>> 進行以下操作時，請先於Microsoft Azure[入口網站](https://portal.azure.com/)註冊帳號，方可使用其資源

* **步驟1**
###### 於Azure入口網站選取`應用程式服務`，點選`建立`，我們將開始創建佈署網站相關資源
![image](https://user-images.githubusercontent.com/101872264/162607485-baba3f91-bf04-429b-84f3-518f5e96c675.png)

* **步驟2**
###### 按照所需填選欄位依序操作，若是初次使用Microsoft Azure`資源群組`為空者，可點選`新建`創建新的資源組，名稱可自行定義，`執行個體詳細資料`中的名稱，即為後續將發佈之網站的名稱，將呈現為`https://[WebName].azurewebsites.net`
###### `執行階段堆疊`依照使用者開發網站時所使用的環境做選取，我是使用ASP.NET開發，因此選取`.NET 6(LTS)`
###### `App Service方案`可依照需求進行設定與方案選取
###### 按照圖片所示禁行操作後，點選`建立`，系統會開始為我們所需環境進行創建
![image](https://user-images.githubusercontent.com/101872264/162607643-1dc835fd-223a-4628-8630-bb505faba7e3.png)

* **步驟3**
###### 此步驟將說明如何創建資料庫伺服器，以便後續發佈資料庫使用
###### `伺服器名稱`可自行定義，會呈現為`[伺服器名稱].database.windows.net`
###### `管理員名稱`以及`密碼`為後續登入的重要資訊，請務必記得
###### 按照步驟輸入完畢後，點選`建立`，系統將自動為我們創建所需環境
![image](https://user-images.githubusercontent.com/101872264/162607654-d0a5c265-9fad-46bb-b96c-f012b1043d8c.png)


* **步驟4**
###### 步驟3我們已完成伺服器的建立，接著我們需要在此伺服器下建立我們所需用到的資料庫，`資料庫名稱`可對應本地SQL Server中的資料庫名稱，也可自行定義，方便後續分辨即可，`伺服器`選取我們剛剛所建立的伺服器，點選`建立`即可
###### `計算 + 儲存體`可以個人需求設定
###### 須注意!!本地端SQL Server若有1個以上資料庫，此處也需創建對應數量的資料庫
![image](https://user-images.githubusercontent.com/101872264/162607670-5f1864e6-a626-48d5-bfa0-1c7def0ef471.png)

* **步驟5**
###### 進行連線前，須完成`防火牆IP設定`，將用戶端IP加入，並選取`是`，允許Azure服務和資源存取此伺服器，設定完畢點選`儲存`即可
![image](https://user-images.githubusercontent.com/101872264/162607677-a46e1283-5388-40ce-bdb6-e304513ff6ca.png)

* **步驟6**
###### 以上步驟我們已完成發佈Azure的前置作業，接著我們要開始進行將本地端網站發佈到Azure的動作
###### 在VS`檔案總管`中，點選專案右鍵，選取`發佈`-> `Azure` -> `App Service[Windows]` -> 選取我們剛剛建立的App Service執行個體 -> `完成`
![image](https://user-images.githubusercontent.com/101872264/162607681-47d3542e-12a3-438e-9fff-5c99ef7e1d55.png)

* **步驟7**
###### 點選`發佈`，系統開始將網站發佈到Azure，完成後可看到下方出現`建置成功` `已成功發佈`，將自動開啟網站
![image](https://user-images.githubusercontent.com/101872264/162607694-d5a63a89-bbc6-4c6a-ba5b-6483cfcd1c78.png)
###### 開啟網站後出現此錯誤訊息不必擔心，因我們目前只有先發佈網站，資料庫尚未發佈上去，因此與資料庫相關的動作皆會出現`處理要求時發生錯誤`
###### 目前進行到這，當你看到這個畫面時，你已完成一半了!!
![image](https://user-images.githubusercontent.com/101872264/162607703-6065bb48-cc30-40a2-b6b9-996e72304fae.png)

* **步驟8**
###### 在Azure選取我們剛剛建立的資料庫伺服器，複製伺服器名稱，開啟SSMS進行連線，此處的登入使用者以及密碼為創建伺服器時所設定的名稱及密碼
![image](https://user-images.githubusercontent.com/101872264/162607709-558f5271-c408-41a5-8906-03ecd3b44b12.png)

* **步驟9**
###### 連線成功後，點開`資料庫`節點，可看到我們剛剛在Azure上所建立的資料庫`DB1`，將本地端的資料庫sql檔案匯入，並在上方選取目標資料庫`DB1`，點選執行，建立相關資料表
![image](https://user-images.githubusercontent.com/101872264/162607717-1ef4580e-5845-46aa-a40d-d263295bbf6a.png)

* **步驟10**
###### 成功執行後可看到DB1資料庫中成功建立所需資料表，右圖為完整資料庫資訊，因使用到兩組資料庫，須個別執行對應的sql語法建立個別資料表，同時在`步驟4`也要建立對應的資料庫數量，此部分需特別注意
![image](https://user-images.githubusercontent.com/101872264/162607726-cc8cf1a3-6aeb-4678-924e-4771529dd565.png)

* **步驟11**
###### 此步驟我們將替換掉現有的edmx檔案，在專案`Models`中找到對應的edmx檔案，`點選右鍵將其刪除`，並重新加入新的`ADO.NET模型`，名稱可自行定義，容易辨別即可
![image](https://user-images.githubusercontent.com/101872264/162607731-570c4aef-0479-46f5-bcdc-fc8ad350b082.png)

* **步驟12**
###### 選擇`來自資料庫的EF Designer` -> `新增連接`，輸入Azure創建的資料庫伺服器名稱，選擇`SQL Server驗證`，輸入使用者名稱及密碼，下方選擇將進行連接的資料庫名稱`DB1`，可點選測試連接以確認是否成功，完成後點選確定
![image](https://user-images.githubusercontent.com/101872264/162607741-f09fc84d-7e52-4b69-9293-e6c2684e734e.png)

* **步驟13**
###### 此步驟須注意，請選取`是，在連接字串中包含敏感性資料`，勾選`資料表`選取要導入的資料庫物件，點選完成即可
![image](https://user-images.githubusercontent.com/101872264/162607752-8716ea9b-9cd0-47a1-9f59-e4ab801f0394.png)

* **步驟14**
###### 加入完畢，請重新建置專案，會發現有很多錯誤訊息，這是因為由於我們的資料庫模型更動了，須將原先的資料庫模型名稱全部替換成我們目前建立的模型名稱，如下圖所示，將左圖中的錯誤，替換成右圖更動後的名稱
###### 若有多組資料庫，除了`步驟4`以及`步驟9`，還需重複執行`步驟11`~`步驟14`，將所有錯誤訊息替換掉重新建置完成即可
![image](https://user-images.githubusercontent.com/101872264/162607762-1ef2198b-c1c6-4e2a-866a-b70539be28d6.png)

* **步驟15**
###### 完成新資料庫模組導入後，可在Web.config檔案中看到，連線字串已自動加入
###### 同時也可替換掉`DefaultConnection`的連線字串，如此一來，在本地端執行程式也可連接到Azure上的資料庫
###### 連線字串中的User id以及Password已隱藏，請自行更改為對應的使用者名稱及密碼
###### 所有操作皆完成後，請再次進行發佈，以更新Azure上的網站資料
```
<add name="db1Entities" connectionString="metadata=res://*/Models.dbModel.csdl|res://*/Models.dbModel.ssdl|res://*/Models.dbModel.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=mytestdbserver123456.database.windows.net;initial catalog=db1;user id=[UserName];password=******;MultipleActiveResultSets=True;App=EntityFramework&quot;" providerName="System.Data.EntityClient" />
```
![image](https://user-images.githubusercontent.com/101872264/162607767-814c684e-9732-4505-ae80-baea5259508e.png)

* **步驟16**
###### 若要查詢或新增資料，可在Azure上選取資料庫並進入`查詢編輯器(預覽)`，選取`編輯資料(預覽)` -> `建立新的資料列`，更動完畢請記得點選`儲存`
![image](https://user-images.githubusercontent.com/101872264/162607775-b19704d1-d970-4f7c-a2bc-cca339ca4abc.png)

* **步驟17**
###### 以上步驟皆完成後，恭喜你，已成功將網站以及資料庫佈署到Azure囉
![image](https://user-images.githubusercontent.com/101872264/162607786-09bd4e0d-9cd1-4395-a027-4c25c68e4c90.png)
