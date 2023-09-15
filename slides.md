---
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: ADTs
monaco: false
---

# Tipos de Dados Algébricos 

ADTs - Algebraic Data Types

---
title: Information
layout: center
---

# Jeova

---
transition: fade-out
---

# Conjuntos

<v-clicks>

- Tipos são conjuntos
- Conjunto `Boolean = { True, False }`
- Conjunto `Int8 = { 0, 1, 2, ..., 255 }`
- Tamanho do conjunto -> Cardinalidade
- `|Boolean| = 2`
- `|Int8| = 256`

</v-clicks>

---
transition: fade-out
---

# Operações de Conjuntos

## Union

<v-clicks>

- Conjunto `V = { a, e, i, o, u }`
- Conjunto `B = { 0, 1 }`
- `V Union B = { a, e, i, o, u, 0, 1 }`

</v-clicks>

## Disjoint Union

<v-clicks>

- `V DUnion B = { V:a, V:e, V:i, V:o, V:u, B:0, B:1 }`
- `|V DUnion B| = |V| + |B|`

</v-clicks>
---
transition: fade-out
---

# Em Código

```haskell {1-2|4-6|7-8|all}
-- V = { a, e, i, o, u }
data Vogal = A | E | I | O | U

-- B = { 0, 1 }
data Binario = Zero | Um

-- V DUnion B = { V:a, V:e, V:i, V:o, V:u, B:0, B:1 }
data VogalBinario = VogalCons Vogal | BinarioCons Binario

a = VogalCons A
e = VogalCons E
z = BinarioCons Zero
```

<v-clicks>

- Conjuntos: Disjoint Union 
- `Vogal DUnion Binario = Vogal 'OU' Binario`
- `|V DUnion B| = |V| + |B|`
- Tipos: Sum Types ou Tagged Union

</v-clicks>

---
transition: fade-out
---

# Operações de Conjuntos

## Product

<v-clicks>

- Conjunto `V = { a, e, i, o, u }`
- Conjunto `B = { 0, 1 }`
- `V x B = { (a,0), (a,1), (e,0), (e,1), ..., (u,0), (u,1)}`
- `|V x B| = |V| * |B| = 10`

</v-clicks>

---
transition: fade-out
---

# Em Código

```haskell {1-5|7-8|all}
-- V = { a, e, i, o, u }
data Vogal = A | E | I | O | U

-- B = { 0, 1 }
data Binario = Zero | Um

-- V x B = { (a,0), (a,1), (e,0), (e,1), ..., (u,0), (u,1)}
type VogalBinarioPar = (Vogal,Binario)

a0 = (A,Zero)
a1 = (A,Um)
u0 = (U,Zero)
```

<v-clicks>

- Conjuntos: Produto Cartesiano
- `Vogal x Binario = Vogal 'E' Binario`
- `|V x B| = |V| * |B|`
- Tipos: Product Types

</v-clicks>

---
transition: fade-out
---

# Algebraic Data Types

<v-clicks>

- Tipos que são construídos com `Sum Types` e `Product Types`

Exemplos em:

- haskell
- kotlin
- typescript

</v-clicks>

---
transition: fade-out
---

# Haskell

```haskell {1|3|5|7|9|9-15|all}
data Hortalica = Couve | Alface
    
data Fruta = Laranja | Pera | Mamao 

data FormaCobranca = Kilo | Unidade

type Preco = Double

data HortiFruti = Horti Hortalica Preco | Fruti Fruta FormaCobranca Preco

hortiFruti= [
    Horti Couve 5.00,
    Fruti Mamao Unidade 7.50,
    Fruti Laranja Kilo 4.50
  ]

main = print hortiFruti
```

---
transition: fade-out
---

# Kotlin

