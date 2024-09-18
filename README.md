# iPickup Pro 使用說明

1.  根據你的作業系統和 CPU 架構，下載合適的 iPickup Pro 壓縮檔案 <https://github.com/ipickup-pro/releases/releases/latest>
2.  首次執行，打開 command prompt app (Windows系統下，執行 > CMD)，並移動路徑至解壓後 folder 位置，然後輸入以下指令以開啟設定介面，瀏覽器會打開網址 <http://localhost:9999>
    
    ```shell
    ipickup_pro-win-x64.exe --config
    ```
3.  設定完成後，於 command prompt app 輸入 bot 執行檔即可開始自動搶購的操作
    
    ```shell
    ipickup_pro-win-x64.exe
    ```
4.  程式啟動後，可於瀏覽器打開 dashboard，網址為 <http://localhost:5555> (位址中的 port 可於設定介面中修改)


# 常見問題 / FAQ


### config.yml 不能讀取

請檢查 YAML 格式是否正確 <https://codebeautify.org/yaml-validator>


### 如何加入其他型號/機款？

可添加至 `properties.yml` 的 `models` 如下:

```yaml
model-id: # 自定意的型號ID
  sku: SKU # Apple商品 part number / SKU
  name: NAME # 商品名稱
```


### Console 顯示的中文字為亂碼

-   Windows 10
    -   Control Panel -> Region

![img](https://i.imgur.com/XVzgFyb.png)

![img](https://i.imgur.com/jT3pNVc.png)


### **如何保存 log 或將程式放置於背後運作**

建議使用 [PM2](https://pm2.keymetrics.io/) ，於 bot 應用程式的 folder 內新增 `ecosystem.config.js` 內容如下：

```javascript
module.exports = {
  apps : [{
    name   : "ipickup-pro",
    script : "./ipickup_pro-linux-x64 -y",
    "args": [
      "--color"
    ],
    "env": { "DEBUG_COLORS": true }
  }]
}
```

執行輸入 `pm2 start` 即可。


### 常見的錯誤和處理方法

-   **訂單只能送貨**
    -   Apple Store 的風控管理，可調試不同的 delay 和開啟 `safe-mode` ，或使用 `browser-mode` (不建議，因 `browser-mode` 太慢和佔用較多資源)
    -   可使用[虚假信用卡](https://saijogeorge.com/dummy-credit-card-generator/)來測試有貨的商品，如設定能通過風控，會出現 card declined 的 error

-   **監察器未能獲取訊息**
    
    如果在 console 和 dashboard 的監察 bar 上持續顯示此訊息，則表示 IP ban，需切換 IP/proxy 或將 `interval` 的數值調高。

-   **登錄失敗，即將重試 / 不能打開頁面 / Server 未能接收請求, 即將重新提交&#x2026;**
    -   IP ban，需切換 IP/proxy
    -   如沒有足夠的 IP/proxy，則減少 Tasks 數量


### 問題回報及一般討論

TG群組: [iPickup Pro Chat 2024](https://t.me/+7t9rErmqZJQ2ODI1)
