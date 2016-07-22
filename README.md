# elm-cooking

A quick colleciton of notes and working code from my experiences learning elm inspired by the out of date https://github.com/izdi/elm-cheat-sheet .  My background is in dynamic typed languages such as elixir, ruby, javascript. I will attempt to illustrate "new to me" strong type concepts.  I will also attempt to document a few cookbook type methods to solve problems the elm way.  I will attempt to include examples which can be pasted into "try elm" http://elm-lang.org/try

`The version targeted for this document is 0.17.x`

I am not likley to put a ton of effort into editing or spellchecking this document.  I may not comply with style guides, feel free to use elm-format on the sample code.



##Matching and destructuring.

### Concepts used
- main
- type alias
- type signature | type annotation
- destructuring
- pattern matching
- string concatenation

To map a whole record and destructure it at the same time

```elm
-- pull in the text function used below
import Html exposing (text)

-- main runs an elm program, note the use of the infix operater
main =
  text <| "Hello, World!    " ++ match foo

-- simple type alias   
type alias Form = 
  { name :String }

-- "compound" type alias  
type alias Foo = 
 {form : Form
 , s : String}

 -- an inital copy of my type alias
foo : Foo
foo = { 
 form = {name = "foo"}
 , s = "bar"}

{- 
the curly brackets here destructure the Foo type argument into variables `s, form` which match the record field names
the `as` keyword interpolates the whole record into the variable `whole` which is the whole record
-}
-- 
match : Foo -> String
match ({s, form} as whole) = 
   toString (
     "--s: " 
     ++ s 
     ++ " --form: " 
     ++ (toString form) 
     ++ " --whole: " 
     ++ (toString whole)
     )
```


# Concepts

###`main` 
can't find docs for main

###`type alias` 
 - [example from the offical docs] (http://elm-lang.org/docs/syntax#type-aliases)

###`type signature | type annotation`

Functions require a type annotation which describes the function arguments as well as the type returned by the function.  Functions can be passed as arguments, so they also need annotation.  the trivial example below returns 2 as the string "2"

``` elm
-- pull in the text function used below
import Html exposing (text)

-- main runs an elm program, note the use of the infix operater
main =
  text <| fun 2

-- function that takes a single argument (Int), and returns a String
fun : Int -> String
fun int = 
  toString int

```

The next example here will create a new function that takes two arguments; the first is a function, the second is an integer.  It returns a String.

```elm
-- pull in the text function used below
import Html exposing (text, hr, div)

-- main runs an elm program, note the use of the infix operater
main =
  div [] [
   text <| fun 2
   , hr [] []
   , text <| fun_takes_fun fun 2
  ]

-- function that takes a single argument (Int), and returns a String
fun : Int -> String
fun int = 
  toString int
  
fun_takes_fun : ( Int -> String ) -> Int -> String
fun_takes_fun function_arg integer_arg =
  function_arg (integer_arg)
  -- you do not need the round brackets
  -- `function_arg integer_arg` works just fine and is the normal way to list arguments with spaces
```

 - [ search for "Functions as arguments"] ( http://www.elm-tutorial.org/en/01-foundations/03-functions-2.html )
 - [ potentailly dated and based on elm 16] (https://github.com/izdi/elm-cheat-sheet#type-annotation )
 -   

###`destructuring`

### Concepts used
- main
- tuple
- string concatenation

destructuring allows you to interpolate multiple variables from a datastructure.

``` elm
-- pull in the text function used below
import Html exposing (text)

-- main runs an elm program, note the use of the infix operater
main =
  text <| fun tuple

-- tuple with two integer values
tuple = (1,2)

-- function that takes a single argument (Int), and returns a String
fun : (Int, Int) -> String
fun (x, y) = 
  toString x
    ++ " <---------> "
    ++ toString y

```

###`pattern matching`

TODO

###`string concatenation`

Strings can be concatenated with the "++" operator along with several other options.

```elm

-- pull in the text function used below
import Html exposing (text)
import String

-- main runs an elm program, note the use of the infix operater
main =
  text <| getStrings

-- concat funciton using the ++ operator
concat : String -> String -> String
concat first second = 
  first ++ second

-- concat function using the String module
concat_with_String : String -> String -> String
concat_with_String first second = 
  String.concat [first, second]

-- list join using ":" and String.join
colon_join : List String -> String
colon_join list = 
  String.join ":" list
  

-- function to concat the other three examples  
getStrings : String
getStrings = 
  concat " first " " second "
  ++ concat_with_String " first " " second "
  ++ colon_join [" first "," second "]
  
```

#TODO: things i struggled with

 - type constructors and dealing with importing/exporting them
 - nested data
 - good dict example with full working examples
 - variable shadowing in let blocks
 - difference in argument order between elixir's |> and elm's
 - product type description and examples
 - union type examples
