# Finite-State-Machine
A simple state machine write in c# that allow you to easily create transition rules between states.
A finite-state machine is a model used to represent and control execution flow. It is perfect for implementing AI in games, producing great results without a complex code.

# Usage
To use the state machine you need to follow a few simple steps
##### Create an enum
In your derived class or whatever you prefer, you can declare you enum, which will represent the state of the state machine:
```javascript
public enum YourEnum
{
	Idle,
	Run,
	Jump
}
```
##### Your monobehivour should inherit from BaseFSM
Remeber to specify the Enum that your ChildFSM should handle:
```javascript
public class ChildFSM : BaseFSM<YourEnum> 
{

}
```

##### Initialize the State Machine
Inside the ChildFSM constructor you have to define the states transition and the initial state machine state:
```javascript
public ChildFSM () : base()
{			
	this.currentState = YourEnum.Idle;
	//Define the state machine transitions
	this.transitions = new Dictionary<StateTransition, YourEnum>
	{
		{ new StateTransition(YourEnum.Idle, YourEnum.Run), YourEnum.Run }, 
		{ new StateTransition(YourEnum.Run, YourEnum.Jump), YourEnum.Jump }, 
	};	
}
```

Where:
```javascript
	{ new StateTransition(YourEnum.Idle, YourEnum.Run), YourEnum.Run }
```
Define the state transition. 
You can see it like:
```javascript
{ new StateTransition(actual state, transition state), final state}
```

##### Usage
For a correct use of the state machine you have to create an instance of your child state machine:
```javascript
ChildFSM fsm = new ChildFSM()
```
Example:
```javascript
public class Program
	{
		static void Main(string[] args)
		{
			ChildFSM fsm = new ChildFSM();
			Console.WriteLine("Current State = " + fsm.currentState);
			//MoveNext used to change the state
			Console.WriteLine("Command.Begin: Current State = " + fsm.MoveNext(PlayerState.Run));
			//CanReachNext used to check if the next state it's reachable
			Console.WriteLine("Invalid transition: " + fsm.CanReachNext(PlayerState.Idle));
			Console.WriteLine("Previous State = " + fsm.previusState);
		}
	}
```
# License
MIT License

# Contact
If you liked the library or you have any suggestions these are my contacts:

1.[Twitter](https://twitter.com/Marcomignano3) 

2.Mail: marco.mignano89 at gmail.com

3.[WebSite](http://marcomignano.com)  

If these was helpfull a simple add on Twitter will be a nice thanks.
# Credits:
It is inspired by the state machine found at: http://stackoverflow.com/questions/5923767/simple-state-machine-example-in-c
