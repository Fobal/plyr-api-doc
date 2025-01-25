---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Game room

## Overview

Game rooms are virtual spaces where players can participate in games. They are managed through a series of atomic operations that ensure data consistency and reliable gameplay experiences. Don't forget that each operation request requires proper headers (see [Headers](../../#base-headers) for header requirements).

## Available Operations

* **Create Game Room**: Initialize a new game room with specific configurations
* **Join Game Room**: Allow players to enter an existing game room
* **Pay Game Room**: Process payments for game room participation
* **Earn Game Room**: Distribute tokens to players from the game room
* **Leave Game Room**: Players can exit the game room
* **End Game Room**: Terminate the game room session

## Operation Flow

### 1. Creating and Joining Game Rooms

You have two options:

#### a) Atomic Operation (Recommended)

* Use `/game/createJoinPay` endpoint
* Single API call that:
  * Creates the game room
  * Joins all players
  * Handles payments
* Ensures data consistency through automatic rollback if any step fails
* Reduces network overhead and complexity

#### b) Separate Operations

1. Create game room
2. Join players individually or in groups
3. Process payments for each participant

### 2. Game Room Management

Once a game room is created:

* **Player Management**
  * Players can join (if game room capacity allows)
  * Players can leave at any time
  * Track player status and participation
* **Token Management**
  * Process initial payments (Pay operation)
  * Distribute rewards (Earn operation)
  * Support multiple tokens per transaction

### 3. Payment Integration

The system supports flexible payment handling:

* **Payment Timing**
  * During game room creation (atomic operation)
  * After game room creation (separate operation)
  * Pre-game or post-game payments
* **Payment Features**
  * Multiple token support
  * Variable amounts per player
* **Token Distribution**
  * Distribute rewards to multiple players
  * Support for different token types
  * Batch distribution capabilities
  * Synchronous or asynchronous processing

## Error Handling

All operations implement robust error handling:

* **Atomic Transactions**
  * Data consistency guaranteed
  * No partial state changes
* **Error Responses**
  * Detailed error messages
  * Error codes for programmatic handling
  * Actionable error resolution steps

## Operation Types

### Synchronous Operations

* Immediate response
* Best for quick operations
* Real-time feedback

### Asynchronous Operations

* Returns task ID
* Status polling available
* Suitable for long-running operations
* Prevents timeout issues

{% hint style="info" %}
Use asynchronous operations for actions that might take longer to complete.
{% endhint %}

## Best Practices

1. **Validation**
   * Verify game room state before operations
   * Validate player eligibility
   * Check payment requirements
   * Ensure sufficient token balances
2. **Error Management**
   * Implement proper error recovery
   * Handle edge cases
   * Log important events
3. **Operation Flow**
   * Use atomic operations when possible
   * Monitor async task status
   * Implement proper retry logic
4. **Security**
   * Always validate authentication
   * Check permissions
   * Protect sensitive data
   * Verify token distributions
5. **Performance**
   * Monitor operation timing
   * Implement rate limiting
   * Cache when appropriate
   * Batch token operations
