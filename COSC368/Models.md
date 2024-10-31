#### What is a model?
- Simplification/representation of reality
- Helps improve user performance and experience by comparing model outputs
- Descriptive Models vs Predictive Models
	- Descriptive models are
		- Used to help understand *how* a user will interact with an interface
		- Help us understand what is going on between the user and the system
		- Address the translation between the user's wants and what the system does
		- Help inform and improve the designs of the actual interfaces

#### Shannon's theorem
- Maximum amount of information that can be sent over a medium
- Distance = Amplitude (A) of moment; distance from cursor to center of target
- Width = Noise / Width of target 
- ID = Distance / Width

#### Fitts' Law (predictive)
- The time to acquire a target
- A function of the distance to and the size of the target
- Assesses human performance in pointing tasks
- MT = a + b * log2(D/W + 1)

- a roughly represents targeting preparation time
- b roughly represents the rate of information processing
- throughput = 1/b
  - a measure of how many units of information a system can process in a given amount of time
  - Low throughput means pointing times increase rapidly with ID
  - High throughput means they increase slowly with ID
 
#### Hick's Law (predictive)
- The time is takes to make a decision
- Increases with the number and complexity of choices
- DT = a + b * log2(n)
- n -> number of choices

Takeaways:
- Minimize choices when response times are critical (nuclear shutdown)
- Breakdown complex tasks into smaller steps to decrease cognitive load
- Avoid overwhelming users by highlighting recommended options / removing invalid options
- Use progressive onboarding (new users get few options, experts get many options)
- Don't simplify to the point of abstraction ("Everything should be made as simple as possible, but not simpler") 

#### Miller's Law (predictive)
- The average person can only keep 7 (+/- 2) items in their working memory
- Cognitive load is the amount of information that we can hold in working memory

Takeaways:
- Don't use 7 to justify unnecessary design limitations
- Organize content into smaller chunks to help users
- Short-term memory varies per pereson based on context and prior exp

#### Steering Law
- Describes the time required to navigate through a 2-dimensional tunnel
- MT = a + b * (Tunnel length / Tunnel width)
![Examples of steering law, shows various sliders](/images/image-4.png)

#### Norman's Executive Evaluation Cycle
- Cycle divided into two phases: execution and evaluation.
- Execution (User -> System).
  - Establishing goal (free up my email inbox)
  - Forming intention (i will delete junk emails)
  - Specifying action sequence (select emails I want to delete)
  - Executing action (click select box on emails, then delete button)
- Evaluation (System -> User)
  - Perceiving system state (I see a notification pop up)
  - Interpreting system state (Notification says emails were moved to trash)
  - Evaluating system state (Fewer emails in inbox)

#### UISO Interaction Framework
- Extended version of Norman's model to take the system into account

- User, Input, System, Output

Execution phase:
- Each step has its own lanuage
- User formulates a goal + task to achieve the goal. Task must be articulated in Input lanuage
- Input is translated into core language
- System then transforms itself described by the operations

Evaluation phase:
- System is in a new state, which must be communicated to the User via Output.
- Values of system attributes are rendered as concepts or features of the Output then observed by User

![UISO Model](image.png)

#### Direct manipulation
- Interaction style where objects of interest are
	- visible
	- can be acted upon via physical, reversible, incremental actions
- Actions should receive immediate feedback
- A central concept of GUIs
- Helps users use the interface with minimal learning

Principles:
- Visibility of objects
	- Continuous representation of the object of interest, visibility of system state / objects
- Physical actions instead of complex syntax
	- Actions are invoked physically via clicks, button presses, and touch gestures
- Continuous rapid feedback & reversible, incremental actions
	- Easy to validate that each action caused the right result
	- Actions build on each other
- Rapid learning
	- Don't have to learn and remember syntax

Advantages:
- Easy to learn
- Low memory requirements
- Easy to undo
- Immediate feedback on user actions

Disadvantages:
- Consumes a lot of screen real estate
- May trap user in 'beginner mode'
- Repetitive physical actions -> carpal action
- Accessibility may suffer (motor/visually impaired)

#### Over/Under-Determined Dialogues
Well-determined -> natural translation from task to input language

Under-determined -> User knows what they want to do, but not how to do it. Happens via over-simplifying or abstraction (i.e. cmdline)

Over-determined -> User forced through unnecessary steps ('Click OK to proceed')
#### Mapping
- Tieing buttons/actions to expected outcomes.
- Good mappings between User and Interface increase usability
  - Dials for stove top
  - Light switches are closer to the light they turn on
#### Affordance
> The perception of what actions are possible 

- The quality of an object to tell us how it wants to be used and to help us use it
  - Buttons -> pushing
  - Chairs -> sitting
  - Sliders -> sliding
  - Dials -> turning
  - Handles -> pulling
#### Signifiers
> Specify how users discover affordances
Cactus
- Signifier -> sharp and pointy
- Affordance -> don't touch

Smooth leafs
- Signifier -> round, smooth
- Affordance -> can touch

Poisonous frog
- Signifier -> neon colors
- Affordance -> poisonous

Disabled menu
- Signifier -> Greyed out options
- Affordance -> disabled, cannot click