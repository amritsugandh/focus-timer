# Implementation Plan: Focus Timer Web App

## Overview

This implementation plan breaks down the Focus Timer Web App into discrete coding tasks. The approach follows a bottom-up strategy: first implementing core modules (timer, visibility detection), then building the state manager to coordinate them, and finally creating the UI layer. Each task builds incrementally with testing integrated throughout to catch errors early.

## Tasks

- [ ] 1. Set up project structure and HTML foundation
  - Create index.html with basic structure and semantic elements
  - Create styles.css with CSS reset and base styles
  - Create app.js as main application entry point
  - Link all files together and verify page loads
  - _Requirements: 5.1, 5.2, 5.4_

- [ ] 2. Implement Timer Module
  - [ ] 2.1 Create timer.js with core countdown logic
    - Implement startTimer() function with setInterval
    - Implement stopTimer() with interval cleanup
    - Implement getRemainingSeconds() getter
    - Implement resetToInitial() to reset to 1500 seconds
    - _Requirements: 1.1, 1.2_
  
  - [ ]* 2.2 Write property test for timer initialization
    - **Property 1: Timer initialization**
    - **Validates: Requirements 1.1**
  
  - [ ]* 2.3 Write property test for time display formatting
    - **Property 2: Time display formatting**
    - **Validates: Requirements 1.2**
  
  - [ ]* 2.4 Write unit tests for timer edge cases
    - Test timer at 0 seconds
    - Test multiple start/stop cycles
    - Test interval cleanup
    - _Requirements: 1.1, 1.2_

- [ ] 3. Implement Visibility Detector Module
  - [ ] 3.1 Create visibility.js with Document Visibility API integration
    - Implement initializeVisibilityDetection() with event listener
    - Implement isTabVisible() using document.visibilityState
    - Implement cleanup() to remove event listeners
    - Add browser compatibility check for Visibility API
    - _Requirements: 2.1, 2.3_
  
  - [ ]* 3.2 Write property test for visibility change detection
    - **Property 4: Visibility change detection**
    - **Validates: Requirements 2.1, 2.3**
  
  - [ ]* 3.3 Write unit tests for visibility detector
    - Test visibility change event handling
    - Test API availability check
    - Test cleanup functionality
    - _Requirements: 2.1, 2.3_

- [ ] 4. Implement Plant Renderer Module
  - [ ] 4.1 Create plant.js with visual state management
    - Implement renderHealthyPlant() with healthy emoji/visual
    - Implement renderDegradedPlant() with degraded emoji/visual
    - Implement renderDeadPlant() with dead emoji/visual
    - Implement renderSuccessPlant() with success emoji/visual
    - Implement updatePlantVisual() to switch between states
    - _Requirements: 4.1, 4.2, 4.3, 4.4, 4.5_
  
  - [ ]* 4.2 Write property test for distinct plant visuals
    - **Property 10: Distinct plant visuals**
    - **Validates: Requirements 4.5**
  
  - [ ]* 4.3 Write unit tests for plant rendering
    - Test each plant state renders correctly
    - Test state transitions update DOM
    - Test CSS classes are applied correctly
    - _Requirements: 4.1, 4.4, 4.5_

- [ ] 5. Checkpoint - Verify core modules work independently
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 6. Implement State Manager
  - [ ] 6.1 Create state.js with central state management
    - Define AppState object structure
    - Implement initializeApp() to set initial state
    - Implement startWorkBlock() to begin timer
    - Implement updateTimer() callback for timer ticks
    - Implement handleVisibilityChange() for tab switches
    - Implement resetTimer() for consequence system
    - Implement completeWorkBlock() for successful completion
    - Implement getState() getter
    - _Requirements: 1.1, 1.3, 1.4, 3.1, 3.2, 3.3_
  
  - [ ]* 6.2 Write property test for state transition after completion
    - **Property 3: State transition after completion**
    - **Validates: Requirements 1.4**
  
  - [ ]* 6.3 Write property test for timer reset on tab switch
    - **Property 5: Timer reset on tab switch**
    - **Validates: Requirements 3.1**
  
  - [ ]* 6.4 Write property test for plant degradation on focus break
    - **Property 6: Plant degradation on focus break**
    - **Validates: Requirements 3.2**
  
  - [ ]* 6.5 Write property test for no consequences when idle
    - **Property 7: No consequences when idle**
    - **Validates: Requirements 3.3**
  
  - [ ]* 6.6 Write property test for plant health preservation
    - **Property 9: Plant health preservation**
    - **Validates: Requirements 4.2**

