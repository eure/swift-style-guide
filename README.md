# Eureka Swift Style Guide

This style guide is a product of our iOS team's more than a year writing, reviewing, and testing Swift code. It reflects the coding rules we have observed as "efficient" in our production apps.

The guidelines here try to accomplish/encourage practices that accomplish the following goals:

- to make it hard to write programmer errors, or at least make them hard to miss
- to increase readability and clarity of intent, *with assumption that the code will be reviewed/consumed by a different person*
- to minimize unnecessary code bloat
- to observe aesthetics that the majority of the team voted for


We understand that a quite a few of the guidelines below are controversial and may even be opposite what the Swift community generally observes, but we have tried and tested these practices in a **team** environment and they work for us.

That said, this is a live document. As our app grows, our team improves, and Swift evolves, our practices will adapt as well and this list will be updated if needed.


## Table of Contents
- [Formatting](#formatting)
    - [Semicolons (`;`)](#semicolons)
    - [Whitespaces](#whitespaces)
    - [Commas (`,`)](#commas)
    - [Colons (`:`)](#colons)
    - [Braces (`{}`)](#braces)
    - [Properties](#properties)
    - [Control Flow Statements](#control-flow-statements)
- [Naming](#naming)
    - [Capitalization](#capitalization)
    - [Semantics](#semantics)
- [Dependencies](#dependencies)
    - [Import Statements](#import-statements)
- [Declaration Order](#declaration-order)
- [Protection from Dynamism](#protection-from-dynamism)
- [Access Modifiers](#access-modifiers)
- [Type Inference](#type-inference)
- [Collections / SequenceTypes](#collections--sequencetypes)
- [Rules on `self`](#rules-on-self)




## Formatting

### Semicolons

#### Trailing semicolons (`;`) are not allowed.
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

***Rationale:*** There is no practical advantage of using trailing semicolons. It is, however, a very good way to catch someone copy-pasting Objective-C code ;)


### Whitespaces

#### Use 4 spaces for tabs.
Set XCode's **Text Editing** settings as shown:
 
<img width="749" alt="screen shot 2016-02-10 at 15 29 59" src="https://cloud.githubusercontent.com/assets/3029684/12940329/3566d882-d00b-11e5-9c2d-344f5c5f70e5.png" />

***Rationale:*** Maintains visually similar indentation across different text editors.


#### All source files should end with a single trailing newline (only).
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Button {
  // ...
}
// <-- One line here
</pre></td>
<td><pre lang=swift>
class Button {
  // ...
} // <-- No new line after
</pre></td>
</tr>
<tr>
<td></td>
<td><pre lang=swift>
class Button {
  // ...
}
// <-- One line here
// <-- Another line here
</pre></td>
</tr>
</table>

***Rationale:*** Prevents no-trailing-newline errors and reduces noise in commit diffs.


#### All functions should be at least one empty line apart each other.
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

***Rationale:*** Gives breathing room between code blocks.


#### Use single spaces around operator definitions and operator calls.
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

***Rationale:*** Readability.


#### Use single spaces around return arrows (`->`) both in functions and in closures.
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

***Rationale:*** Readability.


### Commas

#### Commas (`,`) should have no whitespace before it, and should have either one space or one newline after.
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

***Rationale:*** Keeps comma-separated items visually separate.


### Colons

#### Colons (`:`) used to indicate type should have one space after it and should have no whitespace before it.
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

***Rationale:*** The colon describes the object to its left, not the right. (Just how we write colons in english)


#### Colons (`:`) for `case` statements should have no whitespace before it, and should have either one space or one newline after it.
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

***Rationale:*** Same as he previous rule, the colon describes the object to its left, not the right.


#### Open braces (`{`) should be one space following the previous non-whitespace character.
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

***Rationale:*** Separates the brace from the declaration.


#### Open braces (`{`) for type declarations, functions, and closures should be followed by one empty line.
<table>
<tr><th>OK</th><th>NG</th></tr>
<tr>
<td><pre lang=swift>
class Icon {

    let image: UIImage

    init(image: UIImage) {
    
        self.image = image
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
    }
    
    func doSomething() { self.doSomethingElse() }
}
</pre></td>
</tr>
</table>

***Rationale:*** Gives breathing room when scanning for code.


#### Empty declarations should be written in empty braces (`{}`), otherwise a comment should indicate the reason for the empty implementation.
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

    // do nothing; delegate method required to enable tracking mode
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

***Rationale:*** Makes it clear that the declaration was meant to be empty and not just a missing `TODO`. <br/>


#### Close braces (`}`) should not have empty lines before it. For single line expressions enclosed in braces, there should be one space between the last statement and the closing brace.
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

***Rationale:*** Provides breathing room between declarations while keeping code compact.


#### Close braces (`}`) unless on the same line as its corresponding open brace (`{`), should be left-aligned with the statement that declared the open brace.
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

***Rationale:*** Close braces left-aligned with their opening statements visually express their scopes pretty well. This rule is the basis for the succeeding formatting guidelines below.


### Properties

#### The `get` and `set` statement and their close braces (`}`) should all be left-aligned. If the statement in the braces can be expressed in a single line, the `get` and `set` declaration can be inlined.
The [rules on braces](#braces) apply.
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

***Rationale:*** Combined with the [rules on braces](#braces), this formatting provides very good consistency and scannability.


#### Read-only computed properties should ommit the `get` clause.
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

***Rationale:*** The `return` statement provides enough clarity that lets us use the more compact form.


### Control Flow Statements

#### `if`, `else`, `switch`, `do`, `catch`, `repeat`, `guard`, `for`, `while`, and `defer` statements should be left-aligned with their respective close braces (`}`).
The [rules on braces](#braces) apply.
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

***Rationale:*** Combined with the [rules on braces](#braces), this formatting provides very good consistency and scannability. Close braces left-aligned with their respective control flow statements visually express their scopes pretty well.


#### `case` statements should be left-aligned with the `switch` statement. Single-line `case` statements can be inlined and written compact. Multi-line `case` statements should be indented below `case:` and separated with one empty line.
The [rules on braces](#braces) apply.
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



## Naming

Naming rules are mostly based on Apple's naming conventions, since we'll end up consuming their API anyway.

### Capitalization

#### Type names (`class`, `struct`, `enum`, `protocol`) should be in *UpperCamelCase*. 
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

***Rationale:*** Adopt Apple's naming rules for uniformity.


#### `enum` values and `OptionSetType` values should be in *UpperCamelCase*. 
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

***Rationale:*** Adopt Apple's naming rules for uniformity.


#### Variables and functions should be in *lowerCamelCase*, including statics and constants. An exception is acronyms, which should be *UPPERCASE*.
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

***Rationale:*** Adopt Apple's naming rules for uniformity. As for acronyms, the readability makes keeping them upper-case worth it.


### Semantics

#### Avoid single-character names for types, variables, and functions. The only place they are allowed is as indexes in iterators.
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

***Rationale:*** There is always a better name than single-character names. Even with `i`, it is still more readable to use `index` instead.


#### Avoid abbreviations as much as possible. (although [some](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/APIAbbreviations.html#//apple_ref/doc/uid/20001285-BCIHCGAE) are allowed (`min`/`max`))
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

***Rationale:*** Clarity is prioritized over slight brevity. 


#### Choose names that communicates as much information about what it is and *what it's for*.
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
    // is this the title or the content text?
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

***Rationale:*** Clarity is prioritized over slight brevity. Also, the more specific the name, the less likely they are to collide with other symbols.


#### When pertaining to URLs, distinguish strings from actual `NSURL`s by appending the suffix `~String`.
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

***Rationale:*** Saves a few seconds checking header declarations for the correct type.


#### Do not pertain to constructs (`class`, `struct`, `enum`, `protocol`, etc.) in their names.
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

***Rationale:*** The extra suffix is redundant. It should be noted though that Objective-C protocols with the same name as an existing Objective-C class are bridged to Swift with a `~Protocol` suffix (e.g. `NSObject` and `NSObjectProtocol`). But they are irrelevant to this guideline as they are automatically generated by the Swift compiler.


## Dependencies

### Import Statements

#### `import` statements for OS frameworks and external frameworks should be separated and alphabetized.
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

***Rationale:*** Reduce merge conflicts when dependencies change between branches.



## Declaration Order

#### All type declarations such as `class`, `struct`, `enum`, `extension`, and `protocol`s, should be marked with `// MARK: - <name of declaration>` (with hyphen)
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

***Rationale:*** Makes it easy to jump to specific types when using XCode's *Source Navigator*.


#### All properties and methods should be grouped into the superclass/protocol they implement and should be tagged with `// MARK: <superclass/protocol name>`. The rest should be marked as either `// MARK: Public`, `// MARK: Internal`, or `// MARK: Private`.
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

***Rationale:*** Makes it easy to locate where in the source code certain properties and functions are declared.


#### All `// MARK:` tags should have two empty lines above and  one empty line below.
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

***Rationale:*** Aesthetic. Gives breathing room between type declarations and function groups.


#### The groupings for `// MARK:` tags should be ordered as follows:
- `// MARK: Public`
- `// MARK: Internal`
- Class Inheritance (parent-most to child-most)
    - `// MARK: NSObject`
    - `// MARK: UIResponder`
    - `// MARK: UIViewController`
- Protocol Inheritance (parent-most to child-most)
    - `// MARK: UITableViewDataSource`
    - `// MARK: UIScrollViewDelegate `
    - `// MARK: UITableViewDelegate`
- `// MARK: Private`

***Rationale:*** Makes it easy to locate where in the source code certain implementations are declared. `public` and `internal` declarations are more likely to be referred to by API consumers, so are declared at the top.


#### Under each grouping above, declarations should be ordered as follows:
- `@` properties (`@NSManaged`, `@IBOutlet`, `@IBInspectable`, `@objc`, `@nonobjc`, etc.)
- `lazy var` properties
- computed `var` properties
- other `var` properties
- `let` properties
- `@` functions (`@NSManaged`, `@IBAction`, `@objc`, `@nonobjc`, etc.)
- other functions

***Rationale:*** `@` properties and functions are more likely to be referred to (such as when checking KVC keys or `Selector` strings, or when cross-referencing with Interface Builder) so are declared higher.



## Protection from Dynamism

#### All Objective-C `protocol` implementations, whether properties or methods, should be prefixed with `@objc dynamic`
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

***Rationale:*** Prevents horrible compiler optimization bugs. Trust us.


#### All `IBAction`s and `IBOutlet`s should be declared `dynamic`
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

***Rationale:*** The Swift compiler sometimes mangle these. Writing `dynamic` guarantees safety, even when we declare them as `private`. 


#### All properties used for KVC/KVO and all functions used as `Selector`s should be marked `dynamic`
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

***Rationale:*** Same reason as the preceding rule, the Swift compiler sometimes mangle these. Writing `dynamic` guarantees safety, even when we declare them as `private`. 



## Type Inference



## Collections / SequenceTypes

#### `.count` should only be used when the count value itself is needed
<table>
<tr><th>OK</th></tr>
<tr>
<td><pre lang=swift>
let badgeNumber = unreadItems.count
</pre></td>
</tr>
</table>

Checking if empty or not:
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

Getting the first or last item:
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

Removing the first or last item:
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

Iterating all indexes:
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

Getting the first or last index:
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

Iterating all indexes except the last `n` indexes:
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

Iterating all indexes except the first `n` indexes:
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

***In general, if you have to add or subtract to `count`, there is probably a better, Swift-y way to do it.***

***Rationale:*** Clarity of intent, which in turn reduces programming mistakes (esp. off-by-one calculation errors).
