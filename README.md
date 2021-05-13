<h1> MS Tech Camp #7 </br>
Custom Vision Serviceで画像分類AIを作ろう！</h1>

[MS Tech Camp #7](https://mspjp.connpass.com/event/) で使用するハンズオン資料です。

Custom Vision Service で画像分類モデルを構築し、 APIを用いて送信した画像の分類結果を受け取ります。

## 1. Custom Vision Service プロジェクトを作成する

1-1 ブラウザで [Custom Vision Service ポータル](https://www.customvision.ai/) を開きます。 その後、[サインイン] を選択します。

1-2 サインインを求められたら、Microsoft アカウントの資格証明を使用してサインインします。 このアプリにユーザー情報へのアクセスを許可するように求められたら、[はい] をクリックし、プロンプトが表示されたらサービス使用条件に同意します。

1-3 [新しいプロジェクト] をクリックして、新しいプロジェクトを作成します。

![](images/1-portal-click-new-project.png)

1-4 [新しいプロジェクトの作成] ダイアログで、プロジェクトに "Artworks" という名前を付けます。

1-5 このプロジェクトに使用する リソース グループ を選択します。 リソース グループをまだ用意していない場合は、[新規作成] を選択して新しいリソース グループを作成します。

1-6 必要事項を記入します。以下の表を参照してください。

|項目|記入・設定例|
|--|--|
|Project Types|Classification|
|Classification Types|Multilabel|
|Domain|General|

![](images/1-portal-create-project.png)

## 2. タグを付けた画像をアップロードする

今回のハンズオンでは、ピカソ、ポロック、レンブラントの有名な絵画の画像を Artworks プロジェクトに追加します。 Custom Vision Service がある画家を別の画家から区別することを学習できるように、画像にタグを付けます。

2-1 作成した Artworks プロジェクトで、サイド パネルの [タグ] の右側にあるプラス記号 [+] を選択します。

![](images/2-add-tags.png)

2-2 [Create a new tag](新しいタグの作成) というダイアログ ボックスが表示されます。 タグ名フィールドに「絵画」と入力して、[保存] を選択します。 この操作により、タグ リストに "絵画" タグが作成されます。 さらに追加しましょう。

2-3 手順 1 と 2 を繰り返し、値が ピカソ、ポロック、レンブラント のタグを追加します。 完了すると、タグ リストは次のようになります。

![](images/2-tag-list.png)

プロジェクト内の画像のうちこれらの各タグでタグ付けされたものの数はまだ 0 になっています。 プロジェクトに画像をいくつか追加してタグを割り当てましょう。

2-4 ハンズオンの画像リソースが格納されている [cvs resources.zip](https://github.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/raw/master/cvs-resources.zip) をダウンロードし、ローカル コンピューターに解凍します。

2-5 ポータルに戻り、[Add images](画像の追加) を選択して、プロジェクトに画像を追加します。

![](images/)

2-6 手順 4 でローカルにダウンロードした cvs-resources フォルダーで、"Artists\Picasso" フォルダーに移動します。

2-7 "Artists\Picasso" 内のすべてのファイルを選択し、[開く] を選択します。

![](images/2-fe-browse-picasso-01.png)

2-8 [Image upload](画像のアップロード) ダイアログが開き、アップロードしたすべての画像のサムネイルが表示されます。 [My Tags](マイ タグ) フィールドを選択すると、これらの画像を割り当てることができるタグのドロップダウンが開きます。

![](images/2-upload-picasso-tags.png)

2-9 "絵画" タグと "ピカソ" タグを選択し、[Upload 7 files](7 個のファイルをアップロード) を選択してアップロードを終了します。

2-10 アップロードした画像が Artworks プロジェクトに含まれること、およびタグ リストが更新されて "ピカソ" と "絵画" タグが 7 個の画像に付けられたことが示されていることを確認します。

![](images/2-portal-tagged-01.png)

2-11 [Add images](画像の追加) を選択して、モジュール リソースの "Artists\Rembrandt" フォルダーにあるすべての画像を選択します。 それらに "絵画" と "レンブラント" というタグを付け、[Upload 6 files](6 個のファイルをアップロード) を選択してプロジェクトにアップロードします。

![](images/2-upload-rembrandt.png)

2-12 プロジェクトにピカソの画像と共にレンブラントの画像が表示され、タグの一覧に "レンブラント" と表示されることを確認します。

![](images/2-portal-tagged-02.png)

2-13 同じような方法で、ジャクソン ポロックの絵画を追加し、Custom Vision Service でポロックの絵画も認識できるようにします。 モジュール リソースの "Artists\Pollock" フォルダーですべての画像を選択し、"絵画" と "ポロック" というタグを付けて、プロジェクトにアップロードします。
