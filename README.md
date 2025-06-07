# EXP-8-BACKWARD-CHAINING
# Knowledge base (facts and rules)
facts = {'rain', 'have_umbrella'}

rules = [
    {'if': ['rain', 'have_umbrella'], 'then': 'go_outside'},
    {'if': ['weekend'], 'then': 'relax'},
    {'if': ['exam'], 'then': 'study'},
]

# Backward chaining function
def backward_chain(goal, facts, rules, depth=0):
    indent = "  " * depth
    print(f"{indent}Trying to prove: {goal}")

   if goal in facts:
        print(f"{indent}✓ Found in facts.")
        return True

   for rule in rules:
        if rule['then'] == goal:
            print(f"{indent}Using rule: IF {rule['if']} THEN {goal}")
            if all(backward_chain(subgoal, facts, rules, depth+1) for subgoal in rule['if']):
                facts.add(goal)  # Memorize proven goal
                return True

   print(f"{indent}✗ Cannot prove: {goal}")
    return False

