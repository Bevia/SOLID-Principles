# SOLID-Principles

Dependecy Inversion

```
import UIKit

// ****** non SOLID --> D = Dependency Inversion  ********
// *********  WITHOUT Dependency Inversion :(   **********

struct LowLevelA{

    func getMyDescription(s : String){
        print("LowLevel A getting --> \(s)")
    }
    
}

struct LowLevelB{
    func getMyDescription(s : String){
        print("LowLevel B getting --> \(s)")
    }
}


struct HighLevel{
    
    ///this is the high-level class, cause is doing something significant
    ///this highLevel struct is dependent on low-level structs!
    ///violates the DI principle from SOLID
    
    let lowLevelA : LowLevelA = LowLevelA()
    let lowLevelB : LowLevelB = LowLevelB()
    
    func getDescription(){
        lowLevelA.getMyDescription(s: "this is form HighLeve struct")
        lowLevelB.getMyDescription(s: "this is form HighLeve struct")
    }
}

let highLevel = HighLevel()
highLevel.getDescription()

//*********    Applying SOLID Principles   **********
//*********  With Dependency Inversion :)  **********
/// DI for Dependency Inversion.

protocol DInversion{
    func getMyDescription(s : String)
}

struct LowLevelA_DI : DInversion{
    func getMyDescription(s: String) {
        print("LowLevel A DI getting --> \(s)")
    }
}

struct LowLevelB_DI : DInversion{
    func getMyDescription(s: String) {
        print("LowLevel B DI getting --> \(s)")
    }
}

struct HighLevelDI{
    
    let delegate:DInversion
    
    ///Now we depend on abstraction, no concrete definitions! HighLevel struct is not coupled to
    ///LowLevel entities any more! we're not dependent on low-level classes, but on abstraction,
    ///on DInversion protocol.
    ///we can add or remove low-level classes without touching the this high-level struct
    
    func getDescription(){
        delegate.getMyDescription(s: "this is form HighLeve DI struct")
    }
}

//who are we delegating to? lowLevelA_DI!
var highleveDI = HighLevelDI(delegate: LowLevelA_DI())
highleveDI.getDescription()

//who are we delegating to? lowLevelB_DI!
highleveDI = HighLevelDI(delegate: LowLevelB_DI())
highleveDI.getDescription()


```
