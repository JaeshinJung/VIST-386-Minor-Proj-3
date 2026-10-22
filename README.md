# VIST 386 Minor Project 3: Red Kingdom Pawn (Unity Behavior Proof)

Individual Unity Behavior proof for the **Pawn** unit of the Red Kingdom faction (Alice Factions, Behavior, and Counterplay).

- **Unity:** 6000.3.26f1 (Unity 6.3 LTS, Universal 3D / URP)
- **Unity Behavior:** com.unity.behavior 1.0.16
- **Base:** "Unity Behavior Example" sample imported through the Package Manager (not the deprecated Asset Store demo)

## How to run
1. Open the project folder in Unity Hub with editor 6000.3.26f1.
2. Open `Assets/Samples/Behavior/1.0.16/Unity Behavior Example/SampleScene.unity`.
3. Press **Play**. Select **Agent** in the Hierarchy.
4. In the Inspector, under **Behavior Agent > Example Behavior Graph Blackboard**, change **PlayerDistance**:
   - `0` (below 3) -> **Jab** branch: the Pawn says "JAB! (close range, moving attack)" and holds for 1 s.
   - `10` (3 or more) -> **Braced Thrust** branch: the Pawn says "BRACE + THRUST! (far range)", picks a target and navigates to it.
5. To see the live path, open `Example Behavior Graph.asset`, click **Debug**, and choose **Agent**.

## Behavior Graph
`Assets/Samples/Behavior/1.0.16/Unity Behavior Example/Example Behavior Graph.asset`

```
On Start (Repeat)
 └─ Self says "What should I do?"
     └─ Branch On: PlayerDistance < 3        <- condition
         ├─ True  -> Self says "JAB! ..."             (outcome 1: moving jab)
         │           Wait 1 s
         └─ False -> Self says "BRACE + THRUST! ..."   (outcome 2: braced thrust)
                     Set Random Target from tag "Targets"
                     Target says "Pick Me! Pick Me!"
                     Self navigates to Target
```

**Blackboard variables:** Self (GameObject), Target (GameObject), Speed (float), **PlayerDistance** (float, exposed), **IsBraced** (bool, exposed; reserved for the braced state in the full design).

Requirements check: 1 condition (Branch On), 2+ actions/outcomes (Jab / Braced Thrust), 2+ Blackboard variables (PlayerDistance, IsBraced, plus Self/Target/Speed).
