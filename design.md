# Design Document: Focus Timer Web App

## Overview

The Focus Timer Web App is a single-page application built with vanilla HTML, CSS, and JavaScript. It implements a Pomodoro timer with accountability through tab visibility detection and visual feedback via a virtual plant. The architecture follows a simple event-driven model where the timer, visibility detector, and plant visualization components communicate through a central state manager.

The application runs entirely in the browser with no backend dependencies, using the Document Visibility API to detect when users navigate away from the tab. The consequence system immediately resets the timer and degrades the plant visual when focus is broken.

## Architecture

### High-Level Structure

```
┌─────────────────────────────────────────┐
│           User Interface Layer          │
│  (HTML/CSS - Timer Display & Plant)     │
└─────────────────────────────────────────┘
                    ↕
┌─────────────────────────────────────────┐
│         Application State Manager       │
│   (Central state & event coordination)  │
└─────────────────────────────────────────┘
                    ↕
┌──────────────┬──────────────┬───────────┐
│ Timer Module │ Visibility   │  Plant    │
│              │ Detector     │  Renderer │
└──────────────┴──────────────┴───────────┘
```

### Component Interaction Flow

1. User clicks start button → State Manager initializes timer
2. Timer Module counts down → State Manager updates UI
3. Visibility Detector monitors tab state → Triggers consequence on tab switch
4. Consequence System → State Manager resets timer and updates plant
5. Plant Renderer → Updates visual based on state changes

## Components and Interfaces

### 1. State Manager

Central coordinator that maintains application state and orchestrates component interactions.

**State Structure:**
```javascript
{
  timerState: 'idle' | 'running' | 'completed',
  remainingSeconds: number,
  plantHealth: 'healthy' | 'degraded' | 'dead',
  currentSession: number
}
```

**Interface:**
```javascript
// Initialize the application
function initializeApp()

// Start a new work block
function startWorkBlock()

// Update timer (called every second)
function updateTimer()

// Handle visibility change
function handleVisibilityChange(isVisible)

// Reset timer to initial state
function resetTimer()

// Complete work block
function completeWorkBlock()

// Get current state
function getState()
```

### 2. Timer Module

Manages the countdown logic for 25-minute work blocks.

**Interface:**
```javascript
// Start countdown from 25 minutes (1500 seconds)
function startTimer(onTick, onComplete)

// Stop the timer
function stopTimer()

// Get remaining time in seconds
function getRemainingSeconds()

// Reset to 25 minutes
function resetToInitial()
```

**Implementation Details:**
- Uses `setInterval` with 1-second intervals
- Stores interval ID for cleanup
- Calls `onTick` callback every second with remaining time
- Calls `onComplete` callback when timer reaches zero

### 3. Visibility Detector

Monitors tab visibility using the Document Visibility API.

**Interface:**
```javascript
// Initialize visibility monitoring
function initializeVisibilityDetection(onVisibilityChange)

// Check current visibility state
function isTabVisible()

// Clean up event listeners
function cleanup()
```

**Implementation Details:**
- Listens to `visibilitychange` event on document
- Reads `document.visibilityState` or `document.hidden`
- Calls callback with boolean indicating visibility
- Only triggers consequences when timer is running

### 4. Plant Renderer

Manages the visual representation of the virtual plant.

**Interface:**
```javascript
// Render plant in healthy state
function renderHealthyPlant()

// Render plant in degraded state
function renderDegraded Plant()

// Render plant in dead state
function renderDeadPlant()

// Render success state (work block completed)
function renderSuccessPlant()

// Update plant based on health state
function updatePlantVisual(healthState)
```

**Implementation Details:**
- Uses CSS classes to switch between plant states
- Implements simple visual states using emoji or SVG
- Healthy: 🌱 (green, vibrant)
- Degraded: 🥀 (wilted, brown)
- Dead: 💀 (skull or dead plant)
- Success: 🌻 (blooming flower)

### 5. UI Controller

Manages DOM updates and user interactions.

**Interface:**
```javascript
// Update timer display
function updateTimerDisplay(minutes, seconds)

// Update start button state
function updateStartButton(enabled)

// Show completion message
function showCompletionMessage()

// Show consequence feedback
function showConsequenceFeedback()

// Initialize event listeners
function initializeEventListeners()
```

**Implementation Details:**
- Formats time as MM:SS
- Disables start button when timer is running
- Shows visual feedback for consequences
- Handles button click events

## Data Models

### Application State

```javascript
const AppState = {
  // Timer state: 'idle', 'running', or 'completed'
  timerState: string,
  
  // Remaining time in seconds (0-1500)
  remainingSeconds: number,
  
  // Plant health: 'healthy', 'degraded', or 'dead'
  plantHealth: string,
  
  // Current session number (increments on successful completion)
  currentSession: number,
  
  // Interval ID for cleanup
  intervalId: number | null
}
```

### Timer Configuration

```javascript
const TimerConfig = {
  // Work block duration in seconds (25 minutes)
  WORK_DURATION: 1500,
  
  // Update interval in milliseconds
  TICK_INTERVAL: 1000
}
```

### Plant States

```javascript
const PlantStates = {
  HEALTHY: 'healthy',
  DEGRADED: 'degraded',
  DEAD: 'dead',
  SUCCESS: 'success'
}
```


## Correctness Properties

A property is a characteristic or behavior that should hold true across all valid executions of a system - essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.

### Property 1: Timer initialization

*For any* application state, when a work block is started, the timer should begin at exactly 1500 seconds (25 minutes).

**Validates: Requirements 1.1**

### Property 2: Time display formatting

