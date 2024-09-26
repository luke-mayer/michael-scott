<div align="center">
<h2> Michael Scott - The Hardcore Parkour Geometry Dash Reinforcement Learning Model </h2>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#forward">Forward</a>
    </li>
    <li>
      <a href="#overview">Overview</a>
    </li>
    <li>
      <a href="how-it-works">How It Works</a>
      <ul>
        <li><a href="#implementation">Implementation</a></li>
        <li><a href="#built-with">Built With</a></li>
        <li><a href="#limitations">Limitations</a></li>
      </ul>
    </li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## Forward

This project began as a final group project for the UMD computer science course CMSC421 (Intro to Artificial Intelligence). It was a collaboration between Daniel Guerrero-Martin, Ellison Eitel, Justin Kerns, Luke Mayer (me), and Rithvik Malladi. This is a fork of that original project that seeks to refine the training methods originally used in order to create a model with improved performance. Currently, the project is very similar to the original CMSC421 project with some
minor tweaks and refinements.

## Overview

Michael Scott is a reinforcement learning model that is designed to beat the Geometry Dash levels. Currently, Michael Scott can beat non-space ship sections (more on that later) of the Stereo Madness Level. Michael Scott is trained using a neural network that implements double deep q-learning. "Double" refers to the use of a second target network that updates weights from the online model at less frequent intervals in order to stabilize training and prevent convergence on suboptimal policies. "Deep" refers to the use of multi-layered deep neural network to update model weights. "Q-learning" refers to the use of the q-learning method of reinforcement learning which is more forward thinking in how it calculates rewards for given actions.

## How It Works

### Implementation

One of the things that sets this reinforcement learning project aside from other, similar ones is that it uses a commercial, Steam version of Geometry Dash as opposed to a recreation that allows backend access to the current game state and controls. Instead, screenshots of the game serve as the state and simulated keyboard inputs are used to allow the model to train and play the game in real-time. The game window is reduced to a size of 220 x 260 and the screenshots that serve as the state of the game are further cropped to a size of 80 x 150. This is done to reduce the size of inputs to the neural network, which in turn reduces the time it takes for one epoch or frame of training. The images are also grayscaled to reduce the size of the input and lower complexity. A desktop system with an Nvidia RTX 3080 is able to achieve around 20 epochs, or frames per second during training.

Isolated screenshots of the progress bar are used to determine progress and overall performance. The progress bar is also key in determining the terminal state when the model dies and restarts the level. We can determine when the model dies and restarts by when the progress bar resets to zero. This is extremely important for providing feedback to the model as it gets rewarded for every frame it is alive and punished severely if it dies. It is also minorly punished for every time it jumps. This is to motivate the model to only jump when necessary to avoid death.

See the original report for the CMSC421 class project ([found here](/documentation/)) for a more detailed breakdown of the project as well as cited sources that go into much more detail on deep learning, q-learning, and other concepts used in this project.

### Built With

- Python
- Gymnasium by Farama Foundation (Training environment)
- Pytorch (A framework for building deep learning models)
- Keras (A high-level wrapper for Pytorch)

### Limitations

The main obstacle to this model being able to fully beat Geometry Dash levels is that Geometry Dash has "space-ship" sections in its levels. In these sections, the nature of the game changes significantly. In the normal sections, the player jumps to avoid obstacles. This involves taking the jump action once which triggers an animation lasting several epochs before more input is required. In the space-ship section, the player holds the jump button to fly higher and falls otherwise. The act of holding jump is extremely difficult in the current implementation of inputting actions with the process of holding down jump being interrupted by the processes of the neural network as it trains in real-time. The space-ship sections are also much more dynamic which leads to many more possible states which makes it harder for the model to converge on an optimal policy. Finding solutions to this problem is the next goal of this project.

## Contact

LinkedIn - [https://www.linkedin.com/in/luke-mayer316/](https://www.linkedin.com/in/luke-mayer316/)  
HandShake - [https://umd.joinhandshake.com/profiles/50652472](https://umd.joinhandshake.com/profiles/50652472)  
Portfolio Site - [https://www.lukemayer.com](https://www.lukemayer.com)

## Acknowledgments

Full citations can be found in the original report for the CMSC421 class project which can be found here [/documentation](/documentation). (Note: this fork only addresses the double deep q-learning reinforcement implementation, not the NEAT implementation discussed in the report)
