# Multiagent Pacman Project

This project implements various AI search and decision-making algorithms for Pacman agents in a multiagent setting. The project focuses on implementing minimax, alpha-beta pruning, and expectimax algorithms to create intelligent behavior for Pacman when facing ghost adversaries.

## Project Overview

In this project, Pacman faces off against ghost agents in a classic game setting. The main goal is to implement and evaluate different adversarial search algorithms to help Pacman make optimal decisions in various game scenarios.

The project explores several key concepts in artificial intelligence:
- Adversarial search algorithms (minimax, alpha-beta pruning)
- Probabilistic modeling with expectimax
- Evaluation function design
- Multi-agent coordination and competition

## Getting Started

### Prerequisites

- Python 3.x
- tkinter [link](https://docs.python.org/3/library/tkinter.html)

### Installation

1. Clone or download the project files
2. Navigate to the project directory
3. You're ready to run the game!

## Running the Game

### Basic Game Execution

```bash
python pacman.py
```

### Game Controls

- Use arrow keys or WASD for movement
- Press Ctrl-C to quit the game

## Project Structure

### Key Files

- `multiAgents.py`: Contains the implementation of various agent algorithms
- `pacman.py`: The main game engine
- `game.py`: The core game logic
- `ghostAgents.py`: Implementation of ghost behaviors
- `layout.py`: Code for reading and processing game board layouts
- `util.py`: Useful data structures for implementing search algorithms

### Agent Types

1. **ReflexAgent**: A simple reflex-based agent that evaluates state-action pairs
2. **MinimaxAgent**: Implements the minimax algorithm for adversarial search
3. **AlphaBetaAgent**: Implements minimax with alpha-beta pruning for improved efficiency
4. **ExpectimaxAgent**: Implements the expectimax algorithm for probabilistic modeling of ghosts

## Project Requirements

### Question 1: Reflex Agent (4 points)

Improve the `ReflexAgent` in `multiAgents.py` to play respectably. The agent should consider both food locations and ghost locations to perform well. Your agent should easily clear the `testClassic` layout and perform reasonably well on the `mediumClassic` layout.

```bash
python pacman.py -p ReflexAgent -l testClassic
python pacman.py --frameTime 0 -p ReflexAgent -k 1
```

**Evaluation**: Your agent will be tested on the `openClassic` layout 10 times. You'll receive points based on win rate and average score:
- 0 points if your agent times out or never wins
- 1 point if your agent wins at least 5 times
- 2 points if your agent wins all 10 games
- Additional 1 point if average score > 500
- Additional 2 points if average score > 1000

### Question 2: Minimax (5 points)

Implement the minimax algorithm in the `MinimaxAgent` class. Your implementation should:
- Work with any number of ghosts
- Handle multiple min layers (one for each ghost) for every max layer
- Expand the game tree to an arbitrary depth specified by `self.depth`
- Use the provided evaluation function `self.evaluationFunction`

```bash
python pacman.py -p MinimaxAgent -l minimaxClassic -a depth=4
```

**Note**: A single search ply is considered to be one Pacman move and all the ghosts' responses, so depth 2 search will involve Pacman and each ghost moving two times.

### Question 3: Alpha-Beta Pruning (5 points)

Implement alpha-beta pruning in the `AlphaBetaAgent` class to more efficiently explore the minimax tree. Your implementation should:
- Extend the alpha-beta pruning logic to handle multiple minimizer agents (ghosts)
- Produce identical minimax values as the `MinimaxAgent`
- Process successor states in the order returned by `GameState.getLegalActions`
- Not prune on equality to match the autograder's expected state exploration

```bash
python pacman.py -p AlphaBetaAgent -a depth=3 -l smallClassic
```

### Question 4: Expectimax (5 points)

Implement the expectimax algorithm in the `ExpectimaxAgent` class. This agent models ghosts as probabilistic agents rather than adversarial ones. Your implementation should:
- Replace the min operations with expectation operations
- Model ghosts as choosing uniformly at random from their legal moves
- Use floating-point arithmetic for averages

```bash
python pacman.py -p ExpectimaxAgent -l minimaxClassic -a depth=3
```

Compare the behavior with alpha-beta pruning:
```bash
python pacman.py -p AlphaBetaAgent -l trappedClassic -a depth=3 -q -n 10
python pacman.py -p ExpectimaxAgent -l trappedClassic -a depth=3 -q -n 10
```

### Question 5: Evaluation Function (6 points)

Implement a better evaluation function for Pacman in the `betterEvaluationFunction` function. Unlike the reflex agent, this function evaluates states rather than actions. Your evaluation function should:
- Clear the `smallClassic` layout with one random ghost more than half the time
- Run at a reasonable rate
- Achieve a high average score (around 1000 points when winning)

```bash
python autograder.py -q q5
```

**Evaluation**: Your function will be tested on the `smallClassic` layout 10 times with points assigned as follows:
- 1 point for winning at least once without timing out
- Additional 1 point for winning at least 5 times
- Additional 2 points for winning all 10 times
- Additional 1 point for average score ≥ 500
- Additional 2 points for average score ≥ 1000
- Additional 1 point if games take on average less than 30 seconds

## Testing

### Running Tests

Use the autograder to test your implementations:

```bash
python autograder.py
```

Test specific questions:

```bash
python autograder.py -q q2
```

### Available Test Options

- `-q`: Specify which question to test
- `--no-graphics`: Run tests without graphics
- `--timeout`: Set timeout duration for tests

## Game Layouts

The `layouts/` directory contains various map configurations:

- `smallClassic.lay`: A small game layout
- `mediumClassic.lay`: A medium-sized layout (default)
- `minimaxClassic.lay`: Layout for testing minimax agents
- `trappedClassic.lay`: Layout where Pacman can be trapped
- `originalClassic.lay`: The classic Pacman layout

## Command Line Options

### Game Options

```bash
python pacman.py --layout smallClassic --pacman MinimaxAgent
```

- `-l, --layout`: Choose the game board layout (default: mediumClassic)
- `-p, --pacman`: Select the Pacman agent type (default: KeyboardAgent)
- `-g, --ghosts`: Select the ghost agent type (default: RandomGhost)
- `-k, --numghosts`: Set the number of ghosts (default: 4)
- `-n, --numGames`: Number of games to play (default: 1)
- `-f, --fixRandomSeed`: Fix the random seed for reproducible results
- `-z, --zoom`: Zoom the size of the graphics window (default: 1.0)
- `--frameTime`: Time to delay between frames (default: 0.1)
- `-a, --agentArgs`: Arguments to pass to agents (e.g., "depth=3")
- `-t, --textGraphics`: Display output as text only
- `-q, --quietTextGraphics`: Generate minimal output and no graphics
- `-c, --catchExceptions`: Turns on exception catching
- `--timeout`: Maximum time an agent can spend computing in a game (default: 30s)

## Educational Objectives

This project is designed to teach:
- Implementation of adversarial search algorithms
- Understanding of minimax and expectimax principles
- Pruning techniques for improved efficiency
- Evaluation function design for complex state spaces
- Modeling probabilistic vs. adversarial agents

## Refference
- berkeley ai webpage [link](https://ai.berkeley.edu/project_overview.html)