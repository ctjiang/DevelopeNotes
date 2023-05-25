# Mac
## Unable to configure HTTPS endpoint
無法使用像 https://localhost:7170/WeatherForecast 的方式測試WebAPI

#### Describe the bug
I am using Apple silicon MacOS. I have an existing dotnet 6 project which is working fine.
I install dotnet 7 using visual studio for mac.
After upgrading to dotnet 7, the project just cannot run.
System.InvalidOperationException: Unable to configure HTTPS endpoint. No server certificate was specified, and the default developer certificate could not be found or is out of date. To generate a developer certificate run 'dotnet dev-certs https'. To trust the certificate (Windows and macOS only) run 'dotnet dev-certs https --trust'. For more information on configuring HTTPS see https://go.microsoft.com/fwlink/?linkid=848054. 

#### 解決方式
- 清除所有的dotnet dev-certs https, 可以用Keychain Access或dotnet dev-certs https --clean
- 確定 ~/.aspnet/dev-certs/https directory下的所有檔案清除

之後再執行以下的動作  

dotnet dev-certs https --clean  
sudo dotnet dev-certs https --clean  
dotnet dev-certs https  
dotnet dev-certs https --trust  
dotnet dev-certs https --check --trust  

如此才能將所有包含user/sudo所產生的certifcate都清除，HTTPS才會正常運作

## 無法用IP位置連線
無法使用像 https://192.168.2.11:7170/WeatherForecast 的方式測試WebAPI

#### 解決方式
\<project folder\>/Properties/launchSettings.json  檔案中，
profiles/https/applicationUrl的屬性值，改成
> https://0.0.0.0:7170/WeatherForecast  

的形式

# Windows
