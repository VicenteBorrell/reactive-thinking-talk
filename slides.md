# Reactive Thinking in iOS Development

#### _@pepibumur / @saky_

![image](https://images.unsplash.com/photo-1433190152045-5a94184895da?crop=entropy&dpr=2&fit=crop&fm=jpg&h=975&ixjsv=2.1.0&ixlib=rb-0.3.5&q=50&w=1700)

---

# Who?

**@pepibumur**
iOS Developer at [SoundCloud](https://github.com/pepibumur)
GitHub: [pepibumur](https://github.com/pepibumur)
Twitter: [pepibumur](https://twitter.com/pepibumur)

**@saky**
iOS Developer at [Letgo](letgo.com)
GitHub: [isaacroldan](https://github.com/isaacroldan)
Twitter: [saky](https://github.com/saky)

![fit left](images/who.png)

_[GitDo.io](http://gitdo.io) our spare time project_

---

# Index

- Programming Paradigms
- **Reactive** Libraries
- **Reactive** Motivation
- **Reactive** Thinking
- **Reactive** Caveats
- Conclusion

---

## Paradigms :book:
#### _Ways of seeing the world when it comes to programming_

![fill](images/background_dog.jpeg)

---

### [Wikipedia](https://en.wikipedia.org/wiki/Programming_paradigm)

Data-Driven, [**Declarative**](https://en.wikipedia.org/wiki/Declarative_programming), Dynamic, End-User, Event-Driven, Expression-Oriented, Feature-Oriented, Function-level, Generic, [**Imperative**](https://en.wikipedia.org/wiki/Imperative_programming), Inductive, Language Oriented, Metaprogramming, Non-Structured, Nondeterministic, Parallel computing, Point-free Style, Structured, Value-Level, Probabilistic

---

### Imperative Programming
### Declarative Programming

---

### _Imperative Programming_
### Declarative Programming

---
# How? 🤔
---

```swift
func userDidSearch(term: String) {
	let apiReults = api.search(term: term).execute()
	self.items = self.adaptResults(apiResults)
	self.tableView.reloadData()
}
```

---

## Sequence of *steps*
### that happen in *order*

---

## *Natural* way to program

---

## Execution *state*
#### *(aka side effect)*

---

### Imperative Programming
### _Declarative Programming_

---

# What? 🤔

---

```swift
let predicate = NSPredicate(format: "name == %@", "Pedro")
let regex = NSRegularExpression(pattern: ".+", options: 0)
```

---

## It *doesn't* describe the control flow

---

## *XML*

---

## XML
## *HTML*

---

## XML
## HTML
## *SQL*

---

## XML
## HTML
## SQL
## *Reactive Programming*

---

## *Asynchronous* data-flow programming
#### Describes the state propagation

####### [The introduction to Reactive Programming that you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)

---

```swift
self.fetchAccountCommandFactory.githubAccount()
  .map { $0.hasFeature(.ImagePicker) }
  .observeOn(MainScheduler.instance)
  .subscribeNext { [weak self] hasFeature in
      if hasFeature {
          self?.view?.showImagePicker()
      } else {
          self?.openSubscriptionView()
      }
  }
  .addDisposableTo(self.disposeBag)
```

---

## _Functional_ Reactive Programming
### *(aka FRP)*

---

## Describes *how* data transform from one state to another and *what* triggers it

---

## State contained in a *tree* of transformation *nodes*
#### (functionally pure)

---

## Reactive Libraries

- [RxSwift](https://github.com/ReactiveX/RxSwift)
- [ReactiveCocoa](https://github.com/reactivecocoa/reactivecocoa)
- [BrightFutures](https://github.com/Thomvis/BrightFutures)
- [ReactKit](https://github.com/ReactKit/ReactKit)
- [Bond](https://github.com/SwiftBond/Bond)
<br>
- _More and more..._ [PromiseKit](https://github.com/mxcl/PromiseKit), [Bolts](https://github.com/BoltsFramework), [ReactiveKit](https://github.com/ReactiveKit/ReactiveKit)...

![fill](images/background_reading.jpg)

---

### What _library_ should i use? :sweat_smile:

---

### What _library_ should i use? :sweat_smile:
### Do i need a _library_ for this? :hushed:

---

## Swift 

```swift
var userName: String {
  didSet {
    // React to changes in variables

  }
}
```

---

## Swift

```swift
var userName: String {
  didSet {
    // React to changes in variables
    view.updateTitle(userName)
  }
}
```

---

## Motivation :yum:
#### _Why should I stick to Reactive programming?_

![fill](images/background_motivation.jpeg)


---

- immutability
- Side states safe (clear source of truth)
- Binding
- Encapsulated Observable actions
- Composable
- Ease operations
- Threading (observer & execute)

<!-- SAKY -->

---

- immutability
- Side states safe (clear source of truth)
- _Binding_
- Encapsulated Observable actions
- Composable
- Ease operations
- Threading (observer & execute)

---

# Binding

---

# _UI_ Binding

---

# _UI_ Binding

![inline](images/uibinding1.png)

---

# _UI_ Binding

![inline](images/uibinding2.png)


---
- immutability
- Side states safe (clear source of truth)
- Binding
- Encapsulated Observable actions
- _Composable_
- Ease operations
- Threading (observer & execute)

---

![inline](images/combining2.png)

---

![inline](images/combining.png)

---

- immutability
- Side states safe (clear source of truth)
- Binding
- Encapsulated Observable actions
- Composable
- Ease operations
- _Threading_ (observer & execute)

---

## Threading

![inline](images/threading.png)

---
## Reactive Thinking :grimacing:

![fill](images/background_thinking.jpeg)

---

## Thinking in terms of
# _Observables_
#### Or _Signals/Producers_ in ReactiveCocoa

---

### Actions can be
# **observed**
### How? 🙄

![fill](images/observe.jpg)

---

# Operations

> RxSwift

```swift
Observable<String>.create { (observer) -> Disposable in
    observer.onNext("next value")
    observer.onCompleted()
    return NopDisposable.instance // For disposing the action
}
```

> ReactiveCocoa

```swift
SignalProducer<String>.create { (observer, disposable) in
	observer.sendNext("next value")
	observer.sendComplete()
}
```


---

## Existing Patterns

#### _RxSwift_ ▶︎ RxCocoa (extensions)

#### _ReactiveCocoa_ ▶︎ DO IT YOURSELF

---

# UIKit

```swift
let button = UIButton()
button.rx_controlEvent(.TouchUpInside)
  .subscribeNext { _ in
    print("The button was tapped")
  }
```

---

# Notifications

```swift
NSNotificationCenter.defaultCenter()
	.rx_notification("my_notification", object: nil)
	.subscribeNext { notification
		// We got a notification
	}
```

---

# Delegates

```swift
self.tableView.rx_delegate // DelegateProxy
  .observe(#selector(UITableViewDelegate.tableView(_:didSelectRowAtIndexPath:)))
  .subscribeNext { (parameters) in
		// User did select cell at index path
  }
```

---

# _Playing_ 🏈
### with Observables

![fill](images/playing.jpeg)

---

## Observable

```swift
let tracksFetcher = api.fetchTracks // Background
	.asObservable()
```

---

## Error handling

```swift
let tracksFetcher = api.fetchTracks // Background
	.asObservable()
	.retry(3)
	.catchErrorJustReturn([])
```

---

## Mapping

```swift
let tracksFetcher = api.fetchTracks // Background
	.asObservable()
	.retry(3)
	.catchErrorJustReturn([])
	.map(TrackEntity.mapper().map)
```

---

## Filtering

```swift
let tracksFetcher = api.fetchTracks // Background
	.asObservable()
	.retry(3)
	.catchErrorJustReturn([])
	.map(TrackEntity.mapper().map)
	.filter { $0.name.contains(query) }
```

---

## Flatmapping

```swift
let tracksFetcher = api.fetchTracks // Background
	.asObservable()
	.retry(3)
	.catchErrorJustReturn([])
	.map(TrackEntity.mapper().map)
	.filter { $0.name.contains(query) }
	.flatMap { self.rx_trackImage(track: $0) }
```

---

## Observation thread

```swift
let tracksFetcher = api.fetchTracks // Background
	.asObservable()
	.retry(3)
	.catchErrorJustReturn([])
	.map(TrackEntity.mapper().map)
	.filter { $0.name.contains(query) }
	.flatMap { self.rx_trackImage(track: $0) }
	.observeOn(MainScheduler.instance) // Main thread
```

---

## Throttling
#### _Tipical reactive example_

```swift
func tracksFetcher(query: String) -> Observable<[TrackEntity]>

searchTextField
	.rx_text.throttle(0.5, scheduler: MainScheduler.instance)
	.flatmap(tracksFetcher)
	.subscribeNext { tracks in
		// Yai! Tracks searched
	}
```

---

# _Other_ operators

Combining / Skipping Values / Deferring / Concatenation / Deferring / Take some values / Zipping

> Ease plugging observables

---

# Observing 🤓
### _events_


---

## Subscribing

```swift
observable
  subscribe { event
		case .Next(let value):
			print(value)
		case .Completed:
			print("completed")
		case .Error(let error):
			print("Error: \(error)")
	}
```

---

## Bind _changes_ over the time to an _Observable_

---

### observable ► _bind_ ► observer
#### _(observer subscribes to observable events)_

---

```swift
observable // Observable<String>
	.bindTo(field.rx_text)
```

---

# `rx_text`? :confused:

---

# Reactive _Property_
#### (Control Property in RxSwift)

---

# Subject

#### _Observer_ & _Observable_
##### (Yes.. both)

---

# Reactive _Variable_
#### (Variable in RxSwift)
#### (Property in ReactiveCocoa)

---

```swift
let text: Variable<String> = Variable("")
text.asObservable()
	.subscribeNext { newText
		print("The text did change. New text: \(newText)")
	}

```

---


# :weary: Caveats
#### _Because yes..._
#### _it couldn't be perfect_

<!-- SAKY -->

<br><br>

![fill](images/background_caveats.jpeg)

---

## Debugging

```swift
self.createComment(issueId: issueId, body: body).observable()
    .observeOn(MainScheduler.instance)
    .doOn(onError: { [weak self] error in
        // show Error
    })
    .subscribeCompleted { [weak self] in
        // show Success
    }
    .addDisposableTo(self.disposeBag)

```
<!-- SAKY -->
// RXSWIFT: operador para debuggear -> muestra traza

---

## Retain cycles

```swift
class IssuePresenter {
  let commandFactory = CommandFactory()

  func fetch() {
     commandFactory.fetchCommand.observable()
     .bindTo { self.something }
     .addDisposableTo(disposeBag)
  }
}

```
<!-- SAKY -->

---

## Retain cycles

```swift
class IssuePresenter {
  let commandFactory = CommandFactory()

  func fetch() {
     commandFactory.fetchCommand.observable()
     .bindTo { self.something }
     .addDisposableTo(disposeBag)
  }
}

presenter -> commandFactory -> fetchCommand -> presenter

```
<!-- SAKY -->

---

## Retain cycles

```swift
class IssuePresenter {
  let commandFactory = CommandFactory()

  func fetch() {
     commandFactory.fetchCommand.observable()
     .bindTo { [weak self] in self?.something }
     .addDisposableTo(disposeBag)
  }
}

presenter -> commandFactory -> fetchCommand -> presenter

```
<!-- SAKY -->

---

## Unsubscription
// Disposable bag


---

## Threading?

```swift
let todo: String = "Add code example"
```

---

## A great **power** comes with a great **responsibility**

![fill](images/background_spiderman.png)

<!-- SAKY -->

don't remember what is this about xD

---

![](images/pug_gif.gif)

---

# Conclusions

---

## Prevents _stateful_ code

---

## Aims _unidirectional_ data flow


---

## Data flow manipulation becomes _easier_

---

# But... :sweat:

---

## You couple your project to a _library_ :couple:

---

## Reactive code _spreads_ like a virus :alien:

#### Overreactive

---

## Define reactive design _guidelines_ and stick to them

---

## Have Reactive fun :tada:

---

# References

[rxmarbles.cmo](rxmarbles.cmo)
[http://community.rxswift.org](http://community.rxswift.org)
[github.com/rxswift/rxswift](https://github.com/ReactiveX/RxSwift/)
[github.com/reactivecocoa/reactivecocoa](https://github.com/reactivecocoa/reactivecocoa)

---

## We are hiring
#### pepi@soundcloud.com - isaac@letgo.com
####  :snowflake: BERLIN - BARCELONA :palm_tree:

![fill](images/background_hiring.jpg)

---

![fill](images/gitdo.png)
