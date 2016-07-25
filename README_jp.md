<a href="http://eure.jp"><img alt="eureka" src="https://cloud.githubusercontent.com/assets/3029684/13734246/52816c8c-e9df-11e5-9240-258ecb380968.png" height=60 /></a>
# eureka Swift Style Guide

[English](https://github.com/eure/swift-style-guide/blob/master/README.md) | [日本語](https://github.com/eure/swift-style-guide/blob/master/README_jp.md)

このスタイルガイドは、弊社のiOSチームが1年以上Swiftのコードを書いて、レビューをして、検証を重ねて培ってきたものです。弊社がリリースしているアプリに適用して、**優れている**と判断したコーディングルールを反映しました。

ここに記されたルールは次の目的を達成もしくはサポートしようとするものです。

- プログラマー自身のエラーを減らして、さらにエラーを見つけやすくする
- コードの可読性と明快さを向上させる（他の人がコードをレビューもしくは書き換えると仮定して）
- コードが不必要に肥大することを抑える
- チームメンバーの多数が支持するコーディングの美学を守る

このガイドラインの多くの項目は批判されたり、もしかしたらSwiftコミュニティの一般的なルールとは真逆のことかもしれません。しかし、弊社は**チーム開発**においてこれらのプラクティスを試して、検証してきました。そして、弊社では上手くいっています。

このガイドラインは未完成であり、変更される可能性があります。弊社のアプリが成長したり、チームで改善をしたり、Swift自体が進化を遂げたりすることに従って、このガイドラインも必要に応じて更新していきます。


# 目次
- [スタイルと慣習](#スタイルと慣習)
    - [フォーマット](#フォーマット)
        - [セミコロン (`;`)](#セミコロン)
        - [スペース](#スペース)
        - [コンマ (`,`)](#コンマ)
        - [コロン (`:`)](#コロン)
        - [括弧 (`{}`)](#括弧)
        - [プロパティ](#プロパティ)
        - [条件分岐](#条件分岐)
    - [命名](#命名)
        - [大文字、小文字](#大文字、小文字)
        - [名前の付け方](#名前の付け方)
    - [依存関係](#依存関係)
        - [Import文](#import文)
    - [宣言の順序](#宣言の順序)
- [ベストプラクティス](#ベストプラクティス)
    - [コメント](#コメント)
    - [ダイナミックと安全性](#ダイナミックと安全性)
    - [アクセス修飾子](#アクセス修飾子)
    - [型推論](#型推論)
    - [Collections / SequenceTypes](#collections--sequencetypes)
    - [循環参照を防ぐ](#循環参照を防ぐ)




# スタイルと慣習

## フォーマット

### セミコロン

#### 文末にセミコロン（`;`）は付けない。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
self.backgroundColor = UIColor.whiteColor()
self.completion = { 
    // ...
}
</pre></td>
<td><pre lang=swift>
self.backgroundColor = UIColor.whiteColor();
self.completion = { 
    // ...
};
</pre></td>
</tr>
</table>

***理由：*** 文末にセミコロンを付けることで実用的なメリットはありません。しかし、Objective-Cのコードをコピー&ペーストしたことが一目瞭然というメリットだけがあります。


### スペース

#### タブで半角スペース4つ分を使用する。
Xcodeの**Text Editing**で以下のように設定します。

<img width="749" alt="screen shot 2016-02-10 at 15 29 59" src="https://cloud.githubusercontent.com/assets/3029684/12940329/3566d882-d00b-11e5-9c2d-344f5c5f70e5.png" />

***理由：*** 異なるテキストエディタ間でインデントを揃えるためです。


#### ソースファイルの文末に空行を1行だけ入れる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Button {
  // ...
}
// <-- ここに1行を入れます
</pre></td>
<td><pre lang=swift>
class Button {
  // ...
} // <-- 空行がありません
</pre></td>
</tr>
<tr>
<td></td>
<td><pre lang=swift>
class Button {
  // ...
}
// <-- ここに1行を入れます
// <-- ここの1行は余分です
</pre></td>
</tr>
</table>

***理由：*** 文末に空行がないことで起きるエラーを防ぎ、コミットのdiffのノイズを減らします。


#### メソッドとメソッドの間に1行以上の空行を入れる。
<table>
<tr><th>OK</th></tr>
<tr>
<td><pre lang=swift>
class BaseViewController: UIViewController {
    // ...
    
    override viewDidLoad() {
        // ...
    }
    
    override viewWillAppear(animated: Bool) {
        // ...
    }
}
</pre></td>
</tr>
</table>

***理由：*** コードのブロックとブロックの間に十分な余白を持たせるためです。


#### オペレーターの定義とコール時にオペレーターの周りに半角スペースを1つ入れる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
func <| (lhs: Int, rhs: Int) -> Int {
    // ...
}

let value = 1 <| 2
</pre></td>
<td><pre lang=swift>
func <|(lhs: Int, rhs: Int) -> Int {
    // ...
}

let value = 1<|2
</pre></td>
</tr>
</table>

***理由：*** 可読性のためです。


#### メソッドのreturnの矢印（`->`）の周りに半角スペースを1つ入れる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
func doSomething(value: Int) -> Int {
    // ...
}
</pre></td>
<td><pre lang=swift>
func doSomething(value: Int)->Int {
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** 可読性のためです。


### コンマ

#### コンマ（`,`）の前にはスペースを入れず、後ろには半角スペースを1つ入れるか、新しい行にする。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
let array = [1, 2, 3]
</pre></td>
<td><pre lang=swift>
let array = [1,2,3]
let array = [1 ,2 ,3]
let array = [1 , 2 , 3]
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
self.presentViewController(
    controller,
    animated: true,
    completion: nil
)
</pre></td>
<td><pre lang=swift>
self.presentViewController(
    controller ,
    animated: true,completion: nil
)
</pre></td>
</tr>
</table>

***理由：*** コンマで分けたものが一目で分けられていると判別できるようにします。


### コロン

#### 型を示すコロン（`:`）は後ろに1つの半角スペースを入れて、前には半角スペースを入れない。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
func createItem(item: Item)
</pre></td>
<td><pre lang=swift>
func createItem(item:Item)
func createItem(item :Item)
func createItem(item : Item)
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
var item: Item? = nil
</pre></td>
<td><pre lang=swift>
var item:Item? = nil
var item :Item? = nil
var item : Item? = nil
</pre></td>
</tr>
</table>

***理由：*** コロンは左側のオブジェクトを説明するためであり、右側を説明するためではありません。


#### `case`文のコロン（`:`）は前に半角スペースを入れず、後ろには半角スペースを1つもしくは改行を入れる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
switch result {

case .Success:
    self.completion()
    
case .Failure:
    self.failure()
}
</pre></td>
<td><pre lang=swift>
switch result {

case .Success :
    self.completion()
    
case .Failure:self.reportError()
}
</pre></td>
</tr>
</table>

***理由：*** 前項の理由と同様で、コロンは左側のオブジェクトを説明するためであり、右側を説明するためではありません。


### 括弧

#### 始め波括弧（`{`）は前の文字との間に半角スペースを1つ入れる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Icon {
    // ...
}
</pre></td>
<td><pre lang=swift>
class Icon{
    // ...
}
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
let block = { () -> Void in
    // ...
}
</pre></td>
<td><pre lang=swift>
let block ={ () -> Void in
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** 宣言部分と実装部分を分けるためです。


#### 型の宣言、メソッド、クロージャの始め波括弧（`{`）の次に空行を1行入れる。1文だけのクロージャは1行で書くことができる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Icon {

    let image: UIImage
    var completion: (() -> Void)

    init(image: UIImage) {
    
        self.image = image
        self.completion = { [weak self] in self?.didComplete() }
    }
    
    func doSomething() {
    
        self.doSomethingElse()
    }
}
</pre></td>
<td><pre lang=swift>
class Icon {
    let image: UIImage

    init(image: UIImage) {
        self.image = image
        self.completion = { [weak self] in print("done"); self?.didComplete() }
    }
    
    func doSomething() { self.doSomethingElse() }
}
</pre></td>
</tr>
</table>

***理由：*** コードを読んでいる時に十分な余白を持たせるためです。


#### 実装部分のない宣言は空の波括弧（`{}`）で書く。もしくは、実装部分のない理由をコメントで説明する。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
extension Icon: Equatable {}
</pre></td>
<td><pre lang=swift>
extension Icon: Equatable {
}
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
var didTap: () -> Void = {}

override func drawRect(rect: CGRect) {}

@objc dynamic func controllerDidChangeContent(controller: NSFetchedResultsController) {

    // 何もしていない。このデリゲートメソッドはNSFetchedResultsControllerのトラッキングモードを有効にするため。
}
</pre></td>
<td><pre lang=swift>
var didTap: () -> Void = { }

override func drawRect(rect: CGRect) {
}

@objc dynamic func controllerDidChangeContent(controller: NSFetchedResultsController) {
    
}
</pre></td>
</tr>
</table>

***理由：*** 宣言部分を意図的に空にしているのであって、`TODO`の書き忘れでないことを明確にするためです。


#### 終わり波括弧（`}`）の前に空行を入れない。1行で波括弧が閉じている場合は、終わり波括弧（`}`）の前に半角スペースを1つ入れる。

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Button {

    var didTap: (sender: Button) -> Void = { _ in }

    func tap() {
    
        self.didTap()
    }
}
</pre></td>
<td><pre lang=swift>
class Button {

    var didTap: (sender: Button) -> Void = {_ in}

    func tap() {
    
        self.didTap()
        
    }
    
}
</pre></td>
</tr>
</table>

***理由：*** コードを短くしつつ、宣言と宣言の間に余白を入れるためです。


#### 終わり波括弧（`}`）が対の始め波括弧（`{`）と違う行にある場合、終わり波括弧（`}`）は宣言部分の左端に揃える。

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
lazy var largeImage: UIImage = { () -> UIImage in

    let image = // ...
    return image
}()
</pre></td>
<td><pre lang=swift>
lazy var largeImage: UIImage = { () -> UIImage in

    let image = // ...
    return image
    }()
</pre></td>
</tr>
</table>

***理由：*** 終わり波括弧が左端に揃っていることで、視覚的にスコープを把握しやすいからです。このルールは下のフォーマットガイドラインに基づいています。


### プロパティ

#### `get`と`set`とその終わり波括弧（`}`）は全て左端で揃える。1行で記述できる場合、`get`と`set`の宣言は1行で記述する。
[括弧のルール](#括弧)を適用しています。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
struct Rectangle {

    // ...
    var right: Float {
    
        get {
        
            return self.x + self.width
        }
        set {
        
            self.x = newValue - self.width
        }
    }
}
</pre></td>
<td><pre lang=swift>
struct Rectangle {

    // ...
    var right: Float {
    
        get
        {
            return self.x + self.width
        }
        set
        {
            self.x = newValue - self.width
        }
    }
}
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
struct Rectangle {

    // ...
    var right: Float {
    
        get { return self.x + self.width }
        set { self.x = newValue - self.width }
    }
}
</pre></td>
<td><pre lang=swift>
struct Rectangle {

    // ...
    var right: Float {
    
        get { return self.x + self.width }
        set { self.x = newValue - self.width
            print(self) 
        }
    }
}
</pre></td>
</tr>
</table> 

***理由：*** [括弧のルール](#括弧)と合わせて、このフォーマットは一貫性と可読性を向上させます。


#### 読み取り専用のComputed propertyは`get`を省略する。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
struct Rectangle {

    // ...
    var right: Float {
    
        return self.x + self.width
    }
}
</pre></td>
<td><pre lang=swift>
struct Rectangle {

    // ...
    var right: Float {
    
        get {
        
            return self.x + self.width
        }
    }
}
</pre></td>
</tr>
</table>

***理由：*** `return`が読み取り専用であることを十分明確にしており、より簡潔な記述を可能にしています。


### 条件分岐

#### `if`、`else`、`switch`、`do`、`catch`、`repeat`、`guard`、`for`、`while`、`defer`文は対になっている終わり波括弧（`}`）と左端に揃える。
[括弧のルール](#括弧)を適用しています。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
if array.isEmpty {
    // ...
}
else {
    // ...
}
</pre></td>
<td><pre lang=swift>
if array.isEmpty {
    // ...
} else {
    // ...
}
</pre></td>
</tr>
<tr>
<td></td>
<td><pre lang=swift>
if array.isEmpty
{
    // ...
}
else
{
    // ...
}
</pre></td>
</tr>
</table> 

***理由：*** [括弧のルール](#括弧)と合わせて、このフォーマットは一貫性と可読性を向上させます。条件分岐文と終わり波括弧が視覚的にスコープを分かりやすくしています。

#### `case`文は`switch`文と左端で揃える。1行の`case` 文を書くことも可能である。複数行の`case`文は`case:`の後でインデントを1つ下げ、空行1行で分ける。
[括弧のルール](#括弧)を適用しています。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
switch result {

case .Success:
    self.doSomething()
    self.doSomethingElse()
    
case .Failure:
    self.doSomething()
    self.doSomethingElse()
}
</pre></td>
<td><pre lang=swift>
switch result {

case .Success: self.doSomething()
               self.doSomethingElse()
case .Failure: self.doSomething()
               self.doSomethingElse()
}
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
switch result {

case .Success: self.doSomething()
case .Failure: self.doSomethingElse()
}
</pre></td>
<td><pre lang=swift>
switch result {

	case .Success: self.doSomething()
	case .Failure: self.doSomethingElse()
}
</pre></td>
</tr>
</table> 

***理由：*** Xcodeのオートインデントで適用されるインデントです。また、複数行の場合、`case`文を空行で分けることは視認性を向上させます。

#### `if`、`switch`、`for`、`while`文の条件式は丸括弧（`()`）で囲まない。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
if array.isEmpty {
    // ...
}
</pre></td>
<td><pre lang=swift>
if (array.isEmpty) {
    // ...
}
</pre></td>
</tr>
</table> 

***理由：*** Objective-Cではないからです。


#### 出来る限りネストを避け、早い段階で`return`する。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
guard let strongSelf = self else {

    return
}
// strongSelfを使用したコードをここに書きます
</pre></td>
<td><pre lang=swift>
if let strongSelf = self {

    // strongSelfを使用したコードをここに書きます
}
</pre></td>
</tr>
</table> 

***理由：*** 追うべきネストが多くなればなるほど、コードを追いかけることが困難になります。



## 命名

命名規則はそのほとんどがAppleの命名規則に基づいています。

### 大文字、小文字

#### `class`、`struct`、`enum`、`protocol`の型の名前は*UpperCamelCase*にする。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class ImageButton {

    enum ButtonState {
    	// ...
    }
}
</pre></td>
<td><pre lang=swift>
class image_button {

    enum buttonState {
    	// ...
    }
}
</pre></td>
</tr>
</table>

***理由：*** 統一性を持たせるためにAppleの命名規則を採用しています。


#### `enum`と`OptionSetType`の値を*UpperCamelCase*にする。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
enum ErrorCode {
    
	case Unknown
  	case NetworkNotFound
  	case InvalidParameters
}

struct CacheOptions : OptionSetType {

    static let None = CacheOptions(rawValue: 0)
    static let MemoryOnly = CacheOptions(rawValue: 1)
    static let DiskOnly = CacheOptions(rawValue: 2)
    static let All: CacheOptions = [.MemoryOnly, .DiskOnly]
    // ...
}
</pre></td>
<td><pre lang=swift>
enum ErrorCode {
    
	case unknown
  	case network_not_found
  	case invalidParameters
}

struct CacheOptions : OptionSetType {

    static let none = CacheOptions(rawValue: 0)
    static let memory_only = CacheOptions(rawValue: 1)
    static let diskOnly = CacheOptions(rawValue: 2)
    static let all: CacheOptions = [.memory_only, .diskOnly]
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** 統一性を持たせるためにAppleの命名規則を採用しています。


#### 変数名と関数名は*lowerCamelCase*にする（静的なものや定数も含める）。頭文字語は例外として*UPPERCASE*とする。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
var webView: UIWebView?
var URLString: String?

func didTapReloadButton() {
    // ..
}
</pre></td>
<td><pre lang=swift>
var web_view: UIWebView?
var urlString: String?

func DidTapReloadButton() {
    // ..
}
</pre></td>
</tr>
</table>

***理由：*** 統一性を持たせるためにAppleの命名規則を採用しています。頭文字語に関しては、Upper caseの読みやすさを重視するからです。


### 名前の付け方

#### 1文字の名前を型、変数、関数に付けない。イテレータのインデックスの場所のみ1文字の変数を使用する。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
for (i, value) in array.enumerate() {
    // ... "i" is well known
}
</pre></td>
<td><pre lang=swift>
for (i, v) in array.enumerate() {
    // ... what's "v"?
}
</pre></td>
</tr>
</table>

***理由：*** 1文字の名前より良い名前は必ずあります。`i`に関しては、`index`を使用するよりも可読性が高いです。


#### 出来る限り省略された名前を付けない（ただし、[こちら](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/APIAbbreviations.html#//apple_ref/doc/uid/20001285-BCIHCGAE)は使用して良い（例えば、`min`/`max`））。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
let errorCode = error.code
</pre></td>
<td><pre lang=swift>
let err = error.code
</pre></td>
</tr>
</table>

***理由：*** 僅かに短くなることより、明快さの方が重要です。


#### 名前はそれが何であるかと*何のためであるか*を出来る限り表すものを付ける。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Article {

    var title: String
}
</pre></td>
<td><pre lang=swift>
class Article {

    var text: String
    // これは記事のタイトルかコンテンツか分からない
}
</pre></td>
</tr>
<tr><th>Better</th></tr>
<tr>
<td><pre lang=swift>
class NewsArticle {

    var headlineTitle: String
}
</pre></td>
<td></td>
</tr>
</table>

***理由：*** 僅かに短くなることより、明快さの方が重要です。また、その特徴を表す名前を付けることで、他の名前と衝突することを避けることができます。


#### URLに限っては、文字列と`NSURL`を区別するために名前の末尾に`~String`を付ける。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
var requestURL: NSURL
var sourceURLString: String

func loadURL(URL: NSURL) {
    // ...
}

func loadURLString(URLString: String) {
    // ...
}
</pre></td>
<td><pre lang=swift>
var requestURL: NSURL
var sourceURL: String

func loadURL(URL: NSURL) {
    // ...
}

func loadURL(URL: String) {
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** 正しい型を知るために宣言部分をチェックする時間を節約できます。


#### `class`、`struct`、`enum`、`protocol`などを名前に含めない。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class User {
    // ...
}

enum Result {
    // ...
}

protocol Queryable {
    // ...
}
</pre></td>
<td><pre lang=swift>
class UserClass {
    // ...
}

enum ResultEnum {
    // ...
}

protocol QueryableProtocol {
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** 余分な接尾辞は無駄です。ただし、Objective-Cのクラスと同一名のプロトコルは`~Protocol`の接尾辞を付けてSwiftにブリッジングされることに注意してください（例えば、`NSObject`と`NSObjectProtocol`）。このことはSwiftのコンパイラが自動生成したものであり、このガイドラインとは関係ありません。


## 依存関係

### Import文

#### `import`文はOS固有のフレームワークと外部フレームワークとの間に空行を1行入れて、アルファベット順に並べる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
import Foundation
import UIKit

import Alamofire
import Cartography
import SwiftyJSON
</pre></td>
<td><pre lang=swift>
import Foundation
import Alamofire
import SwiftyJSON
import UIKit
import Cartography
</pre></td>
</tr>
</table>

***理由：*** ブランチ間で依存関係の記述が変更された時、マージコンフリクトを減らします。


## 宣言の順序

#### `class`、`struct`、`enum`、`extension`、`protocol`などの全ての宣言は
`// MARK: - <宣言の名前>`を付ける。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
// MARK: - Icon

class Icon {


    // MARK: - CornerType

    enum CornerType {
    
        case Square
        case Rounded
    }
    // ...
}
</pre></td>
<td><pre lang=swift>
// Icon

class Icon {


    // MARK: CornerType

    enum CornerType {
    
        case Square
        case Rounded
    }
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** Xcodeの*Source Navigator*を使用して、特定の型にジャンプすることが容易になります。


#### 全てのプロパティとメソッドはスーパークラスやプロトコル毎にグループ分けをして、`// MARK: <スーパークラス/プロトコルの名前>`を付ける。その他はアクセスレベルに応じて、`// MARK: Public`、`// MARK: Internal`、`// MARK: Private`をそれぞれ付ける。
<table>
<tr><th>OK</th></tr>
<tr>
<td><pre lang=swift>
// MARK: - BaseViewController

class BaseViewController: UIViewController, UIScrollViewDelegate {


    // MARK: Internal
    
    weak var scrollView: UIScrollView?
    
    
    // MARK: UIViewController
    
    override func viewDidLoad() {
        // ...
    }
    
    override func viewWillAppear(animated: Bool) {
        // ...
    }
    
    
    // MARK: UIScrollViewDelegate
    
    @objc dynamic func scrollViewDidScroll(scrollView: UIScrollView) {
        // ...
    }
    
    
    // MARK: Private
    
    private var lastOffset = CGPoint.zero
}
</pre></td>
</tr>
</table>

***理由：*** ソースコード上のどこにプロパティやメソッドが宣言されているかを容易に特定できます。


#### `// MARK:`タグは上に2行、下に1行の空行を入れる。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
import UIKit


// MARK: - BaseViewController

class BaseViewController: UIViewController {


    // MARK: Internal
    
    weak var scrollView: UIScrollView?
    
    
    // MARK: UIViewController
    
    override func viewDidLoad() {
        // ...
    }
    
    override func viewWillAppear(animated: Bool) {
        // ...
    }
    
    
    // MARK: Private
    
    private var lastOffset = CGPoint.zero
}
</pre></td>
<td><pre lang=swift>
import UIKit
// MARK: - BaseViewController
class BaseViewController: UIViewController {

    // MARK: Internal
    weak var scrollView: UIScrollView?
    
    // MARK: UIViewController
    override func viewDidLoad() {
        // ...
    }
    
    override func viewWillAppear(animated: Bool) {
        // ...
    }
    
    // MARK: Private
    private var lastOffset = CGPoint.zero
}
</pre></td>
</tr>
</table>

***理由：*** コーディングの美学に尽きます。また、型の定義やメソッドのグループの間に十分な余白を与えます。


#### `// MARK:`タグによるグルーピングは次の順番にする:
- `// MARK: Public`
- `// MARK: Internal`
- Classの継承 (最上位の親から子へ)
    - `// MARK: NSObject`
    - `// MARK: UIResponder`
    - `// MARK: UIViewController`
- Protocolの継承 (最上位の親から子へ)
    - `// MARK: UITableViewDataSource`
    - `// MARK: UIScrollViewDelegate `
    - `// MARK: UITableViewDelegate`
- `// MARK: Private`

***理由：*** ソースコード上のどこにプロパティやメソッドが宣言されているかを容易に特定できます。`public`と`internal`の宣言はAPI利用者に最も参照される部分であるため、一番上に配置しています。


#### 上記のグルーピングの内部では以下の順序にする:
- `@`が付くプロパティ(`@NSManaged`, `@IBOutlet`, `@IBInspectable`, `@objc`, `@nonobjc`など)
- `lazy var`
- Computed property(`var`)
- Stored property(`var`)
- `let`プロパティ
- `@`が付く関数(`@NSManaged`, `@IBAction`, `@objc`, `@nonobjc`など)
- その他の関数

***理由：*** `@`が付くプロパティと関数は最も参照されやすいため（KVCのキーや`Selector`の文字列をチェックしたり、Interface Builderと相互に参照し合うなど）、上部に定義しています。



# ベストプラクティス

基本的に、**全てのXcodeのWarningsは無視すべきではありません。**例えば、出来る限り`var`よりも`let`を使用する、使用していない変数は`_`を使用するなどです。


## コメント

#### コメントは「なぜ？」という問いに答えるものであり、それ以外のことはコード自体が説明すべきである。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
let leftMargin: CGFloat = 20
view.frame.x = leftMargin
</pre></td>
<td><pre lang=swift>
view.frame.x = 20 // left margin
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
@objc dynamic func tableView(tableView: UITableView,
 heightForHeaderInSection section: Int) -> CGFloat {

    return 0.01 // tableViewは0を無視してしまうため
}
</pre></td>
<td><pre lang=swift>
@objc dynamic func tableView(tableView: UITableView,
 heightForHeaderInSection section: Int) -> CGFloat {

    return 0.01 // 小さい数字を返す
}
</pre></td>
</tr>
</table>

***理由：*** 最も良いコメントは書いた人自身は必要のないものです。もしコメントを書く必要があるならば、そのコードを書いた理由を説明するべきであり、単に明らかなことを説明するべきではありません。


#### 一時的にローカライズされていない文字列は`// TODO: localize`を付ける。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
self.titleLabel.text = "Date Today:" // TODO: localize
</pre></td>
<td><pre lang=swift>
self.titleLabel.text = "Date Today:"
</pre></td>
</tr>
</table>

***理由：*** 実装した機能をデバッグしてテストをする場合、大抵はネイティブの言語を使用します。そして、翻訳された文字列は分けてテストされます。このガイドラインにより、全ての未翻訳の文字列が説明され、後で見つけることが容易になります。


## ダイナミックと安全性

#### Objective-Cの`protocol`の実装部分（プロパティとメソッドの両方とも）は`@objc dynamic`を最初に付ける。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
@objc dynamic func scrollViewDidScroll(scrollView: UIScrollView) {
    // ...
}
</pre></td>
<td><pre lang=swift>
func scrollViewDidScroll(scrollView: UIScrollView) {
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** コンパイラの最適化による解決困難なバグを防ぎます。


#### `IBAction`と`IBOutlet`は`dynamic`を付ける。
<table>
<tr><th>OK</th></tr>
<tr>
<td><pre lang=swift>
@IBOutlet private dynamic weak var closeButton: UIButton?

@IBAction private dynamic func closeButtonTouchUpInside(sender: UIButton) {
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** Swiftコンパイラはたまに`dynamic`として扱ってくれません。`dynamic`を書くことで、`private`で宣言していたとしても安全性を保証します。


#### KVCやKVOに使用するプロパティと`Selector`として使用するメソッドは`dynamic`を付ける。
<table>
<tr><th>OK</th></tr>
<tr>
<td><pre lang=swift>
override func viewDidLoad() {

    super.viewDidLoad()
    let gesture = UITapGestureRecognizer(target: self, action: "tapGestureRecognized:")
    self.view.addGestureRecognizer(gesture)
}
    
private dynamic func tapGestureRecognized(sender: UITapGestureRecognizer) {
    // ...
}
</pre></td>
</tr>
</table>

***理由：*** 1つ前のルールと同じ理由です。Swiftコンパイラはたまに`dynamic`として扱ってくれません。`dynamic`を書くことで、`private`で宣言していたとしても安全性を保証します。


#### `@IBOutlet`は`weak`で宣言して、型は`ImplicitlyUnwrappedOptional(!)`ではなく`Optional(?)`とする。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
@IBOutlet dynamic weak var profileIcon: UIImageView?
</pre></td>
<td><pre lang=swift>
@IBOutlet var profileIcon: UIImageView!
</pre></td>
</tr>
</table>

***理由：*** サブクラスがその`@IBOutlet`のビューを生成しなかったとしても安全性を保証します。また、`viewDidLoad(_:)`の前にプロパティにアクセスすることでクラッシュすることを防ぎます。


## アクセス修飾子

#### `private`として宣言することをデフォルトとして、必要なときだけ`internal`または`public`として外部に公開する。

***理由：*** Xcodeの補完を必要のないプロパティやメソッドで汚してしまうことを防ぐことができます。また、理論的には、コンパイラが最適化をさらにして、ビルドが速くなるでしょう。


#### ライブラリのモジュール：全ての宣言は明示的に`public`、`internal`、`private`のいずれかを付ける。

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
private let defaultTimeout: NSTimeInterval = 30

internal class NetworkRequest {
    // ...
}
</pre></td>
<td><pre lang=swift>
let defaultTimeout: NSTimeInterval = 30

class NetworkRequest {
    // ...
}
</pre></td>
</tab

***理由：*** APIの使用者にとって意図したことを明確にすることができます。


#### アプリケーションのモジュール：`public`はプロトコルで必要な場合を除いて使用しない。`internal`は書いても書かなくても良い。`private`は必ず書く。

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
private let someGlobal = "someValue"

class AppDelegate {
    // ...
    private var isForeground = false
}
</pre></td>
<td><pre lang=swift>
public let someGlobal = "someValue"

public class AppDelegate {
    // ...
    var isForeground = false
}
</pre></td>
</table>

***理由：*** Appバンドルで`public`は役に立ちません。すなわち、アクセス修飾子は`internal`か`private`のいずれかと推測できます。この場合、`private`を明示するだけで十分です。


#### アクセス修飾子は`@`以外の修飾子の前に付ける。

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
@objc internal class User: NSManagedObject {
    // ...
    @NSManaged internal dynamic var identifier: Int
    // ...
    @NSManaged private dynamic var internalCache: NSData?
}
</pre></td>
<td><pre lang=swift>
internal @objc class User: NSManagedObject {
    // ...
    @NSManaged dynamic internal var identifier: Int
    // ...
    private @NSManaged dynamic var internalCache: NSData?
}
</pre></td>
</table>

***理由：*** [宣言の順序のルール](#宣言の順序)と合わせて、縦方向にコードを流し読みしている時に、可読性が増します。


## 型推論

#### 必要な場合を除いて、変数やプロパティの型は宣言文の左側か右側のいずれか片側から推測できるようにする。

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
var backgroundColor = UIColor.whiteColor()
var iconView = UIImageView(image)
</pre></td>
<td><pre lang=swift>
var backgroundColor: UIColor = UIColor.whiteColor()
var iconView: UIImageView = UIImageView(image)
</pre></td>
</tr>
<tr>
<td><pre lang=swift>
var lineBreakMode = NSLineBreakMode.ByWordWrapping
// or
var lineBreakMode: NSLineBreakMode = .ByWordWrapping
</pre></td>
<td><pre lang=swift>
var lineBreakMode: NSLineBreakMode = NSLineBreakMode.ByWordWrapping
</pre></td>
</tr>
</table>

***理由：*** 冗長になることを防ぐためです。また、ジェネリクスの型にバインドされるときの曖昧さを減らします。


#### リテラルの型（`StringLiteralConvertible`、`NilLiteralConvertible`など）が関係するときは、`as`で直接キャストするよりも明示的に型を宣言する。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
var radius: CGFloat = 0
var length = CGFloat(0)
</pre></td>
<td><pre lang=swift>
var radius: CGFloat = CGFloat(0)
var length = 0 as CGFloat // キャストするよりもイニシャライザの方が良い
</pre></td>
</tr>
</table>

***理由：*** 冗長になることを防ぐためです。また、ジェネリクスの型にバインドされるときの曖昧さを減らします。


## Collections / SequenceTypes

#### `.count`はその値自体が必要な場合のみ使用する。
<table>
<tr><th>OK</th></tr>
<tr>
<td><pre lang=swift>
let badgeNumber = unreadItems.count
</pre></td>
</tr>
</table>

空かどうかをチェックするとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
if sequence.isEmpty {
// ...
</pre></td>
<td><pre lang=swift>
if sequence.count <= 0 {
// ...
</pre></td>
</tr>
</table>

最初か最後の要素を取得するとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
let first = sequence.first
let last = sequence.last
</pre></td>
<td><pre lang=swift>
let first = sequence[0]
let last = sequence[sequence.count - 1]
</pre></td>
</tr>
</table>

最初か最後の要素を削除するとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
sequence.removeFirst()
sequence.removeLast()
</pre></td>
<td><pre lang=swift>
sequence.removeAtIndex(0)
sequence.removeAtIndex(sequence.count - 1)
</pre></td>
</tr>
</table>

全てのインデックスでイテレートするとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
for i in sequence.indices {
    // ...
}
</pre></td>
<td><pre lang=swift>
for i in 0 ..< sequence.count {
    // ...
}
</pre></td>
</tr>
</table>

最初か最後のインデックスを取得するとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
let first = sequence.indices.first
let last = sequence.indices.last
</pre></td>
<td><pre lang=swift>
let first = 0
let last = sequence.count - 1
</pre></td>
</tr>
</table>

最後の`n`個以外全てのインデックスでイテレートするとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
for i in sequence.indices.dropLast(n) {
    // ...
}
</pre></td>
<td><pre lang=swift>
for i in 0 ..< (sequence.count - n) {
    // ...
}
</pre></td>
</tr>
</table>

最初の`n`個以外全てのインデックスでイテレートするとき:
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
for i in sequence.indices.dropFirst(n) {
    // ...
}
</pre></td>
<td><pre lang=swift>
for i in n ..< sequence.count {
    // ...
}
</pre></td>
</tr>
</table>

***基本的に、`count`の値に足したり、引いたりして使用したい場合は、Swiftらしい書き方でもっと良い書き方があるでしょう。***

***理由：*** 意図していることが明確になり、ミスを減らすことができます。特に[Off-by-oneエラー](https://ja.wikipedia.org/wiki/Off-by-oneエラー)を減らすことができます。


## 循環参照を防ぐ

特に、このルールはこれまでずっと議論されてきた`self`を使用するか否かをカバーする内容です。

#### インスタンスのプロパティとメソッドはクロージャ内を含めて、必ず`self`を付ける。

(この意図は次のルールで説明します)

<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
self.animatableViews.forEach { view in
            
    self.animateView(view)
}
</pre></td>
<td><pre lang=swift>
animatableViews.forEach { view in
            
    animateView(view)
}
</pre></td>
</tr>
</table>

***理由：*** `self`を付けるか付けないかを判断するよりも、必ず`self`を付けるようにすることで、ミスを少なくすることができることが分かりました。すなわち、このルールは循環参照に関するルールが必要であることを意味しています。詳細は下のルールをご覧ください。


#### `@noescape`・関数・スタティックメソッドのクロージャ以外のクロージャ内で`self`にアクセスする場合、必ず`[weak self]`を使用する。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
self.request.downloadImage(
    url,
    completion: { [weak self] image in

        self?.didDownloadImage(image)
    }
)
</pre></td>
<td><pre lang=swift>
self.request.downloadImage(
    url,
    completion: { image in

        self.didDownloadImage(image) // 循環参照
    }
)
</pre></td>
</tr>
</table>

***理由：*** 上記の`self`が必須となるルールと合わせて、循環参照が起きうる箇所を簡単に特定できるようになります。`self`にアクセスしているクロージャを探し、`[weak self]`が抜けていないかを確認するだけです。


#### クロージャ内で参照をキャプチャするのに`unowned`を使用しない。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
self.request.downloadImage(
    url,
    completion: { [weak self] image in

        self?.didDownloadImage(image)
    }
)
</pre></td>
<td><pre lang=swift>
self.request.downloadImage(
    url,
    completion: { [unowned self] image in

        self.didDownloadImage(image)
    }
)
</pre></td>
</tr>
</table>

***理由：*** `weak`よりも`unowned`の方が便利ですが（`Optional`として扱う必要がないため）、クラッシュを起こしやすくなります。誰もゾンビオブジェクトは好ましくないでしょう。


#### クロージャ内でweakな`self`をアンラップする必要がある場合、`` `self` ``に対してバインドする。
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
self.request.downloadImage(
    url,
    completion: { [weak self] image in

        guard let `self` = self else { 
        
            return
        }
        self.didDownloadImage(image)
        self.reloadData()
        self.doSomethingElse()
    }
)
</pre></td>
<td><pre lang=swift>
self.request.downloadImage(
    url,
    completion: { [weak self] image in

        guard let strongSelf = self else { 
        
            return
        }
        strongSelf.didDownloadImage(image)
        strongSelf.reloadData()
        strongSelf.doSomethingElse()
    }
)
</pre></td>
</tr>
</table>

***理由：*** シンタックスハイライトを有効にするためです。

---

[トップへ戻る](#目次)
