
# PRD: Timeframe-Based Priority System

## Introduction/Overview

This feature replaces the current 1-10 urgency scale on the "Prioritise & Manage" page with a timeframe selector that allows users to specify when they want to complete a task. The system will automatically convert the selected timeframe into an urgency score, which will then be used with the existing importance rating to calculate priority.

**Problem it solves:** The current 1-10 urgency scale is abstract and subjective. Users often struggle to decide whether a task is a "7" or an "8" in urgency. A concrete timeframe (e.g., "complete in 3 days") is more intuitive and actionable.

**Goal:** Make task prioritization more intuitive by allowing users to set completion timeframes, while maintaining the existing priority calculation system.

## Goals

1. Replace the urgency rating interface (1-10 scale) with a timeframe selector
2. Automatically convert timeframes to urgency scores for priority calculation
3. Maintain the existing importance rating system (1-10 scale)
4. Display timeframes clearly in the task list views
5. Ensure backward compatibility with existing tasks

## User Stories

1. **As a user**, I want to specify when I need to complete a task using days/weeks/months/years, so that I can set more concrete and meaningful deadlines.

2. **As a user**, I want the system to automatically calculate urgency from my chosen timeframe, so that I don't have to think about abstract urgency scores.

3. **As a user**, I want to see both the timeframe and time remaining for my tasks, so that I know exactly when things are due.

4. **As a user**, I want my existing tasks to work with the new system, so that I don't lose my current priority data.

## Functional Requirements

### FR1: Timeframe Selector UI
1.1. The urgency question interface must display a slider control instead of the 1-10 button grid  
1.2. The slider must have a unit selector with options: Days, Weeks, Months, Years  
1.3. The slider range must update based on selected unit:
   - Days: 1-6
   - Weeks: 1-3
   - Months: 1-11
   - Years: 1-10  
1.4. The current selected value must be displayed clearly (e.g., "3 weeks")  
1.5. Both the slider and unit selector must be positioned together for easy interaction

### FR2: Importance Rating
2.1. The importance rating interface must remain unchanged (1-10 scale with buttons)  
2.2. The importance question must still appear after the timeframe is selected  
2.3. The flow must be: Timeframe → Importance → Next task or completion

### FR3: Urgency Calculation
3.1. The system must convert timeframes to urgency scores (1-10) using this formula:
   - Convert timeframe to total days
   - Urgency = 11 - min(10, ceil(days/30 * 10))
   - Examples:
     - 1 day = urgency 10
     - 3 days = urgency 10
     - 1 week (7 days) = urgency 9
     - 2 weeks (14 days) = urgency 9
     - 1 month (30 days) = urgency 9
     - 3 months (90 days) = urgency 7
     - 6 months (180 days) = urgency 4
     - 1 year (365 days) = urgency 1  
3.2. The calculated urgency score must be stored in the task's `urgency` field  
3.3. The original timeframe values must be stored separately in new fields: `timeframeValue` and `timeframeUnit`

### FR4: Task Display
4.1. Tasks in the priority list must display both the timeframe and time remaining  
4.2. Display format: "Complete in: 3 weeks (21 days remaining)"  
4.3. Time remaining must be calculated from the current date to the target completion date  
4.4. If a task is overdue, display "Overdue by X days" in red/warning color  
4.5. The priority score display must show: "Priority Score: X (U:Y × I:Z)" where Y is the calculated urgency

### FR5: Priority Calculation
5.1. Priority must continue to be calculated as: `urgency × importance`  
5.2. The urgency value used in calculation must be the auto-calculated value from the timeframe  
5.3. Tasks must be sorted by priority score in descending order within each quadrant

### FR6: Editing Priority
6.1. When editing a task's priority, the timeframe selector must display the current timeframe values  
6.2. Users must be able to change both the timeframe and importance  
6.3. Changing the timeframe must recalculate the urgency score automatically

### FR7: Backward Compatibility
7.1. Existing tasks with urgency/importance scores (but no timeframe data) must prompt the user to re-rate them with the new timeframe system  
7.2. When an old task is re-rated, add the `timeframeValue` and `timeframeUnit` fields  
7.3. The system must handle mixed states where some tasks have timeframes and others don't  
7.4. Display a notice: "This task needs to be re-rated with the new timeframe system" for old tasks

## Non-Goals (Out of Scope)

1. Changing the quadrant categorization system (urgent/important matrix)
2. Adding calendar integration or date pickers
3. Implementing recurring tasks or deadline reminders
4. Modifying the importance rating system
5. Adding deadline notifications or alerts
6. Implementing task dependencies or subtasks

## Design Considerations

### UI Components Needed:
1. **Slider Control:**
   - HTML5 range input styled to match existing button aesthetics
   - Value display showing current selection (e.g., "3" with "weeks")
   - Min/max labels

2. **Unit Selector:**
   - Four buttons/toggles for: Days, Weeks, Months, Years
   - Active state styling to show selected unit
   - Position adjacent to or integrated with slider

3. **Task Display Updates:**
   - Add timeframe info row below task title
   - Use muted color for "days remaining" text
   - Red/warning styling for overdue tasks

### Visual Layout:
```
How long do you need to complete this task?
[Task card display here]

Select your timeframe:
[Days] [Weeks] [Months] [Years]  ← Unit selector buttons

1 ———————●————— 3                ← Slider
1 = Minimum          3 = Maximum  ← Labels
```

## Technical Considerations

1. **Data Structure Changes:**
   - Add `timeframeValue` (number) to task object
   - Add `timeframeUnit` (string: 'days'|'weeks'|'months'|'years') to task object
   - Add `targetDate` (timestamp) calculated from timeframe
   - Maintain `urgency` field for compatibility

2. **Calculation Logic:**
   - Create utility function to convert timeframe to days
   - Create utility function to calculate urgency from days
   - Create utility function to calculate days remaining

3. **Integration Points:**
   - Modify `renderPriorityQuestion()` to show slider instead of button grid
   - Modify `setPriorityRating()` to accept timeframe data
   - Modify task display in `renderPriorityTasks()` to show timeframe
   - Update `calculatePriority()` if needed (should work as-is)

## Success Metrics

1. **User Engagement:** 90% of users complete the new timeframe-based priority rating (vs current completion rate)
2. **Task Completion:** Increase in tasks completed by their target timeframe by 15%
3. **User Feedback:** Positive feedback on the intuitiveness of the new system (target: 4+ stars out of 5)
4. **Re-rating Rate:** At least 80% of existing tasks re-rated within first week of feature launch

## Open Questions

1. ✅ How to handle tasks where the timeframe passes? Display as overdue? (Answered: Yes, show "Overdue by X days" in warning color)
2. ✅ Should we allow users to switch back to the old 1-10 scale? (Answered: No, timeframe-only)
3. Should we add a "No deadline" option for tasks without time constraints?
4. How to handle timeframes less than 1 day (e.g., "complete in 4 hours")? Currently out of scope.
5. Should the default unit be based on task quadrant? (e.g., Q1 defaults to Days, Q4 defaults to Months)