[Link](https://pl.kotl.in/6LmeUQJ_Z)

```kotlin {1|3|5|7|9|9-12|14-18|all} {maxHeight:'45vh'} 
enum class Hortalica { Couve, Alface }
    
enum class Fruta { Laranja, Pera, Mamao }

enum class FormaCobranca { Kilo, Unidade }

typealias Preco = Double

sealed class HortiFruti()

data class Horti(val horti: Hortalica, val preco: Preco): HortiFruti()
data class Fruti(val fruti: Fruta, val cobranca: FormaCobranca, val preco: Preco): HortiFruti()

val hortiFruti = listOf(
    Horti(Hortalica.Couve, 5.00),
    Fruti(Fruta.Mamao, FormaCobranca.Unidade, 7.50),
    Fruti(Fruta.Laranja, FormaCobranca.Kilo, 4.50)
)

fun main() {
    println(hortiFruti)
}
```

---
transition: fade-out
---

# TypeScript 

[Link](https://www.typescriptlang.org/play?noFallthroughCasesInSwitch=true#code/KYOwrgtgBAEg9gJwC4EMA2BLAxiqBvKAYTjADdgoAaKAQTQDMUsKBfAKCk6jdEigDEEYVPigAZFAhQgAVimoAFYFOoBZFBBRwo7HuGj9Em4gCMpIHKIDSGNHGoBVEBgAmKF6zZskATwAOFAoIwFjaALxQ+ibKXr4BsIhIGILCGFAR8MhpAD4CQkleGCBIyozMCVn4HFwA+qgA5gBcUADkABaJGC2U1ZwdWc2ZqJg4PVxQfsGhzUEhcGy6RSUIZRQpSVXjdShNrfT5XWNc+6nN6-K9UKFm0jhnRiim5qOXk3MzU-O6oSAAzkhQfpJdYYZo0BBSHwAHiGyQOAD50lAANqXAjbXbtTrdQGdQaJdDYFAAOmIZGA1De0ygAFZiQAGek6I6cdENZotE5JHFc0F5YQk9SaexXOA3Cwoe4IYxi54kpyudwUiafZoAdmJNKZLBZogxHN5PIOZ3yJIk5jk1GucqlMvFOGJNjslNVUAALJrtT0ALpeH6-OBoYDEor0OAACiBcNSAEpLkA)

```ts {1|3|5|7|9-21|23-27|all} {maxHeight:'45vh'}
enum Hortalica { Couve , Alface }
    
enum Fruta { Laranja, Pera, Mamao }

enum FormaCobranca { Kilo, Unidade }

type Preco = number

type HortiFruti = Horti | Fruti

interface Horti {
    _tag: 'horti',
    horti: Hortalica,
    preco: Preco
}

interface Fruti {
    _tag: 'fruti',
    fruti: Fruta,
    cobranca: FormaCobranca,
    preco: Preco
}

const hortiFruti: Array<HortiFruti> = [
    { _tag: 'horti', horti: Hortalica.Couve, preco: 5.00 },
    { _tag: 'fruti', fruti: Fruta.Mamao, cobranca: FormaCobranca.Unidade, preco: 7.50 },
    { _tag: 'fruti', fruti: Fruta.Laranja, cobranca: FormaCobranca.Kilo, preco: 4.50 },
]

console.info(hortiFruti)
```

---
transition: fade-out
---

# Final: Scala 3

[Link](https://scastie.scala-lang.org/ieMliDxRRe2a4zjxFUnjEw)

```scala {1-17|18-20|22-30|32-37|39-47|49-57|59-69|59-74|all} {maxHeight:'45vh'} 
/*
  Dada uma lista de pessoas, com nomes e idades, faça consultas baseado na idade.

  Nome   | Idade
  -----------------
  alice  | 65
  bob    | 25
  chien  | 15
  daniel | 35
  elisa  | 45
  
  Busque todas as pessoas com idades
  - q1. maior que 30                 
  - q2. igual a 25                   
  - q3. menor ou igual a 45          
  - q4. maior que 20 e menor que 60  
*/
import FindByAgeCmd.*

type Age = Int

case class Person(name: String, age: Age)

val people = List(
  Person("alice", 65),
  Person("bob", 25),
  Person("chien", 15),
  Person("daniel", 35),
  Person("elisa", 45)
)

enum FindByAgeCmd:
  case EqualTo(value: Age)
  case GreaterThan(value: Age)
  case LessThan(value: Age)
  case OrCond(a: FindByAgeCmd, b: FindByAgeCmd)
  case AndCond(a: FindByAgeCmd, b: FindByAgeCmd)

def filterByAge(cmd: FindByAgeCmd, person: Person): Boolean = {  
  cmd match {
    case EqualTo(value) => person.age == value
    case GreaterThan(value) => person.age > value
    case LessThan(value) => person.age < value
    case OrCond(cmdA, cmdB) => filterByAge(cmdA, person) || filterByAge(cmdB, person)
    case AndCond(cmdA, cmdB) => filterByAge(cmdA, person) && filterByAge(cmdB, person)
  }
}

def show(cmd: FindByAgeCmd): String = {
  cmd match {
    case EqualTo(value) => s"Igual a $value"
    case GreaterThan(value) => s"Maior que $value"
    case LessThan(value) => s"Menor que $value"
    case OrCond(cmdA, cmdB) => s"(${show(cmdA)}) OU (${show(cmdB)})"
    case AndCond(cmdA, cmdB) => s"(${show(cmdA)}) E (${show(cmdB)})"
  }
}

/*
-- Busque todas as pessoas com idades
--  - q1. maior que 30                 -> GreaterThan 30
--  - q2. igual a 25                   -> EqualTo 25
--  - q3. menor ou igual a 45          -> OrCond (LessThan 45) (EqualTo 45)
--  - q4. maior que 20 e menor que 60  -> AndCond (GreaterThan 20) (LessThan 60)
*/
def query(cmd: FindByAgeCmd) = {
  val result = people.filter(p => filterByAge(cmd, p))
  println(s"${show(cmd)}: $result")
}

query(GreaterThan(30))
query(EqualTo(25))
query(OrCond(LessThan(45), EqualTo(45)))
query(AndCond(GreaterThan(20), LessThan(60)))
```

---
transition: fade-out
---

# Conclusão

<v-clicks>

- Fizemos uma ponte entre matematica e tipos
- ADTs são bons para modelagem do dominio
- ADTs contribuem para código idiomático
- ADTs podem oferecer formas de deixar o código mais seguro (exhaustive pattern matching)
- Varias linguagens modernas estão melhorando o suporte para ADTs
  - Java21: Pattern Matching, Records, Sealed Classes, Switch Expression
  - Python (PEP 622): type hints, @dataclass, @sealed, exhaustive pattern matching
  - Dart 3: Sealed classes, pattern matching
  - Scala 3


</v-clicks>

---
transition: fade-out
---

Fim
