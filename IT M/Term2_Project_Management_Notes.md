# Term 2: Project Management Notes

## 1. Network Diagram
- **Definition**: A graphical tool showing project activities and their dependencies, read left to right or top to bottom, with boxes representing activities.
- **Purpose**:
  - Enhances visibility and control over the project schedule.
  - Identifies total project duration and critical path (longest duration path).
  - Addresses complex activity interactions.
- **Examples**:
  ![Image Example](https://www.wrike.com/tp/storage/uploads/993b47cd-88b4-4dee-8a0a-b13445593700/project-schedule-network-diagram.jpg)
  - Basic network diagram layout.
  - Shows activity durations (e.g., Path A: 1-2-4-7 = 90 days).
  - Displays start/end dates for a software project.

## 2. Critical Path
- **Definition**: The longest path in the network diagram, setting the shortest possible project completion time.
  - Delays in critical path activities delay the entire project unless offset later.
  - Not the shortest path or the path with the most critical activities.
  - Multiple critical paths with the same duration are possible.
- **Procedure to Find Critical Path**:
  1. Draw the network diagram.
  2. List all possible paths.
  3. Sum the duration of each path.
  4. The path with the longest duration is the critical path.
- **Example**:
![Figure B](https://pmstudycircle.com/wp-content/uploads/2022/10/critical-path-method-cpm-diagram.webp)
  - Path A: 10-12-9 = 31 days (Critical Path).
  - Path B: 5-12-9 = 26 days.
  - Path C: 5-7-6 = 18 days.
  - Path D: 3-7-6 = 18 days.
  - Path E: 3-4-6 = 13 days.
- **Exercise (Table 1)**:
  - **Activities and Durations**:
    - A: 12 days (no predecessors).
    - B: 6 days (no predecessors).
    - C: 13 days (predecessor: A).
    - D: 12 days (predecessors: A, B).
    - E: 11 days (predecessors: C, D).
    - F: 13 days (predecessor: D).
    - G: 11 days (predecessors: E, F).
  - **Tasks**:
    - Construct network diagram.
    - Calculate project completion time.
    - Identify activities critical to timely completion.

## 3. Slack and Float
- **Definition**:
  - **Slack/Float**: Excess time/resources for a task without delaying subsequent tasks (free float) or the project (total float).
    - **Positive Slack**: Ahead of schedule.
    - **Negative Slack**: Behind schedule.
    - **Zero Slack**: On schedule.
  - **Slack**: Refers to delays in starting an activity.
  - **Float**: Refers to extra time to complete an activity.
- **Calculation**:
![Figure B](https://pmstudycircle.com/wp-content/uploads/2022/10/critical-path-method-cpm-diagram.webp)
  - Slack = Critical path duration - Path duration.
  - Critical path activities have zero float.
  - Example: Path A-B-C (31 days, critical), Path D-E-F (18 days, float = 31-18 = 13 days).
- **Critical Activity**: An activity with zero float (not necessarily on the critical path).

## 4. Critical Path Method (CPM)
- **Definition**: A technique to plan processes by identifying critical and non-critical tasks to avoid delays and bottlenecks.
- **Components**:
  1. List all activities (from Work Breakdown Structure).
  2. Estimate durations.
  3. Define dependencies.
  4. Identify milestones/deliverables.
- **Process**:
  - Build network diagram.
  - Calculate path durations.
  - Identify critical path (longest duration or shortest completion time).
- **Example**:
![Figure B](https://pmstudycircle.com/wp-content/uploads/2022/10/critical-path-method-cpm-diagram.webp)
  - Paths: Activity 3-4-6 (13 days), Activity 10-12-9 ( 31 days, critical), Activity 5-7-6 (9 days).
- **Benefits**:
  - Visualizes timeline and dependencies.
  - Supports planning, scheduling, and control.
  - Enables contingency planning and float allocation.
  - Highlights critical activities.
  - Allows critical path shortening via:
    - **Pruning**: Trimming activities.
    - **Fast-Tracking**: Performing tasks in parallel.
    - **Crashing**: Adding resources to shorten durations.
- **Limitations**:
  - Assumes unlimited resources.
  - Ignores resource dependencies.
  - Risks float misuse.
  - May neglect non-critical activities.
  - Projects may miss approved timelines.

## 5. Early Start (ES) and Early Finish (EF)
- **Forward Pass**:
  - **ES** = Early Finish of predecessor + 1 (first activity ES = 1).
  - **EF** = ES + Duration - 1.
  - ![Figure C](https://plaky.com/learn/wp-content/uploads/2025/03/Activity-Node-1.png)
- **Example (Path A-B-C)**:
  - A: ES = 1, EF = 1 + 10 - 1 = 10.
  - B: ES = 10 + 1 = 11, EF = 11 + 12 - 1 = 22.
  - C: ES = 22 + 1 = 23, EF = 23 + 9 - 1 = 31.
- **Multiple Predecessors**:
  - Use predecessor with the greater EF (e.g., E uses D’s EF=5 over G’s EF=3).

## 6. Late Start (LS) and Late Finish (LF)
- **Backward Pass**:
- ![Figure B](https://pmstudycircle.com/wp-content/uploads/2022/10/critical-path-method-cpm-diagram.webp)
  - **LS** = LF - Duration + 1.
  - **LF** = LS of successor - 1.
  - LF of last activity = EF of critical path’s last activity (e.g., 31).
- **Example (Path A-B-C)**:
  - C: LF = 31, LS = 31 - 9 + 1 = 23.
  - B: LF = 23 - 1 = 22, LS = 22 - 12 + 1 = 11.
  - A: LF = 22 - 1 = 21, LS = 21 - 10 + 1 = 12.
  - ![Image Ex1](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750104141/wcksfybpqhuwzuehmvnc.png)
  - ![Image Ex2](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750104185/ajhxm7rjdnwn3iam1zah.png)
  - ![Image Ex3](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750104248/zfr3f2chxg5le5g8szom.png)
  - ![Image Ex4](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750104299/mnwka4t9tqdty92yhquc.png)
  - ![Image Ex5](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750104359/cg2f5mvgolkcodqzfj5k.png)
  - ![Image Ex6](https://res.cloudinary.com/ddsojj7zo/image/upload/v1750104435/ygv85vkmz63dgyyt7tjl.png)
- **Multiple Successors**:
  - Use successor with the earlier LS (e.g., D uses B’s LS=11 over E’s LS=19).
- **Critical Path**: ES = LS and EF = LF.

## 7. Program Evaluation Review Technique (PERT)
- **Definition**: A tool for estimating project duration under uncertainty, using three time estimates per activity.
- **Time Estimates**:
  - **Optimistic (o)**: Shortest time (best case).
  - **Most Likely (m)**: Normal time.
  - **Pessimistic (p)**: Longest time (worst case).
  - **Expected Time (te)**: te = (o + 4m + p) ÷ 6.
- **Steps**:
  1. Identify activities and milestones.
  2. Sequence activities.
  3. Construct network diagram.
  4. Estimate times (o, m, p).
  5. Determine critical path and slacks.
  6. Update chart as project progresses.
- **Example**:
![Figure](https://upload.wikimedia.org/wikipedia/commons/thumb/3/37/Pert_chart_colored.svg/1200px-Pert_chart_colored.svg.png)
  - Activity A: o=2, m=4, p=6, te=(2+4*4+6)÷6=4 months.
- **Elements**:
  - **Events**: Nodes marking activity start/end (no resources).
  - **Activities**: Arrows showing tasks (consume resources).
- **Advantages**:
  - Optimizes resource use.
  - Simplifies planning.
  - Works without prior data.
  - Improves completion date estimates.
  - Focuses on critical elements.
  - Enables proactive control.
- **Disadvantages**:
  - Unreliable without good time estimates.
  - Ignores costs.
  - Complex to interpret/update.
  - Subjective estimates may introduce bias.
- **PERT vs. CPM**:
  - CPM: Uses one time/cost estimate per activity.
  - PERT: Uses three time estimates, no costs, ideal for time-critical, uncertain projects.

## 8. Stakeholders
- **Definition**: Individuals/organizations influencing or influenced by the project, with varying authority/impact (positive, neutral, negative).
- **Key Roles**:
  - **Customer**: Acquires product.
  - **User**: Uses product.
  - **Performing Organization**: Executes project.
  - **Project Manager**: Manages project.
  - **Project Team**: Performs work.
  - **Sponsor**: Funds project.
  - **Influencers**: Indirectly affect project.
  - **PMO**: Oversees project management.
  - **Functional Managers**: Manage non-product areas (e.g., HR).
  - **Operations Management**: Manage core areas (e.g., R&D).
  - **Sellers/Vendors**: Supply components/services.
  - **Business Partners**: Provide expertise/support.
- **Concerns (Software Projects)**:
  - Customer: Requirements, reliability, security.
  - Manager: Cost, schedule, resources.
  - Architect: Maintainability, portability.
  - Developer: Components, reuse.
  - Tester: Functionality, regression.
- **Plan Stakeholder Management**:
  - Develop strategies based on stakeholders’ needs, expectations, and impact.
  - Use Stakeholder Engagement Assessment Matrix.

## 9. Organizational Structures
- **Types**:
  - **Functional**:
    - Organized by departments (e.g., Engineering).
    - **Pros**: Clear authority, specialization, career paths.
    - **Cons**: Silos, slow decisions, low PM power.
  - **Projectized**:
    - Organized by projects, PM has full control.
    - **Pros**: Unified command, effective communication.
    - **Cons**: Resource duplication, unclear career paths.
  - **Matrix**:
    - Combines functional and projectized (Weak, Balanced, Strong).
    - **Pros**: Efficient resource use, retains functional teams.
    - **Cons**: Dual reporting, complexity, conflicts.
- **Project Influence**:
  - Functional: Low PM authority, 0-25% full-time staff.
  - Weak Matrix: Limited PM authority, 15-60% full-time.
  - Balanced Matrix: Moderate PM authority, 50-95% full-time.
  - Strong Matrix: High PM authority, 85-100% full-time.
  - Projectized: Full PM authority, nearly all staff full-time.
- **Frames**:
  - Structural: Roles and coordination.
  - Human Resources: Balances organizational/individual needs.
  - Political: Manages conflict and power.
  - Symbolic: Emphasizes culture and symbols.

## 10. Common-Sense Project Approach
- **Start Right**: Define problem, set realistic goals.
- **Maintain Momentum**: Minimize turnover, prioritize quality, limit interference.
- **Track Progress**: Monitor work products via reviews.
- **Make Smart Decisions**: Simplify approaches.
- **Postmortem Analysis**: Document lessons learned.

## 11. Communication
- **Definition**: Exchanging information effectively when the interpreted message matches the intended one.
- **Types**:
  - **Verbal (7%)**: Speaking, writing, listening, reading.
  - **Nonverbal (93%)**: Gestures, tone (38%), body language (55%).
    - Interacts via repeating, conflicting, complementing, substituting, regulating, accenting.
- **Barriers**:
  - Lack of clarity, completeness, brevity, timeliness.
  - Organizational, status, semantic, inattention, perceptual issues.
  - Information overload, premature evaluation, channel dysfunction.
- **Overcoming Barriers**:
  - Ensure clarity, compassion, integrity.
  - Provide feedback, maintain attention.

## 12. Risk Management
- **Key Focus**:
  - **Types of Risks**: Technical, schedule, cost, resource, external.
  - **Processes**:
    1. Identify risks.
    2. Analyze (qualitative/quantitative).
    3. Plan responses.
    4. Implement responses.
    5. Monitor and control.
  - **Response Strategies**:
    - **Avoid**: Use alternative methods or skip risky tasks.
    - **Transfer**: Share impact (e.g., insurance).
    - **Mitigate**: Reduce probability/impact.
    - **Accept**: Proceed if mitigation isn’t cost-effective.
- **Manager’s Role**:
  - Maintain risk list from planning to completion.
  - Collect risks from all stakeholders.
  - Seek mitigation advice.
  - Distinguish risks (potential) from issues (current).