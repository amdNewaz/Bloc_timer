
![flutter_timer](https://user-images.githubusercontent.com/77064568/130818685-ea7c89d1-9d73-4c6a-a4bc-786fdf9e031f.gif)


Key Topics
Observe state changes with BlocObserver.
BlocProvider, Flutter widget which provides a bloc to its children.
BlocBuilder, Flutter widget that handles building the widget in response to new states.
Prevent unnecessary rebuilds with Equatable.
Learn to use StreamSubscription in a Bloc.
Prevent unnecessary rebuilds with buildWhen.

Timer Bloc
TimerState
We’ll start off by defining the TimerStates which our TimerBloc can be in.

Our TimerBloc state can be one of the following:

TimerInitial — ready to start counting down from the specified duration.
TimerRunInProgress — actively counting down from the specified duration.
TimerRunPause — paused at some remaining duration.
TimerRunComplete — completed with a remaining duration of 0.
Each of these states will have an implication on the user interface and actions that the user can perform. For example:

if the state is TimerInitial the user will be able to start the timer.
if the state is TimerRunInProgress the user will be able to pause and reset the timer as well as see the remaining duration.
if the state is TimerRunPause the user will be able to resume the timer and reset the timer.
if the state is TimerRunComplete the user will be able to reset the timer.
In order to keep all of our bloc files together, let’s create a bloc directory with bloc/timer_state.dart.

Note that all of the TimerStates extend the abstract base class TimerState which has a duration property. This is because no matter what state our TimerBloc is in, we want to know how much time is remaining. Additionally, TimerState extends Equatable to optimize our code by ensuring that our app does not trigger rebuilds if the same state occurs.

Next up, let’s define and implement the TimerEvents which our TimerBloc will be processing.

TimerEvent
Our TimerBloc will need to know how to process the following events:

TimerStarted — informs the TimerBloc that the timer should be started.
TimerPaused — informs the TimerBloc that the timer should be paused.
TimerResumed — informs the TimerBloc that the timer should be resumed.
TimerReset — informs the TimerBloc that the timer should be reset to the original state.
TimerTicked — informs the TimerBloc that a tick has occurred and that it needs to update its state accordingly.
If you didn’t use the IntelliJ or VSCode extensions, then create bloc/timer_event.dart and let’s implement those events.
