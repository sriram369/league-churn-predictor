

# **League of Legends Player Churn Prediction System**

**A Cloud Computing Capstone Project for Riot Games**

## **Project Overview**

This project is a **Proof of Concept (POC)** for a system designed to help Riot Games, the creator of *League of Legends*, solve a critical business problem: **players quitting matches out of frustration** (often called "rage quitting").

When players abruptly leave games, it hurts the experience for others, disrupts matchmaking, and can lead to players leaving the game entirely, which costs Riot potential revenue. Our system uses **artificial intelligence (AI)** and **cloud computing** to identify players who are likely to quit *before they actually do*, allowing for potential interventions to keep them engaged.

This project was developed as part of the **BU.330.740 Large Scale Computing on the Cloud** course.

## **The Problem: Why Players Quit**

In competitive online games like *League of Legends*, players can become frustrated by:
- Losing streaks or falling far behind in a match.
- Negative interactions with teammates (toxic chat).
- Feeling that the matchmaking was unfair.

This frustration can lead to a player suddenly disconnecting from the game. For Riot, this is bad for business because:
1.  It ruins the game for the other nine players in the match.
2.  Unhappy players are less likely to spend money on in-game cosmetics.
3.  Over time, it can damage the game's reputation and player base.

## **Our Proposed Solution**

We designed a software system that analyzes game data in **real-time** to predict which players are at high risk of quitting.

**The Core Idea:** By monitoring specific signals from a live game—like how often a player dies, their gold difference, if they are spamming pings, or starting surrender votes—our AI model can calculate a **"Quit Probability" score**. If the score is very high, the system could trigger a helpful action, like a positive in-game message, to try and calm the player down.

## **How We Built the Proof of Concept (POC)**

Since we could not access Riot's actual live game data, we took a two-step approach to prove our idea works:

### **1. Simulating Real Game Data**
We wrote a program that creates realistic, fictional matches. This simulator acts like a mini *League of Legends* server, generating data for hundreds of matches with two types of players:
-   **"Tilted" Players:** Those having a bad game, showing signs of frustration.
-   **"Normal" Players:** Those having a standard game experience.

The data includes all the key signals our real system would look for.

### **2. Building and Training the AI Model**
We used the simulated match data to train a **Machine Learning model** (specifically, a Random Forest classifier). Think of this like teaching the computer to recognize patterns:
-   We showed it thousands of data examples from simulated games.
-   For each example, we told the computer whether that fictional player ended up quitting or not.
-   The computer learned which combinations of signals (many deaths + toxic chat + surrender votes) most strongly predict a player is about to quit.

## **Key Results & Findings**

*   **Model Accuracy:** Our AI model can correctly predict whether a player will rage quit **74.9% of the time** in our simulation. When tested on a larger dataset of 10,000 matches, the patterns became even clearer.
*   **Top Predictors:** The model identified the most important warning signs:
    1.  **Players starting or voting for a surrender** (43% importance).
    2.  **Having a large gold deficit** (being far behind in gold) at the 15-minute mark (21% importance).
    3.  **A drop in Actions Per Minute (APM)**, which indicates the player is becoming less engaged (16% importance).
*   **Business Impact:** Based on Riot's published player numbers, if this system were implemented, it could proactively help retain players, potentially safeguarding an estimated **$135 million in annual revenue**.
*   **Scalability:** We mathematically validated that the system design can scale from analyzing 200 matches (our test) to handling **625,000 matches per hour**, matching Riot's real-world traffic.

## **The Proposed Cloud Architecture**

For a full implementation at Riot, we designed a system using Amazon Web Services (AWS):

1.  **AWS Kinesis:** Would ingest millions of real-time data events from live game servers.
2.  **AWS EMR (Spark):** Would process this streaming data to calculate the key signals (like gold deficit, death counts) for each player.
3.  **AWS SageMaker:** Would host our trained AI model, receiving the processed signals and calculating the live "Quit Probability" score.
4.  **AWS Lambda:** If the score is above a critical threshold (e.g., 85%), this service would instantly send a signal back to the game server to trigger a subtle intervention.

## **Project Files**

*   **`LoL_Churn_Indicator_POC.ipynb`**: This is the main Jupyter Notebook, containing all the code for the data simulation, AI model training, testing, and results analysis. It was built in **Google Colab**.
*   **`README.md`**: This file, explaining the project.

## **How to View/ Run This Project**

The easiest way to explore this project is through **Google Colab**:

1.  Go to [https://colab.research.google.com/](https://colab.research.google.com/)
2.  Select the **"GitHub"** tab.
3.  Paste the URL of this GitHub repository.
4.  Open the `LoL_Churn_Indicator_POC.ipynb` notebook.
5.  You can now run each code cell step-by-step to see the simulation in action and generate the results.

*(No installation is needed on your own computer, as Colab runs everything in the cloud.)*

## **Team & Academic Context**

This project was created by **[Your Name/Team Name]** for the course **BU.330.740: Large Scale Computing on the Cloud**. The goal was to identify a real-world business problem and design a viable, cloud-native big data solution, supported by a working proof of concept.

**Disclaimer:** This is an **academic/portfolio project**. It is not affiliated with, endorsed by, or connected to Riot Games. All game data was simulated for educational purposes to demonstrate system design principles and machine learning application.

---

## **In Simple Terms: What Did We Actually Do?**

Imagine you're a coach watching a soccer game. You can see when a player gets frustrated: they might stop running, argue with the referee, or make reckless tackles. A good coach spots these signs early and might substitute the player to prevent them from getting a red card.

Our project is like building an **AI coach for *League of Legends***.

1.  **We defined the signs of frustration:** For a video game, this is data like frequent deaths, negative chat, and calling for surrender.
2.  **We created practice games:** Since we couldn't watch real Riot games, we simulated thousands of them to have data to work with.
3.  **We trained the AI:** We showed our AI all the simulated game data and the outcomes, teaching it the connection between the signs and a player quitting.
4.  **We proved it could work:** Our tests show the AI coach can correctly spot a player about to quit most of the time. We also designed a plan for how Riot could build a full-scale version using cloud services to monitor all their games simultaneously.

This project demonstrates how **data, AI, and cloud computing** can be combined to solve a tangible, expensive problem in the gaming industry.
