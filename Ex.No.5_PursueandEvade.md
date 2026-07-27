# Ex.No: 5  Implementation of Steering behaviour-Pursue and Evade in Unity
### DATE:27.07.2026                                                                            
### REGISTER NUMBER :212224223002 
### AIM: 
To write a program to simulate the process of Pursue and Evade behavior in Unity using NavigationMeshAgent. 
### Algorithm:
```
1. Create a New Unity Project by Open the  Unity Hub and create a new 3D Project.
2. Name the project "SteeringBehaviors" and select a location. Click Create.
3.Open Unity Scene (default is SampleScene).
  In the Hierarchy, create a Plane:
  Right-click → 3D Object → Plane (this will be the ground).
  Set its Scale to (10, 1, 10) for a larger surface.
  Create three Capsule for the Player, Pursuer, and Evader:
  Rename them to "Player", "Pursuer", and "Evader".
  Set their Y Position to 0.5 (so they sit on the ground).
  Change their Material for better distinction (optional).
3. Check AI navigation in window.
 Window → AI → Navigation (opens the Navigation tab).  If it is not available then add package by name "com.unity.ai.navigation"
4. Select the Plane, go to the Navigation tab, and mark it as Navigation Static.
   Go to the Bake tab and click Bake.
   or
   Add navMeshSurface to plane and bake 
4. Add NavMeshAgent Component 
    Select Pursuer, and Evader.
    Click Add Component → Search for NavMeshAgent and add it.
    Adjust NavMeshAgent Settings:
    Player: Set Speed = 5.
    Pursuer: Set Speed = 4.
    Evader: Set Speed = 6.
5. Write a script for  Player_movement behavior and save it

using UnityEngine;

public class player : MonoBehaviour
{
    // Start is called before the first frame update
    public float speed;
    void Start()
    {
        float xdir = Input.GetAxis("Horizontal") * speed;
        float zdir = Input.GetAxis("Vertical") * speed;
        transform.position = new Vector3(xdir, zdir);
    }

    // Update is called once per frame
    void Update()
    {

    }
}
**Evader script**
using UnityEngine;
using UnityEngine.AI;

[RequireComponent(typeof(NavMeshAgent))]
public class Evader : MonoBehaviour
{
    // Start is called before the first frame update
    public NavMeshAgent agent;
    public Transform target;
    public float evadespeed;
    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
    }

    void Evade()
    {
        Vector3 fleedir = transform.position - target.position;
        Vector3 evadeposition = transform.position + fleedir.normalized * evadespeed;
        agent.SetDestination(evadeposition);

    }
    // Update is called once per frame
    void Update()
    {
        Evade();
    }
}
**Pursuer script**
using UnityEngine;
using UnityEngine.AI;

[RequireComponent(typeof(NavMeshAgent))]
public class Pursuer : MonoBehaviour
{
    // Start is called before the first frame update
    public NavMeshAgent agent;
    public Transform target;
    public float speed;
    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
    }
    // Update is called once per frame
    void Pursue()
    {
        Vector3 targetvelocity = target.position - transform.position;
        Vector3 futurepos = transform.position + targetvelocity.normalized * speed;
        agent.SetDestination(futurepos);
    }
    // Update is called once per frame
    void Update()
    {
        Pursue();
    }
}

7. Attach the Script to each player,pursuer and Evader.
   Drag & Drop the Target from the Hierarchy into the "Target" field in the script component ( For pursuer and Evader).
12. Run the game 
13. Stop the program
    
```
### Output:
<img width="1917" height="1197" alt="image" src="https://github.com/user-attachments/assets/fa9f8e4a-f3ce-4b24-960e-043846d30734" />
<img width="1917" height="1198" alt="image" src="https://github.com/user-attachments/assets/ab8df944-a5c6-4803-9760-c4cd6c132188" />





### Result:
Thus the simple pursue and evade behavior was implemented successfully.
