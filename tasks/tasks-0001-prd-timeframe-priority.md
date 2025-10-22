
# Tasks: Timeframe-Based Priority System

## Relevant Files

- `index.html` - Main application file containing UI, styling, and all JavaScript logic

### Notes

- This is a single-file application, so all changes will be made to `index.html`
- No separate test files exist; testing will be manual/visual
- Changes will modify the existing priority rating system while maintaining backward compatibility

## Tasks

- [x] 1.0 Update Data Structure and Storage
  - [x] 1.1 Add timeframe fields to task data structure (timeframeValue, timeframeUnit, targetDate)
  - [x] 1.2 Update localStorage load function to initialize new fields for backward compatibility
  - [x] 1.3 Update Firestore sync to handle new fields when loading remote data
- [x] 2.0 Create Timeframe Selector UI Components
- [ ] 3.0 Implement Timeframe to Urgency Conversion Logic
- [ ] 4.0 Update Task Display to Show Timeframes
- [ ] 5.0 Implement Backward Compatibility and Migration
