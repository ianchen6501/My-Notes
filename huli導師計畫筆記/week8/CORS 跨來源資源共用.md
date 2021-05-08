# CORS 跨來源資源共用
### 非同一個資訊來源
> 來自於不同網域（domain）、通訊協定（protocol）或通訊埠（port）的資源時

### 跨源請求(cross-origin HTTP request)
> 基於安全性考量，程式碼所發出的跨來源 HTTP 請求會受到限制。例如，XMLHttpRequest 及 Fetch 都遵守同源政策（same-origin policy）。
> 如果要跨源請求，server 端的 header 會有下面的字串

``Access-Control-Allow-Origin:``

###### tags: `week8`