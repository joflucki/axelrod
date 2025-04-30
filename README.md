# Axelrod

![GitHub License](https://img.shields.io/github/license/joflucki/axelrod?color=red)
![Deno Badge](https://img.shields.io/badge/built%20with-Rust-00894f?logo=rust)
![GitHub last commit](https://img.shields.io/github/last-commit/joflucki/axelrod?color=purple)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/joflucki/axelrod/test.yml?label=tests)

**A simple Rust API for simulating games based on Robert Axelrod's collaborate/defect scenario.**

The `axelrod` crate provides a straightforward way to define agents with different strategies and run simulations of the iterated Prisoner's Dilemma and similar games. It's designed to be:

* **Simple:** Easy to understand and use API.
* **Flexible:** Allows users to define custom agent strategies.
* **Parallel:** Capable of running a large number of games concurrently for efficient analysis.
* **Rust-native:** Leverages the performance and safety of the Rust programming language.

## Getting Started


### Installation

Add the following to your `Cargo.toml` file under the `[dependencies]` section:

```toml
[dependencies]
axelrod_rs = "0.1.0"
````

Then, in your Rust code, you can import the crate:

```rust
extern crate axelrod_rs;
```

### Basic Usage

```rust
use axelrod_rs::Agent;
use axelrod_rs::Game;
use axelrod_rs::Decision;

// Define a simple agent that always cooperates
struct CooperatingAgent;

impl Agent for CooperatingAgent {
    fn decide(&self, history: &[((Decision, Decision), i32)]) -> Decision {
        Decision::Cooperate
    }
}

// Define a simple agent that always defects
struct DefectingAgent;

impl Agent for DefectingAgent {
    fn decide(&self, history: &[((Decision, Decision), i32)]) -> Decision {
        Decision::Defect
    }
}

fn main() {
    let agent1 = CooperatingAgent;
    let agent2 = DefectingAgent;
    let rounds = 5;
    let payoffs = ((3, 3), (0, 5), (5, 0), (1, 1)); // (CC, CD, DC, DD)

    let game = Game::new(agent1, agent2, rounds, payoffs);
    let results = game.play();

    println!("Game Results: {:?}", results);
}
```

## Contribution

This project is open-sourced under the [MIT License](LICENSE). If you have any suggestions or find issues, feel free to open an issue on the repository. Collaboration and contribution is further detailed in the [Contributing Guide](CONTRIBUTING.md) and in the [Code of Conduct](CODE_OF_CONDUCT.md).

## License

This project is licensed under the [MIT License](LICENSE). See the `LICENSE` file for more information.
