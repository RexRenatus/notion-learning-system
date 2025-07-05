# 🤖 AI Prompt Templates - Notion Learning System

## Overview
This file contains all AI prompt templates used throughout the system for various analysis and summary tasks.

---

## 📊 Daily Analysis Prompts

### Daily Reflection Analysis
```
Analyze today's learning journal and comments to identify patterns and insights:

## 9. AI-assisted daily reflection (Epiphany row)

At the end of each day, an automated reviewer (AI) MUST:

1. Open the current day's journal file.
2. Parse the **Reflections** section.
3. Append a new section **"Epiphany"** that contains:
   - **Patterns Observed:** Concise summary of recurring themes or hidden messages.
   - **Actionable To-Do:** Bullet list of systems, processes, or tasks inferred from the reflections.

TASKS COMPLETED:
{completed_tasks}

STUDY SESSIONS:
{session_details}

TIME ALLOCATION:
{time_by_subject}

Please provide:
1. **Thought Patterns**: Identify any recurring themes or concerns in the comments
2. **Productivity Insights**: When was the user most/least productive?
3. **Hidden TODOs**: Extract any implied tasks or commitments mentioned in comments
4. **Energy Patterns**: Identify emotional or energy states from the language used
5. **Learning Insights**: Key breakthroughs or struggles in today's learning
6. **Recommendations**: Specific, actionable suggestions for tomorrow

Keep analysis practical and actionable, focusing on patterns that can improve learning efficiency.
```

### Morning Sitrep Generation (6 AM)
```
Generate a comprehensive morning situation report for effective daily planning:

YESTERDAY'S DATA:
- Completed: {yesterday_completed}
- Missed: {yesterday_missed}
- Key Insights: {yesterday_insights}
- Time Spent: {yesterday_time_breakdown}

TODAY'S CONTEXT:
- Calendar Events: {calendar_events}
- Scheduled Study: {planned_sessions}
- Due Tasks: {due_tasks}
- Current Streaks: {streak_data}

WEEKLY TRENDS:
- Progress: {weekly_progress}
- Time Distribution: {weekly_time_dist}
- Consistency: {consistency_rate}

Generate a motivating yet realistic sitrep that includes:
1. **Priority Focus**: Top 3 things to accomplish today
2. **Time Blocking**: Suggested schedule based on calendar and energy patterns
3. **Risk Alerts**: Potential conflicts or at-risk streaks
4. **Motivation**: Personalized encouragement based on recent progress
5. **Quick Wins**: 2-3 easy tasks to build momentum
6. **Strategic Reminder**: Connection to larger goals

Format for easy mobile reading with clear sections and emojis.
```

---

## 📈 Pattern Recognition Prompts

### Weekly Pattern Analysis
```
Perform deep pattern analysis on the week's learning data:

COMMENT ANALYSIS:
{week_comments}

PRODUCTIVITY DATA:
{time_blocks_by_day}
{focus_quality_scores}
{completion_rates}

SUBJECT SWITCHING:
{subject_transition_log}

Identify:
1. **Recurring Thought Patterns**: What themes appear multiple times?
2. **Optimal Study Times**: When is focus highest?
3. **Subject Synergies**: Which subjects work well together?
4. **Fatigue Patterns**: When does productivity drop?
5. **Motivation Triggers**: What language indicates high/low motivation?
6. **Hidden Obstacles**: Unstated barriers to progress
7. **Success Patterns**: Conditions that led to breakthrough moments

Provide actionable recommendations for schedule optimization.
```

### Process Identification Prompt
```
Analyze learning activities to identify repeatable processes:

ACTIVITIES LOG:
{detailed_activity_log}

OUTCOMES:
{results_by_activity}

Extract:
1. **Successful Patterns**: Step-by-step processes that led to good outcomes
2. **Failure Patterns**: Common sequences that led to poor results
3. **Optimization Opportunities**: Where processes could be streamlined
4. **Missing Steps**: Implied activities not explicitly logged
5. **Process Templates**: Reusable workflows for different subject types

Format as flowchart-ready process descriptions.
```

---

## 🎯 Goal Decomposition Prompts

### Smart Goal Breakdown
```
Decompose this high-level goal into actionable daily tasks:

GOAL: {goal_description}
DEADLINE: {target_date}
CURRENT LEVEL: {starting_point}
AVAILABLE TIME: {hours_per_week}
CONSTRAINTS: {user_constraints}

Create:
1. **Milestone Map**: Major checkpoints with success criteria
2. **Weekly Targets**: Specific, measurable weekly goals
3. **Daily Actions**: 3-5 concrete daily tasks (15-30 min each)
4. **Progress Metrics**: How to measure advancement
5. **Adjustment Triggers**: When to modify the plan
6. **Habit Anchors**: Tasks to build into daily routine

Ensure all tasks follow the "second nature" principle - simple enough to repeat daily until automatic.
```

### Multi-Subject Balancing
```
Optimize study schedule across multiple subjects:

ACTIVE SUBJECTS: {subject_list_with_priorities}
TIME AVAILABLE: {daily_hours}
ENERGY PATTERNS: {energy_by_time}
DEADLINES: {upcoming_deadlines}
CURRENT PROGRESS: {progress_by_subject}

Design:
1. **Priority Matrix**: Which subjects need attention when
2. **Rotation Schedule**: Optimal subject switching pattern
3. **Deep vs Shallow**: Which subjects need deep focus blocks
4. **Synergy Pairs**: Subjects that complement each other
5. **Recovery Blocks**: When to schedule easier tasks
6. **Flexibility Rules**: How to adjust when life intervenes

Account for cognitive load and the principle of building foundations gradually.
```

---

## 🔄 Habit Formation Prompts

