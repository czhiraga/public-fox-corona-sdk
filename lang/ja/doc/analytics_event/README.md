# アクセス解析による課金イベント計測
アプリ内課金を利用していない売上をトラッキングするために、各パラメータを明示的に指定できます。 本機能では広告経由および自然流入経由での売上をそれぞれ計測可能です。
※広告経由の売上のみを計測したい場合はLTV計測で計測可能ですので本機能の実装は必要ありません。※主に自然流入経由の売上を計測したい場合などに本機能を実装してください。## Androidへの組み込み
課金イベントトラッキングの実装はNamedJavaFunctionインターフェースの配列に次の対象クラスを追記します。
* CoronaAnalyticsManagerクラス
**[Java記述例]**
クラスをインポート
```java
import jp.appAdForce.android.corona.CoronaAnalyticsManager;
```

課金イベントトラッキング実行クラスをNameJavaFunction配列に追加
```java
@Overridepublic void onLoaded(com.ansca.corona.CoronaRuntime runtime) {    com.naef.jnlua.LuaState luaState = runtime.getLuaState();    com.naef.jnlua.NamedJavaFunction[] luaFunctions;    luaFunctions = new com.naef.jnlua.NamedJavaFunction[] {        new CoronaAdManager.SendConversionWithStartPageUrl(),        new CoronaLtvManager(),        new CoronaAnalyticsManager(),        new CoronaAnalyticsManager.SendPurchaseEvent(),    }    luaState.register("foxPlugin", luaFunctions);    luaState.pop(1);}```
**[Lua記述例]**
```lua
// プラグインをインポート
Local Fox = require "plugin.fox"
Fox.sendPurchaseEvent(eventName,						action,						label,						orderId,						sku,						itemName,						price,						quantity,						currency);```## iOSへの組み込み
**[Lua記述例]**```lua
// プラグインをインポート
Local Fox = require "plugin.fox"
Fox.sendEventPurchase(eventName, action, label, orderID, sku, itemName, price, quantity, currency);```|パラメータ|タイプ|最大長|必須|概要|
|:---|:---:|:---:|:---:|:---|
|eventName|String|255|必須|トラッキングを行うイベントを識別できる任意の名前を設定します。<br>イベント名は自由に設定可能です。<br>イベント単位でグルーピングされ、それぞれのイベントごとに集計を行うことができます。||action|String|255|オプション|イベントに属するアクション名を設定します。<br>アクション名は自由に設定可能です。<br>各イベントをドリルダウンすることで、アクションごとに集計を行うことができます。<br>特に指定しない場合は””を設定してください。|
|label|String|255|オプション|アクションに属するラベル名を設定します。<br>ラベル名は自由に設定可能です。<br>各アクションをドリルダウンすることで、ラベルごとに集計を行うことができます。<br>特に指定しない場合は””を設定してください。||orderID|String|255|オプション|注文番号。特に指定いない場合は""を設定してください。|
|sku|String|255|オプション|商品コード。特に指定しない場合は””を設定してください。||itemName|String|255|必須|商品名||price|double||必須|商品単価|
|quantity|int||必須|購入数||currency|String||オプション|通貨コード。指定しなかった場合は"JPY"|