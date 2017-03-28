# クロスプラットフォームなASP.NETアプリケーション開発

ASP.NETというとWindows環境でしか動作しないように思われている。

しかし、2016年11月に正式リリースとなったASP.NET Coreを使用することで、LinuxやMacでも動作するクロスプラットフォームなASP.NETアプリケーションの開発を行うことができる。

このテキストでは、ASP.NET CoreをVisual Studioを使用しないで開発を行う

## 前提条件
本テキストを進めるにあたり、以下を理解していることをおすすめする。
1. C#を書くことができる or Javaが理解し、書くことができる
2. コマンドでの操作に支障がない（OSの基本的なコマンド操作ができる）

## 説明環境
OS：macOS Sierra version 10.12.3
メモリ：4GB
CPU：Intel Core i5
.NET Command Line Tools：1.0.0-rc3

## 環境構築
1. .NET Coreのインストール

      [.NET Coreのページ](https://www.microsoft.com/net/download/core#/sdk)に各環境でのインストール手順が記載されているので、そちらを参照してインストールのこと

2. 新しいプロジェクトの作成
    1.  プロジェクト用のディレクトリを作成

        .NET Coreはプロジェクトファイルが含まれるディレクトリをプロジェクトのディレクトリとして認識する。

        今回は「TodoApp」というフォルダを作成する。

        ここからはコマンドでの操作が続くため、ターミナルを起動しておくとよい。

        ```
        # TodoAppのフォルダ作成
        mkdir TodoApp
        # カレントディレクトリをプロジェクトフォルダに変更
        cd TodoApp
        ```
    2. プロジェクトの作成
        dotnetコマンドを使用して、ASP.NET Coreのアプリケーションを作成する。

        ``` 
        ~$ dotnet new -t web
        ~$ ls
        Controllers			appsettings.json
        Program.cs			bower.json
        Startup.cs			bundleconfig.json
        TodoApp.csproj			runtimeconfig.template.json
        Views				web.config
        appsettings.Development.json	wwwroot
        ```

        dotnet new コマンドは「-t」スイッチにより、生成されるプロジェクトの種類が異なる。
        代表的な例を以下にあげておく。

        スイッチパラメータ|生成プロジェクト
         ------------- | ----------- 
         Console | コンソールアプリケーション 
         Web | ASP.NET Webアプリケーション 
         Lib | .NET Coreライブラリ 
         Xunittest | xUnitテストプロジェクト 

        上記以外のスイッチについてはヘルプを参照のこと（dotnet new --help）
        
3. まずは動かしてみる

    1. ライブラリのリストア
        作成直後の場合、アプリケーションを動かすのに必要なライブラリが不足している。
        そのため、ライブラリを復元する（これをリストアという）。

        リストアには以下のコマンドを使用する。

        ```
        ~$ dotnet restore
          Restoring packages for /Users/Foo/TodoApp/TodoApp.csproj...
          Generating MSBuild file /Users/Foo/TodoApp/obj/TodoApp.csproj.nuget.g.props.
          Generating MSBuild file /Users/Foo/TodoApp/obj/TodoApp.csproj.nuget.g.targets.
          Writing lock file to disk. Path: /Users/Foo/TodoApp/obj/project.assets.json
          Restore completed in 2.36 sec for /Users/Foo/TodoApp/TodoApp.csproj.
  
          NuGet Config files used:
              /Users/Foo/.nuget/NuGet/NuGet.Config
  
          Feeds used:
             https://api.nuget.org/v3/index.json
        ```

        .NET Coreは.NET Frameworkと同様に[nuget](https://www.nuget.org)によるライブラリの管理を行っている。

    2. アプリケーションの実行
    
        リストアが完了したところで、アプリケーションを実行する

        アプリケーションの実行は以下のコマンドで実行できる。

        ```
        ~$ dotnet run .
        Hosting environment: Production
        Content root path: /Users/kurihara/TodoApp
        Now listening on: http://localhost:5000
        Application started. Press Ctrl+C to shut down.
        ```

        ブラウザから[アプリケーション](http://localhost:5000)にアクセス
        以下の画面が表示されることを確認する。