- [ ] 7. Implement UI Controller
  - [ ] 7.1 Create ui.js with DOM manipulation functions
    - Implement updateTimerDisplay() to format and show MM:SS
    - Implement updateStartButton() to enable/disable button
    - Implement showCompletionMessage() for work block completion
    - Implement showConsequenceFeedback() for visual feedback
    - Implement initializeEventListeners() for button clicks
    - _Requirements: 1.2, 1.5, 3.4, 5.1, 5.2_
  
  - [ ]* 7.2 Write property test for visual feedback on consequence
    - **Property 8: Visual feedback on consequence**
    - **Validates: Requirements 3.4**
  
  - [ ]* 7.3 Write unit tests for UI controller
    - Test timer display formatting
    - Test button state management
    - Test completion message display
    - Test consequence feedback visibility
    - _Requirements: 1.2, 1.5, 3.4_

- [ ] 8. Wire components together in main app
  - [ ] 8.1 Integrate all modules in app.js
    - Import all modules (timer, visibility, plant, state, ui)
    - Initialize state manager on page load
    - Connect timer callbacks to state manager
    - Connect visibility detector to state manager
    - Connect state updates to UI controller
    - Connect state updates to plant renderer
    - Wire start button to startWorkBlock()
    - _Requirements: 1.1, 1.2, 1.3, 1.4, 2.1, 2.3, 3.1, 3.2, 3.3, 3.4_
  
  - [ ]* 8.2 Write integration tests for complete flow
    - Test full work block completion without tab switches
    - Test consequence system triggers on tab switch
    - Test timer reset and plant degradation together
    - Test multiple work block cycles
    - _Requirements: 1.1, 1.3, 1.4, 3.1, 3.2, 4.2_

- [ ] 9. Implement CSS styling
  - [ ] 9.1 Style the timer display
    - Large, prominent font for timer
    - Clean, minimal styling
    - Centered layout
    - _Requirements: 5.1, 5.3, 5.4_
  
  - [ ] 9.2 Style the plant visualization
    - Clear, visible plant display
    - Smooth state transitions (if any)
    - Positioned prominently below timer
    - _Requirements: 5.2, 5.3, 5.4_
  
  - [ ] 9.3 Style the start button and feedback elements
    - Clear, accessible button styling
    - Consequence feedback styling (subtle but noticeable)
    - Completion message styling
    - _Requirements: 1.5, 3.4, 5.3, 5.5_
  
  - [ ] 9.4 Apply minimal color palette and typography
    - Choose 2-3 colors maximum
    - Select clean, readable font
    - Ensure sufficient contrast
    - Avoid distracting animations
    - _Requirements: 5.3, 5.5_

- [ ] 10. Add error handling and edge cases
  - [ ] 10.1 Add Visibility API compatibility check
    - Check for document.visibilityState support
    - Provide fallback or warning if unavailable
    - _Requirements: 2.1_
  
  - [ ] 10.2 Add timer edge case handling
    - Prevent multiple simultaneous timers
    - Clamp timer display to non-negative values
    - Handle browser sleep/wake scenarios
    - _Requirements: 1.1, 1.2_
  
  - [ ] 10.3 Add state validation
    - Validate state transitions
    - Check DOM elements exist before updating
    - Add cleanup on page unload
    - _Requirements: 1.1, 1.4, 3.1_
  
  - [ ]* 10.4 Write unit tests for error handling
    - Test Visibility API unavailable scenario
    - Test rapid start/stop attempts
    - Test invalid state transitions
    - Test DOM element missing scenarios

- [ ] 11. Final checkpoint - Complete system verification
  - Ensure all tests pass, ask the user if questions arise.

## Notes

- Tasks marked with `*` are optional and can be skipped for faster MVP
- Each task references specific requirements for traceability
- Checkpoints ensure incremental validation
- Property tests validate universal correctness properties with 100+ iterations using fast-check
- Unit tests validate specific examples and edge cases
- The implementation follows a modular approach for maintainability
- All modules are vanilla JavaScript with no framework dependencies
