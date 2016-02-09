# Eureka Swift Style Guide

This style guide is a product of our iOS team's more than a year writing, reviewing, and testing Swift code. It reflects the coding rules we have observed as "efficient" in our production apps.

The guidelines here try to accomplish/encourage practices that accomplish the following goals:

- to make it hard to write programmer errors, or at least make them hard to miss
- to increase readability and clarity of intent, with assumption that the code will be reviewed/consumed by a different person
- to minimize unnecessary code bloat
- to observe aesthetics that the majority of the team voted for

We understand that a quite a few of the guidelines below are controversial and may even be opposite what the Swift community generally observes, but we have tried and tested these practices within our team.

That said, this is a live document. As our app grows, our team improves, and Swift evolves, our practices will adapt as well and this list will be updated if needed.


## Table of Contents
- [Whitespaces](#whitespaces)
- [Naming](#naming)
- [Dependencies](#dependencies)
- [Declaration Order](#declaration-order)
- [Protection from Dynamism](#protection-from-dynamism)
- [Type Inference](#type-inference)
- [Collections / SequenceTypes](#collections--sequencetypes)



## Whitespaces

### All source files should end with a single trailing newline (only).
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

**Rationale:** Prevents no-trailing-newline errors and reduces noise in commit diffs.


### Use 4 spaces for tabs.
 Set XCode's **Text Editing** settings as shown:
 
<img width="475" alt="screen shot 2016-02-09 at 14 52 28" src="https://cloud.githubusercontent.com/assets/3029684/12908678/f264612c-cf3c-11e5-8093-9ab04ac37dbc.png"/><br/>
**Rationale:** Prevents whitespace-only code diffs, while maintaining visually similar indentation across different text editors.


### Commas (`,`) should have no whitespace before it, and either one space or one newline after.
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

**Rationale:** Prevents whitespace-only code diffs.


### Colons (`:`) used to indicate type should have once space after it and no whitespace before it.
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

**Rationale:** Prevents whitespace-only code diffs.


### Colons (`:`) for `case` statements should have no whitespace before it, and either one space or one newline after it. A single-line statement after the `case` can be written inline.
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
<tr>
<td><pre lang=swift>
switch result {

case .Success: self.completion()
case .Failure: self.failure()
}
</pre></td>
<td><pre lang=swift>
switch result {

case .Success: self.doSomething()
    self.completion()
    
case .Failure:self.failure()
}
</pre></td>
</tr>
</table>

**Rationale:** Prevents whitespace-only code diffs, while keeping `case` statements visually aligned and uniform with each other.


### Opening curly braces (`{`) should be one space following the previous non-whitespace character.
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

**Rationale:** Prevents whitespace-only code diffs.


### Opening curly braces (`{`) for type declarations, functions, and closures should be followed by one empty line.
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

**Rationale:** Prevents whitespace-only code diffs.


### Empty declarations should be written in empty curly braces (`{}`), otherwise a comment should indicate the reason for the empty implementation.
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

**Rationale:** Makes it clear that the declaration was meant to be empty and not just a missing `TODO`. <br/>


### Closing curly braces (`}`) should not have empty lines before it. For single line closures, there should be one space between the last statement and the closing brace.
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

**Rationale:** Prevents whitespace-only code diffs, while keeping code compact.


### All functions should be at least one empty line apart each other
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

**Rationale:** Gives breathing room between code blocks.



## Naming



## Dependencies

### `import` statements for OS frameworks and external frameworks should be separated and alphabetized.
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

**Rationale:** Reduce merge conflicts when dependencies change between branches.



## Declaration Order

### All type declarations such as `class`, `struct`, `enum`, `extension`, and `protocol`s, should be marked with `// MARK: - <name of declaration>` (with hyphen)
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

**Rationale:** Makes it easy to jump to specific types when using XCode's *Source Navigator*.


### All properties and methods should be grouped into the protocol/subclass they implement and should be tagged with `// MARK: <protocol/superclass name>`. The rest should be marked as either `// MARK: Public`, `// MARK: Internal`, or `// MARK: Private`.
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

**Rationale:** Makes it easy to locate where in the source code certain properties and functions are declared.


### The first `// MARK:` in a type declaration should have one empty line above, the rest should have two empty lines above. All `// MARK:` tags should have one empty line below.
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

**Rationale:** Aesthetic. Gives breathing room between type declarations and function groups.


### The groupings for `// MARK:` tags should be ordered as follows:
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

**Rationale:** Makes it easy to locate where in the source code certain implementations are declared. `public` and `internal` declarations are more likely to be referred to by API consumers, so are declared at the top.


### Under each grouping above, declarations should be ordered as follows:
- `@` properties (`@NSManaged`, `@IBOutlet`, `@IBInspectable`, `@objc`, `@nonobjc`, etc.)
- `var` properties
- computed properties
- `lazy` properties
- `let` properties
- `@` functions (`@NSManaged`, `@IBAction`, `@objc`, `@nonobjc`, etc.)
- other functions

**Rationale:** `@` properties and functions are more likely to be referred to (such as when checking KVC keys or `Selector` strings, or when cross-referencing with Interface Builder) so are declared higher.



## Protection from Dynamism

### All Objective-C `protocol` implementations, whether properties or methods, should be prefixed with `@objc dynamic`
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

**Rationale:** Prevents horrible compiler optimization bugs. Trust us.


### All `IBAction`s and `IBOutlet`s should be declared `dynamic`
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

**Rationale:** The Swift compiler sometimes mangle these. Writing `dynamic` guarantees safety, even when we declare them as `private`. 


### All properties used for KVC/KVO and all functions used as `Selector`s should be marked `dynamic`
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

**Rationale:** Same reason as the preceding rule, the Swift compiler sometimes mangle these. Writing `dynamic` guarantees safety, even when we declare them as `private`. 



## Type Inference



## Collections / SequenceTypes


