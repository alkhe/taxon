# taxon

`taxon` is a concise type system for annotating and documenting Javascript APIs.

## Basics

### Primitives
```js
any ('a' | 5 | [])
int (123)
real (3.0234)
bool (true)
string ('hello')
none (undefined)
void (undefined)
null (null)
nan (NaN)
```

### Builtins
```js
Array<Type>: [...values: Type]
Shallow<Type>: { ...properties: Type }
Maybe<Type>: Type | none
Tuple<A, B, ..., Z>: [A, B, ..., Z]
Of<A, B, ..., Z>: A | B | ... | Z
```

### Definition
```js
Integer: int
```

### Validation
```js
'x' :: string // true
5.6 :: int // false
undefined :: Maybe<bool> // true
true :: Maybe<bool> // true
3 :: Maybe<bool> // false
```

### Application
```js
[Class.myMethod]: Function
[Class.instance]: Data
```
```js
[Class
	[myMethod]: Function
	[instance]: Data
]
```

## Rules

### Functions
```js
Adder: (augend: int, addend: int) => int
```

#### Optional Arguments
```js
Alert: (message: string, [type: string]) => void
```

#### Default Arguments
```js
Alert: (message: string, type = 'default': string) => void
```

### Objects
```js
Human: { height: int, weight: int }
```
```js
FunctionMap: { ...functions: Function }
```

## Templating
```js
Accumulator<Type, Modifier>: (acc: Type, mod: Modifier) => Type
```

## Algebraics
```js
Computable: int | real
```
```js
Leaf: int
Branch: { value: int, ...leaves: Maybe<Node> }
Node: Branch | Leaf
```

## Composition

### Property
```js
Human: { height, weight: int }
```
```js
Human: { (height, weight): int }
```

### Algebraic
```js
Leaf<Value>: Value
Branch<Value>: { value: Value, (left, right): Maybe<Leaf<Value>> }
Node: Branch | Leaf
Heap: Node<int>
```

Algebraics cannot be used directly as applications.

### Substitution
```js
Animal: { weight: int }
Dog: { #Animal, color: string }
```
```js
[View]: (element: HTMLElement) => View
[Model]: (model: Shallow<Function>) => Model
[ViewModel]: (#View, #Model) => Construct
```
