# AndroidCordova1
學習Android Cordova:學習創建Cordova項目，使用Cordova插件Camera，通過js調用Android系統Camera

## 項目簡介
  學習Cordova,創建Cordova項目，使用AS打開Cordova項目，使用Cordova安裝插件，並且使用Cordova Camera插件調用系統相機功能。

## 項目結構
  Cordova項目結構介紹，以及使用插件簡介。
  
###  Cordova項目結構介紹   
    Cordova創建項目目錄結構：   
    hello項目文件夾下：
      hooks文件夾：鉤子；    
      node_modules文件夾:node.js的對應cordova使用模塊；   
      platforms文件夾：Cordova生成對應平台的項目文件，這裡我們使用cordova platforms add android，生成android項目，
      後面使用AS可以直接導入platforms/android項目。     
      plugins文件夾:cordova插件目錄，Cordova項目安裝的插件。   
      www文件夾:頁面文件，包括css,js,html等文件；    
      config.xml:配置文件，記錄Cordova項目id,項目名，以及使用的插件，頁面過濾規則；    
      package.json:項目信息json格式文件；
      package-lock.json:denpendences的版本信息；   
      
### Android Cordova應用結構
   我們開發Android移動應用，需要的是platforms下面生成的andorid項目。直接使用As，import目錄platforms/android項目。   
   Android項目結構視圖：     
      CordovaLib文件夾，這個相當于一個依賴，使用Cordova相關東西。     
      assets文件夾：
      www文件夾下：css,js,html文件等，結構和hello的項目文件夾下相同，相當一個copy。但當我們在As修改www中文件，就和hello項目下不一樣了，
      它是不會影響到hello項目下www文件夾的。   
        index.html:項目主界面；   
        css目錄：css樣式文件；   
        js目錄：js動作文件；   
        plugin.cordova-plugin-camera.www文件夾：cordova-plugin-camera插件使用的js文件；   
        cordova-js-src:Cordova項目生成的js文件；    
     java文件夾：   
         MainActivity:項目主 Acitivity;     
         org.apache.cordova包下：是使用的插件的對應Class文件；   

### 簡單Camera插件使用
    index.html文件：加入一個按鈕，點擊調用camera進行拍照；   
            <div>
                <button  id="button1">點擊拍照</button>
                <img src="" id="image1" style="width:200px;height:200px;"/>
            </div>
    index.js文件：為按鈕註冊點擊事件，編寫事件處理，調用Cordova Camera插件提供的js功能；    
            //添加點擊事件監聽
            document.getElementById("button1").addEventListener("click",takePhoto,true);
            //拍照函數
            function takePhoto(){
                //拍照
                navigator.camera.getPicture(successMethod,failMethod,
                {destinationType:Camera.DestinationType.FILE_URL,
                sourceType:Camera.PictureSourceType.CAMERA,
                quality:75});
            }
            //拍照成功
            function successMethod(imageUrl){
                console.log("lujie:"+imageUrl);
                var image1 = document.getElementById("image1");
                image1.src = imageUrl;
            }

            //拍照失敗
            function failMethod(message){
                navigator.notification.alert("拍照失敗："+message);
            }

           

      
