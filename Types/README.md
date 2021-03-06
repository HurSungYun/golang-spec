# [타입(Types)](#types)

* Go 버전: 1.9
* 원문: [Types](https://golang.org/ref/spec#Types)
* 번역자: Jhonghee Park (@jhonghee), 허성연 (@hursungyun)

A type determines the set of values together with operations and methods specific to those values.
A type may be denoted by a *type name*, if it has one, or specified using a *type literal*, which composes a type from existing types.

타입은 어떠한 값들의 집합과 그 값들에 대한 연산과 메소드로 이루어져 있다.
타입은 *타입 이름*을 가지고 있는 경우 그것으로 표시되거나, 이미 존재하는 타입들을 조합한 *타입 리터럴*을 사용하여 표시된다.

<pre>
<a id="Type">Type</a>      = <a href="#TypeName">TypeName</a> | <a href="#TypeLit">TypeLit</a> | "(" <a href="#Type">Type</a> ")" .
<a id="TypeName">TypeName</a>  = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> | <a href="/Expressions/qualified_identifiers.html#QualifiedIdent">QualifiedIdent</a> .
<a id="TypeLit">TypeLit</a>   = <a href="/Types/array_types.html#ArrayType">ArrayType</a> | <a href="/Types/struct_types.html#StructType">StructType</a> | <a href="/Types/pointer_types.html#PointerType">PointerType</a> | <a href="/Types/function_types.html#FunctionType">FunctionType</a> | <a href="/Types/interface_types.html#InterfaceType">InterfaceType</a> | <a href="/Types/slice_types.html#SliceType">SliceType</a> | <a href="/Types/map_types.html#MapType">MapType</a> | <a href="/Types/channel_types.html#ChannelType">ChannelType</a> .
</pre>

Named instances of the boolean, numeric, and string types are [predeclared](/Declarations%20and%20scope/predeclared_identifiers.html). 
Other named types are introduced with [type declarations](/Declarations%20and%20scope/type_declarations.html).
*Composite types*—array, struct, pointer, function, interface, slice, map, and channel types—may be constructed using type literals.

boolean, numeric, 그리고 string 타입의 인스턴스들은 [미리 선언되어(predeclared)](/Declarations%20and%20scope/predeclared_identifiers.html)있다.
다른 이름있는 타입들은 [타입 선언(type declarations)](/Declarations%20and%20scope/type_declarations.html)을 통해 쓰일 수 있다.
*복합 타입(Composite types)*-배열(array), 구조체(struct), 포인터(pointer), 함수(function), 인터페이스(interface), 슬라이스(slice), 맵(map), 그리고 채널(channel) 타입-은 타입 리터럴을 사용해 만들어 질 수 있다.


Each type T has an *underlying type*: If T is one of the predeclared boolean, numeric, or string types, or a type literal, the corresponding underlying type is T itself. Otherwise, T's underlying type is the underlying type of the type to which T refers in its [type declaration](/Declarations%20and%20scope/type_declarations.html).

각각의 타입 T는 *내재 타입(underlying type)*을 가지고 있다: 만약 T가 사전에 선언(predeclared)된 boolean, numeric, 또는 string 타입 중 하나이거나 타입 리터럴이라면 T 스스로가 내재 타입이 된다.
그 외의 경우, T의 내재 타입은 [타입 선언(type declarations)](/Declarations%20and%20scope/type_declarations.html)에서 T가 참조하는 타입의 내재 타입이다.

```
type (
    A1 = string
    A2 = A1
)

type (
    B1 string
    B2 B1
    B3 []B1
    B4 B3
)
```

The underlying type of string, A1, A2, B1 and B2 is string. The underlying type of []B1, B3, and B4 is []B1.

string, A1, A2, B1 그리고 B2의 내재 타입은 string이다. []B1, B3, 그리고 B4의 내재 타입은 []B1이다.