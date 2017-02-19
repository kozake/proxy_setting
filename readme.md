# プロキシの設定方法

## NPM

以下のコマンドを用いて設定してください。

```
npm config set proxy http://username:password@host:port
npm config set https-proxy http://username:password@host:port
```

または、次のファイルを編集してください。

Windowsの場合は

`
C:\Users\[account_name]\.npmrc
`

Macの場合は

`
~/.npmrc
`

```
proxy=http://username:password@host:port
https-proxy=http://username:password@host:port
```

## Git

次のファイルを編集してください。

Windowsの場合は

`
C:\Users\[account_name]\.gitconfig
`

Macの場合は

`
~/.gitconfig
`

```
[http]
    proxy = http://username:password@host:port
[https]
    proxy = https://username:password@host:port

# プロキシ除外設定
[http "http://host:port/"]
    proxy = 
```

## Bower

次のファイルを編集してください。

Windowsの場合は

`
C:\Users\[account_name]\.bowerrc
`

Macの場合は

`
~/.bowerrc
`

```
{
    "proxy":"http://username:password@host:port",
    "https-proxy":"http://username:password@host:port" 
}
```

## Maven

次のファイルを編集してください。

Windowsの場合は

`
C:¥Users¥[account_name]¥.m2¥settings.xml 
`

Macの場合は

`
~/.m2/settings.xml 
`

```
<settings>
    <proxies>
        <proxy>
            <id>http</id>
            <active>true</active>
            <protocol>http</protocol>
            <username>username</username>
            <password>password</password>
            <host>host</host>
            <port>port</port>
            <nonProxyHosts>nonProxyHosts</nonProxyHosts>
        </proxy>
        <proxy>
            <id>https</id>
            <active>true</active>
            <protocol>https</protocol>
            <username>username</username>
            <password>password</password>
            <host>host</host>
            <port>port</port>
            <nonProxyHosts>nonProxyHosts</nonProxyHosts>
        </proxy>
    </proxies>
</settings>
```

## Gradle

次のファイルを編集してください。

Windowsの場合は

`
[your_project]¥gradle.properties
[your_project]¥gradle¥wrapper¥gradle-wrapper.properties
`

グローバル設定を変更するならこちら

`
C:¥Users¥[account_name]¥.gradle¥gradle.properties
`

Macの場合は

`
[your_project]/gradle.properties
[your_project]/gradle/wrapper/gradle-wrapper.properties
`

グローバル設定を変更するならこちら

`
USER_HOME/.gradle/gradle.properties
`

```
## Proxy setup
systemProp.proxySet="true" 
systemProp.http.keepAlive="true" 
systemProp.http.proxyHost=proxyHost
systemProp.http.proxyPort=proxyPort
systemProp.http.proxyUser=proxyUser
systemProp.http.proxyPassword=proxyPassword
systemProp.http.nonProxyHosts=nonProxyHosts1|nonProxyHosts2

systemProp.https.keepAlive="true" 
systemProp.https.proxyHost=proxyHost
systemProp.https.proxyPort=proxyPort
systemProp.https.proxyUser=proxyUser
systemProp.https.proxyPassword=proxyPassword
systemProp.https.nonProxyHosts=nonProxyHosts1|nonProxyHosts2
## end of proxy setup
```

**注意**

Java 8 Update 111 (8u111)の変更点である「HTTPSトンネリングのBasic認証の無効化」により、Java 8 Update 111以降でGradle Wrapperを取得しようとすると、以下のようなエラーが発生する場合があります。

（参考）
https://www.java.com/ja/download/faq/release_changes.xml

```
Exception in thread "main" java.io.IOException: Unable to tunnel through proxy. Proxy returns "HTTP/1.0 407 Proxy Authentication Required" 
        at sun.net.www.protocol.http.HttpURLConnection.doTunneling(HttpURLConnection.java:2124)
        at sun.net.www.protocol.https.AbstractDelegateHttpsURLConnection.connect(AbstractDelegateHttpsURLConnection.java:183)
        at sun.net.www.protocol.http.HttpURLConnection.getInputStream0(HttpURLConnection.java:1546)
        at sun.net.www.protocol.http.HttpURLConnection.getInputStream(HttpURLConnection.java:1474)
        at sun.net.www.protocol.https.HttpsURLConnectionImpl.getInputStream(HttpsURLConnectionImpl.java:254)
        at org.gradle.wrapper.Download.downloadInternal(Download.java:58)
        at org.gradle.wrapper.Download.download(Download.java:44)
        at org.gradle.wrapper.Install$1.call(Install.java:61)
        at org.gradle.wrapper.Install$1.call(Install.java:48)
        at org.gradle.wrapper.ExclusiveFileAccessManager.access(ExclusiveFileAccessManager.java:65)
        at org.gradle.wrapper.Install.createDist(Install.java:48)
        at org.gradle.wrapper.WrapperExecutor.execute(WrapperExecutor.java:128)
        at org.gradle.wrapper.GradleWrapperMain.main(GradleWrapperMain.java:61)
```

エラー対策として、「jdk.http.auth.tunneling.disabledSchemes」システム・プロパティを"" (空)に設定してください。

（例）

```
gradlew -Djdk.http.auth.tunneling.disabledSchemes="" tasks
```

## IntelliJ IDEA

File -> Settings... を選択し、Appearance & Behavior -> System Settings -> HTTP Proxyを選択してください。

設定画面にプロキシ設定を入力してください。

## VSCode

ファイル(F) -> 基本設定(P) -> ユーザー設定(U) を選択し、settings.jsonに次の技術を追加してください。

```
// 既定の設定を上書きするには、このファイル内に設定を挿入します
{
        // 使用するプロキシ設定。設定されていない場合、環境変数 http_proxy および https_proxy から取得されます。
    "http.proxy": "http://username:password@host:port/",

    // 提供された CA の一覧と照らしてプロキシ サーバーの証明書を確認するかどうか。
    "http.proxyStrictSSL": false
}
```
