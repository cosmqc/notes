- Encapsulate best practice as guidelines / rules of thumb
- Identify common pitfalls, handholding user for invalid inputs
- Simple, easy to use, 'thinking hats'

- Formative - guide design decisions
- Summative - help you evaluate systems

- Keep them in mind, but don't take them as gospel

## Advantages
- Minimalist
	- A few guidelines cover most problems
	- Easily remembered and applied
- Discount usability engineering
	- Cheap and fast
	- Can be done by experts and novices

## Disadvantages
- Very general, lots of overlaps
- Subtleties in application, up to us to think of how and where to apply them
# Nielsen's 10 Heuristics
## Visibility of system status
- Design should always keep users informed about what is happening
- No action with consequence to the user should be taken without feedback
- Via appropriate feedback
	- Error noise for successful operation will confuse
	- Informative, not verbose. Only necessary info and nothing else. Helpful / reassuring.
	- User can only store 7 (+/- 2) items in memory before they start forgetting
- Needs to be within a reasonable amount of time
	- Delayed feedback results in repeated commands, people lose trust in system
	- Response times have an effect on the user
		- 0.1s is the limit for users feeling *they* are the one doing the operation, not the computer
		- 1s is the limit for users feeling they are freely navigating the digital space, feels clunky
		- 10s is usually the limit for the user focusing on a task 
- e.g. 
	- 'You are here' indicator on mall maps
	- Elevator button lights up when you've pushed it / current floor displayed
	- Symbols to show state - battery level, wifi connection
## Match between System and Real World
- Speak the users' language in terms familiar to them
- Follow real-world conventions
- Information should be displayed in a natural and logical order
- Never assume that the developers understanding of words and objects match those of the users
- Shouldn't use similar words for similar concepts, i.e. share and done at end of form
- e.g.
	- Stovetop controls that are in the same size/positions as the heating elements
#### Skeuomorphism
- Objects that mimic real-world counterparts in appearance and interaction
	- e.g. Place to destroy files is a rubbish bin, home menu is a house.
	- Doesn't only have to be icons, a smartwatch itself is skeuomorphic.
- Also applies to how the user feels while interacting, and expectations of the process
	- i.e.
		- Choosing movie on Netflix feels like scanning the shelves of a video store
		- Highlighting passages on PDF matches dragging a highlighter over paper 
## User Control and Freedom
- Users often perform actions by mistake / change their minds
- Need a quick 'emergency exit' to get back without going through an extended process
- Emergency exit should be clearly labelled and discoverable
- Allows a user to exit a flow, undo their previous action, and go back to the system's previous state
- Back, cancel, close, undo options. 'Redo' to support undoing an undo. 
## Consistency and Standards
- The interface should meet user's expectations
- UI should be predictable and learnable
- Internal consistency -> consistent within the product/family of products, all windows apps have minimize, maximize, close in same spot/same order.
- External consistency -> consistent in industry, ctrl c/ctrl v/ctrl x as copy/paste/cut
- Designing against convention adds to user's cognitive load
## Error Prevention
- Best design carefully prevent problems from occuring in the first place
- Either
	- Eliminate error-prone conditions, or
	- Check for error-prone conditions and present with a confirmation option
	- Disabling illegal action
- Enable system restrictions to ensure users cannot do illegal actions
## Recognition rather than Recall
- Make elements visible instead of having users remember it
- Users should not have to remember information of one part of the interface to use another
- Reduce the information users have to remember
## Flexibility and Efficiency of Use
- Shortcuts are hidden from novice users
	- Allows expert user to do actions more efficiently
	- Doesn't overwhelm novice user with lots of things (options/tutorials)
- **Accelerators** - things that aren't necessary but speed up work (keybaord shortcuts, touch gestures)
- **Personalization** - system changes content/functionality to suit the user's needs (frequently used options, fyp)
- **Customization** - user changes the interface/how they interact w it to suit their own needs (moving panes in VSC, change keybinds, rearrange menus)
## Aesthetic and Minimalist Design
- Interfaces should not contain info that is irrelevant or rarely needed
- Every bit of irrelevant info competes with more necessary info in the user's mind
- Reduce short-term memory load
## Help users recognize, diagnose, and recover from errors
- Errors messages should
	- be expressed in plain language (no error codes)
	- precisely indicate the problem (cannot open as Word is not on your device)
	- constructively suggest a solution (reset password text links to reset page), and
	- be presented in a way that helps the user notice and recognize them (red box, highlight field, bold)
## Help and Documentation
- Ensure documentation is easy to search
- Present documentation in context when the user needs it
- List concrete steps that need to happen

# Inspection methods
- 
