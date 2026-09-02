# ExpNo:10 Implementation of Classical Planning Algorithm
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Program:
```
from collections import deque

def find_plan(initial_state, goal_state, actions):
    # Queue stores tuples of (current_state, path_taken)
    queue = deque([(initial_state, [])])
    visited = []

    def is_goal(state):
        return all(state.get(k) == v for k, v in goal_state.items())

    def satisfies_preconditions(state, preconditions):
        return all(state.get(k) == v for k, v in preconditions.items())

    def apply_action(state, effect):
        new_state = state.copy()
        new_state.update(effect)
        return new_state

    while queue:
        current_state, path = queue.popleft()

        if is_goal(current_state):
            return path

        if current_state in visited:
            continue
        visited.append(current_state)

        for action_name, action_data in actions.items():
            preconditions = action_data['precondition']
            effect = action_data['effect']

            if satisfies_preconditions(current_state, preconditions):
                next_state = apply_action(current_state, effect)
                queue.append((next_state, path + [action_name]))

    return None

# --- Example 1 Test ---
initial_state_1 = {'A': 'Table', 'B': 'Table'}
goal_state_1 = {'A': 'B', 'B': 'Table'}

actions_1 = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan_1 = find_plan(initial_state_1, goal_state_1, actions_1)
print("Example 1 Output:", plan_1)

# --- Example 2 Test ---
initial_state_2 = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state_2 = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions_2 = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan_2 = find_plan(initial_state_2, goal_state_2, actions_2)
print("Example 2 Output:", plan_2)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']

![Uploading image.png…]()

```

# Please Prepare Solution or Definition For the method find_plan(initial_state, goal_state, actions)
<h3>You Can use any of the searching Strategies for planning and executing a sequence of actions.<br> You can also look in to the Code given in the Repository.</h3>