### Habit Transition Analysis
```
Evaluate when a learning task has become "second nature":

TASK: {task_description}
COMPLETION HISTORY: {last_30_days}
TIME TRENDS: {completion_times}
REMINDER DEPENDENCE: {reminder_interaction}
QUALITY METRICS: {performance_scores}

Assess:
1. **Automaticity Score**: How automatic is this behavior? (0-100)
2. **Consistency Rating**: Completion rate without reminders
3. **Efficiency Trend**: Is completion time decreasing?
4. **Quality Stability**: Is performance consistent?
5. **Cognitive Load**: User-reported effort level
6. **Graduation Readiness**: Should this move to "maintenance mode"?

Recommend whether to continue active tracking or transition to periodic check-ins.
```

---

## 📊 Progress Visualization Prompts

### Visual Progress Summary
```
Create a narrative description of progress suitable for visualization:

SUBJECT DATA: {all_subject_metrics}
TIME PERIOD: {period}
MILESTONES: {achieved_milestones}
STREAKS: {streak_information}

Generate:
1. **Hero's Journey**: Narrative arc of learning progress
2. **Mountain Climb**: How far up each "peak" (goal)
3. **Skill Tree**: Which abilities have been unlocked
4. **Heat Map Story**: Consistency patterns as weather
5. **XP Adventure**: Gamified progress narrative
6. **Foundation Building**: What base has been established

Use vivid metaphors that can be translated into visual dashboards.
```

---

## 🚨 Alert & Intervention Prompts

### Risk Detection
```
Identify learning risks that need intervention:

RECENT PATTERNS: {last_7_days}
STREAK STATUS: {all_streaks}
ENGAGEMENT METRICS: {interaction_data}
GOAL DEADLINES: {upcoming_deadlines}

Flag:
1. **Streak Risks**: Subjects about to lose streaks
2. **Burnout Signals**: Overextension patterns
3. **Neglected Areas**: Subjects falling behind
4. **Deadline Dangers**: Goals at risk of missing targets
5. **Motivation Dips**: Engagement decreasing
6. **Balance Issues**: Unhealthy focus distribution

Suggest gentle interventions that maintain momentum without adding pressure.
```

---

## 📝 Notes on Prompt Usage

1. **Variables in {}**: Replace with actual data from databases
2. **Prompt Length**: Keep under 1500 tokens for efficiency
3. **Response Format**: Request structured output for easy parsing
4. **Personalization**: Add user-specific context as needed
5. **Iteration**: Track which prompts give best results and refine

---

---

## 🔍 Specialized Pattern Recognition Prompts

### Time Productivity Analysis
```
Analyze time-based productivity patterns from study sessions:

SESSION DATA:
{sessions_with_timestamps}

QUALITY SCORES:
{focus_quality_by_time}

COMPLETION RATES:
{task_completion_by_hour}

Identify:
1. **Peak Performance Hours**: When is focus highest?
2. **Optimal Session Length**: How long before diminishing returns?
3. **Best Time by Subject**: Which subjects work best at which times?
4. **Energy Cycles**: Natural rhythm throughout the day
5. **Break Patterns**: Optimal rest intervals

Provide specific recommendations for time blocking.
```

### Subject Switching Pattern Analysis
```
Analyze subject transition patterns for optimal learning flow:

SWITCHING LOG:
{subject_transitions_with_times}

PERFORMANCE DATA:
{performance_before_after_switch}

CONTEXT:
{energy_levels_and_time_of_day}

Extract:
1. **Synergistic Pairs**: Which subjects complement each other?
2. **Costly Switches**: Which transitions hurt performance?
3. **Optimal Rotation**: Best sequence for multiple subjects
4. **Context Switching Cost**: Time lost in transitions
5. **Flow Maintenance**: How to preserve deep focus

Design an optimal daily subject rotation schedule.
```

### Energy Pattern Recognition
```
Map energy levels to optimize study scheduling:

SELF-REPORTED ENERGY:
{energy_ratings_by_time}

PERFORMANCE METRICS:
{actual_performance_data}

EXTERNAL FACTORS:
{sleep_meals_exercise_weather}

Determine:
1. **Energy Peaks**: When you're naturally most alert
2. **Energy Valleys**: Low points to avoid difficult tasks
3. **Recovery Patterns**: How quickly you recharge
4. **Energy Drains**: What activities deplete you fastest
5. **Energy Boosters**: What activities restore energy

Create an energy-optimized daily template.
```

### Procrastination Trigger Analysis
```
Identify and address procrastination patterns:

DELAYED TASKS:
{tasks_started_late_or_skipped}

CONTEXT DATA:
{circumstances_around_delays}

COMPLETION PATTERNS:
{eventual_completion_data}

Uncover:
1. **Common Triggers**: What causes procrastination?
2. **Avoidance Patterns**: Which tasks get delayed most?
3. **Environmental Factors**: External procrastination triggers
4. **Emotional States**: Feelings linked to delays
5. **Success Strategies**: What helps you start despite resistance

Design personalized anti-procrastination protocols.
```

### Success Pattern Recognition
```
Analyze conditions that lead to breakthrough learning:

HIGH-PERFORMANCE SESSIONS:
{top_20_percent_sessions}

BREAKTHROUGH MOMENTS:
{self_reported_insights}

ENVIRONMENTAL DATA:
{conditions_during_success}

Identify:
1. **Success Prerequisites**: What conditions enable peak performance?
2. **Breakthrough Patterns**: Common elements in "aha" moments
3. **Flow State Triggers**: How to reliably enter deep focus
4. **Momentum Builders**: What creates positive learning spirals
5. **Success Sequences**: Reproducible patterns for excellence

Create a "success recipe" for consistent high performance.
```

---

**Last Updated**: 2025-07-04
**Version**: 1.1