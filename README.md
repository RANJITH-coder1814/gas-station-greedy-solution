# ⛽ Gas Station (LeetCode 134)

## 🧩 Problem Statement
There are `n` gas stations arranged in a circular route.

- `gas[i]` = amount of gas at station `i`
- `cost[i]` = gas required to travel from station `i` to `(i + 1)`

You start with an empty tank and can begin at any station.

👉 Return the starting station index if you can travel around the circuit once, otherwise return `-1`.

---

## 💡 Approach (Greedy)

### Key Observations:
- If total gas < total cost → ❌ impossible
- If solution exists → ✅ it is unique
- Reset starting point when tank becomes negative

---

## 🚀 Algorithm
1. Traverse all stations
2. Maintain:
   - `total` → total gas balance
   - `tank` → current gas
   - `start` → candidate index
3. If `tank < 0`:
   - Set `start = i + 1`
   - Reset `tank = 0`
4. Final check:
   - If `total >= 0` → return `start`
   - Else return `-1`

---

## 🧑‍💻 Code (C++)

```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int total = 0, tank = 0, start = 0;

        for (int i = 0; i < gas.size(); i++) {
            int diff = gas[i] - cost[i];
            total += diff;
            tank += diff;

            if (tank < 0) {
                start = i + 1;
                tank = 0;
            }
        }

        return total >= 0 ? start : -1;
    }
};
