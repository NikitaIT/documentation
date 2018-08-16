# Interfaces

Interfaces are meant for interacting with data from a dataset. You define an interface to control precisely which data is presented to which users. You have to declare each interface individually.

Each interface has a _name_ that is unique for every interface in the same context.

When running an application in your browser, you are watching one user-interface at any given moment in time. Each hyperlink on your screen represents an atom to which some interface applies. To navigate to that user-interface, just click on the hyperlink. You will see the interface being applied solely to the atom you just clicked. To determine the atom\(s\) to which an interface applies, each interface has an _interface expression_.

Note: The interface definition must be outside a pattern

## Example

The following figure is an example of a user interface, which shows the name, status, e-mail and co-workers of a person called "J. Lovell".

![Example of a user interface](https://github.com/AmpersandTarski/documentation/blob/master/Figures/InterfaceLovellRaw.jpg?raw=true)

The specification of this interface is given in the following code fragment

```text
INTERFACE Person : I[Person]
BOX
  [ "Name"       : personName
  , "Status"     : personStatus
  , "Email"      : personEmail
  , "Works with" : workswith 
  ]
```

To understand this fragment, take notice of:

1. The name of this interface is `Person`. This name immediately follows the keyword `INTERFACE`.
2. The expression following the colon, `I[Person]`, is the interface expression of this interface.
3. The interface can be applied to any atom from the _domain of the interface expression_. So this particular interface is applicable to any atom of type `Person`. In the screenshot, it applies to `"J. Lovell"`.
4. The labels "Name", "Status", "Email", and "Works with" correspond to field names in the user interface.  
5. Each expression at the right of a field name specifies which data is presented in the field. For this reason it is called the _field expression_ for that field. Field name and field expression are separated by a colon.
6. Of all pairs `<"J. Lovell", x>` from the field expression, the field displays the right atom `x`. A field expression always works on one specific atom on the left, which is `"J. Lovell"` in this example.
7. Field expressions are subject to type checking. The following relations provide an example for getting a type-correct interface:

   ```text
   RELATION personName :: Person * PersonName [UNI]
   RELATION personStatus :: Person * PersonStatus [UNI]
   RELATION personEmail :: Person * Email [UNI,TOT]
   RELATION workswith :: Person * Person
   ```

   The source concepts of a field expression must match the target concept of the interface expression.

8. Looking at the screenshot, we can tell that `"J. Lovell"` has one personName \(which is `"J. Lovell"`\), it has no personStatus, one personEmail and three persons to work with in `RELATION workswith`.

## Nesting

You can create structure in an interface by nesting. Here is an example:

![Example of a nested user interface](https://github.com/AmpersandTarski/documentation/blob/master/Figures/InterfaceAlphaBoardNested.jpg?raw=true)

The specification of this interface is given in the following code fragment.

```text
INTERFACE "Project"  : I[Project] BOX
  [ "Project"     : I[Project]
  , "Name"        : projectName
  , "Current PL"  : pl
  , "Administration" : I[Project] BOX
     [ "Project leaders" : project~;assignee/\pl BOX
        [ "Name"      : personName
        , "Status"    : personStatus
        , "Email"     : personEmail
        ]
     , "Project members" : project~;assignee/\member BOX
        [ "Name"      : personName
        , "Status"    : personStatus
        , "Email"     : personEmail
        ]
     ]
  ]
```

Notice the following features:  
1. The structure of an interface is hierarchical. It consists of boxes within a box. This is because a field expression may be followed by a `BOX` with a list of subinterfaces. Without it, it is just a field expression. 2. When a field expression is followed by a `BOX`, every atom in the _codomain of the field expression_ is displayed in a box of its own on the screen. That box behaves like an interface with the field expression serving as interface expression of that subinterface. 3. By this mechanism, the hierarchical structure of the entire interface translates directly to the hierarchical structure of the web-page in which it is displayed. 4. The source concept of a field expression must match with the target concept of the field expression outside the box.  
5. The target concept of a field expression that has a box, must match with the source concepts of each field inside that box.

## Formatting

Especially in more complicated interfaces, you will find it nice to adapt the layout of the fields of your interface. For this purpose, you can substitute the word `BOX` by `COLS`, `ROWS`, or `TABS`, as in the following code fragment.

```text
INTERFACE "Project"  : V[SESSION*Project] ROWS
  [ "Project"     : I[Project]
  , "Name"        : projectName
  , "Current PL"  : pl
  , "Administration" : I[Project] TABS
     [ "Project leaders" : project~;assignee/\pl COLS
        [ "Name"      : personName
        , "Status"    : personStatus
        , "Email"     : personEmail
        ]
     , "Project members" : project~;assignee/\member COLS
        [ "Name"      : personName
        , "Status"    : personStatus
        , "Email"     : personEmail
        ]
     ]
  ]
```

Notice the effect that these changes have on the user interface.

![Example of formatting by COLS, ROWS, or TABS](https://github.com/AmpersandTarski/documentation/blob/master/Figures/InterfaceAlphaBoardFormatted.jpg?raw=true)

Notice the following features:  
1. The keyword `TABS` turns the box into a tabulated layout.  
2. The keyword `COLS` turns the layout 90 degrees into columns.  
3. The keyword `ROWS` is default for any box. It does not change the effect of `BOX`.

## Assignment

Compile and run the script [Project Administration Example](https://github.com/AmpersandTarski/ampersand-models/tree/master/Examples/ProjectAdministration). Start by reproducing everything that is shown above. It is quite likely that you will be trying out your own ideas before you get to the end... Have fun!

## What have you learned?

After finishing your assignment, you have learned:

* to explain how an interface definition is displayed on the screen of a user.
* to predict which data items an interface applies to, if you know which pairs are in an interface expression.
* to predict which data items are displayed, if you know which pairs are in a field expression.
* to explain which atoms are used in a sub-interface.
* to understand what the keywords `TABS`, `COLS`, and `ROWS` do to your display.

 More than one interfaces may apply to the same atom. That gives you a choice on runtime to which interface you want to navigate. If no interface applies, that atom is not navigable.
