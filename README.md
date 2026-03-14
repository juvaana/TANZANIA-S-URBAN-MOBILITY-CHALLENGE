# TANZANIA-S-URBAN-MOBILITY-CHALLENGE 
Predict Peak Daladala Demand. Build Smarter Cities.
Tanzania’s cities move fast. Dar es Salaam never sleeps. Mwanza expands. Arusha grows. Dodoma builds. Mbeya connects.
Yet transport demand remains unpredictable.
This challenge puts you in control.
Your mission is simple but powerful: build a machine learning model that predicts when a daladala route will hit peak demand.
This is not theory.
This is not toy data.

You will be working with an urban mobility simulation built at national scale.

Welcome to Juvaana.





Why This Matters
Rush hour congestion costs time and productivity.

Rain changes commuter behavior.

End-of-month salary cycles shift transport patterns across cities.

If we can accurately predict peak demand:

Operators can optimize dispatch
Cities can reduce congestion
Transportation systems become smarter and more efficient
This is how data transforms infrastructure.





The Challenge
You are provided with historical simulation data from five Tanzanian cities:

Dar es Salaam
Mwanza
Arusha
Dodoma
Mbeya
Each row represents a daladala route at a specific hour.

Your task is to predict whether demand will be:

High demand → peak = 1
Normal demand → peak = 0
The idea is simple.

The modeling is serious.





The Data
You will receive three files:

train.csv – Contains features along with the target variable peak
test.csv – Contains only features (you must predict peak)
Within the dataset, you will find meaningful signals:

Strong patterns during morning rush hours (6–9 AM)
Evening rush hours (4–8 PM)
Higher demand intensity in Dar es Salaam
Weather influences commuter behavior
Salary cycles impact transport flow
Population density plays a role
There is also:

Distribution shift between training and test data
Noise features included
Real-world data is not clean — and neither is this dataset.





Evaluation
Submissions are ranked using the F1 Score.

We use F1 because we care about balanced performance — not simply predicting the majority class.

Higher F1 score = Better model
Better model = Higher leaderboard ranking






Submission Format
Your submission must:

Be named submission.csv
Contain exactly two columns: id and peak
Match the IDs in the test set
Include only binary values in the peak column (0 or 1)
Contain no probabilities
Invalid formats will be automatically rejected.





Strategy Tips
Explore feature importance early
Study city-specific behavior
Account for rainfall-related distribution shifts
Avoid overfitting noisy variables
Modeling Suggestions
Logistic Regression → Strong baseline
Boosting models → Potentially stronger performance
A strong baseline should achieve an F1 score of approximately 0.70 or higher.

Can you push beyond 0.80?





Rewards
This is Juvaana’s onboarding challenge.

Top performers will receive:

Official Juvaana Data Explorer Badge
Verified digital certificate
Featured profile on the national leaderboard
Early access to upcoming Juvaana Prize Competitions
Future challenges will include cash prizes.

This is where you build your competitive edge.





Rules
External data is not allowed
Manual relabeling is prohibited
Reverse engineering test labels is forbidden
Collaboration is not permitted unless team format is explicitly enabled
We monitor anomalies.

Play fair. Compete hard.





Beginner Friendly
This is a beginner-friendly competition.

We have provided tutorials to guide you through:

Getting started with Juvaana competitions
Understanding the platform
Making participation smoother and more accessible




Final Question
Are you ready to predict peak demand and help design smarter cities?
