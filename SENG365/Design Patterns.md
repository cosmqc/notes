#SENG365
**Design patterns** are to simplify problems and solutions in software using separation of concerns: separating code into distinct sections so each section addresses specific concerns. Examples of separation of concerns:
- Object-oriented programming (classes, objects, methods)
- Web computing
	- HTML (structure/organisation of content)
	- CSS (styling)
	- JS (functionality)

An example:
> We want to display data to the user in different ways (i.e. bar chart, table, pie graph, etc.)
> We want to keep our data independant of the way it is being displayed
> We may also want to compute extra values depending on what display we're using

We need some connection (**bridge**) between the views and data.
We can reuse both the views and data, but need different bridges for each scenario.

## MVC (Model - View - Controller)
### Pros
- Multiple views
- Synchronized views
- Pluggable views and controllers
- Exchangeable look and feel
### Cons
- Complexity
- Can have lots of updates / notifications
- Links between controller and view
- Coupling of model to controller/view
- Mix of platform-dependant/independant code in controller/view


![[Pasted image 20240610201329.png]]

## MVP (Model - View - Presenter)
Pure MVP has no interaction between the model and view, but in practise it ranges between this, MVC, and whatevers in the middle.

![[Pasted image 20240610201719.png]]
## MVVM (Model - View - ViewModel)
- ViewModel is just the data currently required by the view
- Use data binding to link the data shown (or changed by the user) on the view to the viewmodel.
- ViewModel and View are stored on the client, Model is stored on the server

![[Pasted image 20240610204238.png]]

## MV* (Model - View - Whatever)
¯\\_(ツ)_/¯


