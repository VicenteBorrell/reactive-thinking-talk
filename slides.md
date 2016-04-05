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
## *SLQ*

---

## XML
## HTML
## SLQ
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
### (functionally pure)

---

## Reactive Libraries

- [RxSwift](https://github.com/ReactiveX/RxSwift)
- [ReactiveCocoa](https://github.com/reactivecocoa/reactivecocoa)
- [BrightFutures](https://github.com/Thomvis/BrightFutures)

![fill](images/background_reading.jpg)

---

## Motivation :yum:
#### _Why should I stick to Reactive programming?_

![fill](images/background_motivation.jpeg)


---

```swift
let todo: String = "Move the motivation points to different slides to make it dynamic"
```

- Inmutability
- Side states safe (clear source of truth)
- Binding
- Encapsulated Observable actions
- Composable
- Ease operatiosn
- Threading (observer & execute)

<!-- SAKY -->

---

## Reactive Thinking :grimacing:

![fill](images/background_thinking.jpeg)

<!-- PEPI -->
---

## Thinking in terms of
# _Observables_
#### Or _Signals/Producers_ in ReactiveCocoa

<!-- PEPI -->
---

#### _Creating_ observables
####  _Combining_ observables
#### _Observing_ observables
<!-- PEPI -->

---

### _Creating_ observables
####  _Combining_ observables
#### _Observing_ observables
<!-- PEPI -->

---

- External actions

```swift
let button = UIButton()
button.rx_controlEvent(.TouchUpInside)
  .subscribeNext { _ in
    print("The button was tapped")
  }
```
<!-- PEPI -->

---

## Creating Observables

- Existing Patterns
- Backend actions

<!-- PEPI -->

---

#### _Creating_ observables
###  _Combining_ observables
#### _Observing_ observables

<!-- PEPI -->

---

#### _Creating_ observables
####  _Combining_ observables
### _Observing_ observables

<!-- PEPI -->

---

## Combining Observables
- Operators

```swift
let todo: String = "Show some examples of operators"
```
<!-- PEPI -->

---

## Observing

- Binding
- Subscribing

<!-- PEPI -->

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
let todo: String = "Add code example"
```
<!-- SAKY -->


---

## Retain cycles

```swift
let todo: String = "Add code example"
```
<!-- SAKY -->

---

## Threading?

```swift
let todo: String = "Add code example"
```

---

## A great **power** comes with a great **responsibility**

![fit](images/background_spiderman.png)

<!-- SAKY -->

---

![](images/pug_gif.gif)

---

# Conclusions

---

# References

rxmarbles.cmo
http://community.rxswift.org

<!-- PEPI -->

---

## We are hiring
#### pepi@soundcloud.com - isaac@letgo.com
####  :snowflake: BERLIN - BARCELONA :palm_tree:

![fill](images/background_hiring.jpg)

---

GITDO

<!-- PEPI -->