*For any* remaining seconds value between 0 and 1500, the display function should produce a string in MM:SS format where MM is zero-padded minutes and SS is zero-padded seconds.

**Validates: Requirements 1.2**

### Property 3: State transition after completion

*For any* completed work block, the application state should transition to allow starting a new work block.

**Validates: Requirements 1.4**

### Property 4: Visibility change detection

*For any* visibility state change (visible to hidden or hidden to visible), the visibility detector should trigger its callback with the correct visibility status.

**Validates: Requirements 2.1, 2.3**

### Property 5: Timer reset on tab switch

*For any* timer state during an active work block, when a tab switch occurs, the timer should reset to 1500 seconds.

**Validates: Requirements 3.1**

### Property 6: Plant degradation on focus break

*For any* active work block with a healthy plant, when the user switches tabs, the plant health should change to degraded or dead.

**Validates: Requirements 3.2**

### Property 7: No consequences when idle

*For any* non-running timer state (idle or completed), tab switches should not trigger timer resets or plant health changes.

**Validates: Requirements 3.3**

### Property 8: Visual feedback on consequence

*For any* consequence application (timer reset or plant degradation), the UI should update to reflect the change within one render cycle.

**Validates: Requirements 3.4**

### Property 9: Plant health preservation

*For any* work block that completes without visibility changes, the plant should remain in healthy or success state throughout.

**Validates: Requirements 4.2**

### Property 10: Distinct plant visuals

*For any* two different plant health states, the rendered output should be visually distinct (different CSS classes, emojis, or SVG states).

**Validates: Requirements 4.5**

## Error Handling

### Timer Edge Cases

1. **Rapid start/stop**: Prevent multiple timers running simultaneously by clearing previous interval before starting new one
2. **Negative time**: Ensure timer never displays negative values by clamping to zero
3. **Browser sleep/wake**: Handle cases where browser tab is suspended and resumed after long periods

### Visibility API Compatibility

1. **API availability**: Check for `document.visibilityState` support and fall back gracefully if unavailable
2. **Multiple rapid switches**: Debounce visibility changes to prevent multiple rapid consequence applications
3. **Browser differences**: Handle both `visibilitychange` event and vendor-prefixed versions if needed

### State Consistency

1. **Invalid state transitions**: Validate state transitions to prevent impossible states (e.g., completed while running)
2. **DOM not ready**: Ensure DOM elements exist before attempting to update them
3. **Cleanup on page unload**: Clear intervals and remove event listeners when page unloads

### User Experience

1. **Accidental tab switches**: Consider a grace period (1-2 seconds) before applying consequences for very brief tab switches
2. **Visual feedback timing**: Ensure consequence feedback is visible long enough for users to notice
3. **Button state management**: Prevent double-clicks on start button by disabling during timer run

## Testing Strategy

### Dual Testing Approach

The Focus Timer will use both unit tests and property-based tests to ensure comprehensive coverage:

- **Unit tests**: Verify specific examples, edge cases, and error conditions
- **Property tests**: Verify universal properties across all inputs using randomized testing

### Unit Testing Focus Areas

Unit tests should focus on:

1. **Specific examples**: 
   - Timer starts at exactly 25:00
   - Timer displays 00:00 when complete
   - Start button is present in DOM

2. **Edge cases**:
   - Timer behavior at 0 seconds
   - Visibility changes during idle state
   - Multiple rapid start attempts

3. **Integration points**:
   - State manager coordinates timer and plant updates
   - Visibility detector triggers consequence system
   - UI updates reflect state changes

4. **Error conditions**:
   - Visibility API not supported
   - DOM elements missing
   - Invalid state transitions

### Property-Based Testing Configuration

Property tests will use **fast-check** (JavaScript property-based testing library) with the following configuration:

- **Minimum 100 iterations** per property test
- Each test tagged with: **Feature: focus-timer, Property {number}: {property_text}**
- Random input generation for:
  - Timer states (remaining seconds 0-1500)
  - Plant health states
  - Visibility state transitions
  - Application states (idle, running, completed)

### Property Test Implementation

Each correctness property must be implemented as a single property-based test:

1. **Property 1**: Generate random initial states, start work block, verify timer = 1500s
2. **Property 2**: Generate random seconds (0-1500), verify MM:SS format with zero-padding
3. **Property 3**: Generate random completed states, verify can restart
4. **Property 4**: Generate random visibility changes, verify callbacks triggered
5. **Property 5**: Generate random running timer states, simulate tab switch, verify reset to 1500s
6. **Property 6**: Generate random active states with healthy plant, simulate tab switch, verify degradation
7. **Property 7**: Generate random idle/completed states, simulate tab switch, verify no consequences
8. **Property 8**: Generate random consequence triggers, verify UI updates
9. **Property 9**: Generate random work blocks, complete without switches, verify plant healthy/success
10. **Property 10**: Generate pairs of different health states, verify distinct rendering

### Test Coverage Goals

- 100% coverage of state transitions
- 100% coverage of consequence system logic
- 100% coverage of visibility detection
- 90%+ coverage of UI controller functions
- All 10 correctness properties validated through property tests
- All edge cases covered through unit tests

### Testing Tools

- **Test Framework**: Jest or Mocha
- **Property Testing**: fast-check
- **DOM Testing**: jsdom or browser environment
- **Assertions**: Chai or Jest assertions
- **Coverage**: Istanbul/nyc

### Manual Testing Checklist

While automated tests cover functional correctness, manual testing should verify:

1. Visual design matches minimal, distraction-free aesthetic
2. Plant visuals are clear and distinguishable
3. Timer is prominently displayed
4. Consequence feedback is noticeable but not jarring
5. Overall user experience feels smooth and focused
