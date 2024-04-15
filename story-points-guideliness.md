# Story Points Guideliness

Story points measure the effort needed to implement a task, focusing on complexity rather than time.

## Why it is useful

1. **Efficient Workload Management**: Knowing how much one should work efficiently. Story points allow team members to understand and manage their workload better, leading to more efficient, relaxing, and focused work.
2. **Realistic Commitments with Product**: Making promises to the product based on realistic estimations. This helps in setting achievable goals and delivering consistent value.
3. **Relaxed and Agile Work Environment**: Creating a more relaxed and agile work atmosphere. Since story points focus on relative effort rather than time, it reduces stress and allows for a more flexible and adaptive work approach.
4. **Improved Task Prioritization**: Better prioritizing tasks. By understanding the complexity and effort involved, teams can make more informed decisions about what to work on first, ensuring that the most critical tasks are addressed promptly.

## Fibonacci Sequence

The Fibonacci sequence (1, 2, 3, 5, 8, 13, ...) is often used for assigning story points. This sequence is preferred because:

- **Complexity Representation**: The Fibonacci sequence (1, 2, 3, 5, 8, 13, ...) mirrors the non-linear increase in task complexity, making it ideal for estimating larger, more complex tasks.
- **Discouraging Minute Precision**: The sequence's increasing gaps prevent overly precise estimations, encouraging a focus on general effort rather than exact time. The difference between 8 and 13 is more significant than between 8 and 9, which discourages unnecessary precision in the estimation.
- **Ease of Use**: Its straightforward progression simplifies the estimation process, especially helpful for new team members.

# **Guidelines for Estimating Efforts**

**A good heuristic is to follow the following equation**

$$
Effort=Code Interaction+Uncertainty+Implementation Difficulty+Testing Difficulty+Quality Expectation+Documentation Difficulty
$$

**Where**

- **Code Interaction**: The extent of interaction with other parts of the code.
- **Uncertainty**: The level of uncertainty or unpredictability associated with the task.
- **Implementation Difficulty**: The complexity involved in implementing the solution.
- **Testing Difficulty**: The effort required to thoroughly test the implementation.
- **Quality Expectation**: The required quality level, is often higher for core business features.
- **Documentation Difficulty**: The effort needed to document the implementation and its functionalities.

I**mportant Note**: This equation does not measure time. Each component reflects the complexity, risk, and effort involved, rather than a time-based estimate. Story points focus on the relative difficulty of tasks, not how long they will take.

# **Poker Planning**

- **Collaborative Estimation**: Engage the entire team in the estimation process (e.g., [Planning Poker](https://planningpokeronline.com/new-game/)) to leverage diverse perspectives.
- **Consensus**: Strive for a common understanding and agreement on point allocation.

# Others

## **Estimating Bugs**

Bugs can be tricky and vary in complexity. They often require extra investigation to fully understand. To avoid underestimating, it's safer to overestimate their complexity as they tend to scale unpredictably. In complex cases, consider splitting the task: first, investigate the bug, then tackle the fix as a separate task. This method helps in providing a more accurate and less stressful estimate.

## **Estimating Spikes**

Spikes are used to research a problem or explore a solution. They differ from regular tasks as they aim to gather information, not deliver features. For spikes, avoid using effort or story points for estimation. Instead, time-box them, typically in days, to keep them focused and efficient.

# Personal Insights

The previous information focused on an agnostic framework. Now, I'd like to share some personal insights. Please take these with a grain of salt, as what works for some teams may not necessarily work for others.

- **One-Point Tasks:** For one-point tasks only, you can estimate them to be 3 to 5 hours. This ensures if something goes wrong, the task is still contained within a day. Remember: A programmer isn't just coding—they're also handling PR reviews, attending meetings, and writing documentation.

- **Competitive Underestimation:** When one developer claims a task is easy, others might stay silent to avoid looking less capable. Avoid this.

- **Team Completion:** The best predictor of meeting sprint goals is the length of time a team has worked together. Consider how long a team has been together. New teams might struggle more with completing tasks—it's a normal part of team growth. If the percentage of completion is less than  65% the problem has nothing to do with the devs but the amount of work they have. 

- **Consitency is Everything:** Trust is hard to get and easy to loose. Failing to meet goals is worse than "underperforming". Is better to overestimate than underestimate. Just don't go crazy overestimating everything. That's just stupid. 
