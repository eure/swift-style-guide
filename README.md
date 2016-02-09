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
- [Dynamic Protection](#dynamic-protection)
- [Type Inference](#type-inference)
- [Collections / SequenceTypes](#collections-sequencetypes)


## Whitespaces

- All source files should have a single trailing newline *at most*.
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

- Use 4 spaces for tabs. Set XCode's **Text Editing** settings as shown:
<img width="475" alt="screen shot 2016-02-09 at 14 52 28" src="https://cloud.githubusercontent.com/assets/3029684/12908678/f264612c-cf3c-11e5-8093-9ab04ac37dbc.png"/><br/>
**Rationale:** Prevents whitespace-only code diffs, while maintaining visually similar indentation across different text editors.


- Commas (`,`) should have no whitespace before it, and either one space or one newline after.
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

- Colons (`:`) used to indicate type should have once space after it and no whitespace before it.
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

- Colons (`:`) for `case` statements should have no whitespace before it, and either one space or one newline after it. A single-line statement after the `case` can be written inline.
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
    
case .Failure: self.failure()
}
</pre></td>
</tr>
</table>
**Rationale:** Prevents whitespace-only code diffs, while keeping `case` statements visually aligned and uniform with each other.

- Opening curly braces (`{`) should be one space following the previous non-whitespace character.
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

- Opening curly braces (`{`) for type declarations, functions, and closures should be followed by one empty line.
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

- Empty declarations should be written in empty curly braces (`{}`), otherwise a comment should indicate the reason for the empty implementation.
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
**Rationale:** Makes it clear that the declaration was meant to be empty and not just a missing `TODO`.

- Closing curly braces (`}`) should not have empty lines before it. For single line closures, there should be one space between the last statement and the closing brace.
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


## Naming

## Dependencies

## Declaration Order

## Dynamic Protection

## Type Inference

## Collections / SequenceTypes
