# WeightR
A shiny app to let you now how much you should lift today, based on r/Fitness Basic Beginner Routine.

## Instructions for use

You need to provide the following information:

- the weight of your bar
- the trained body part (lower / upper body)
- the weight you lifted during your last training
- the number of reps you completed in your last set 

Based on this information, the app computes how wuch you should lift at your next training. You also get the detail of how much to put on each side of the bar, as well as suggestions for incremental warm-ups.

## How is the new weight computed?

Performs 3 sets for each exercise. The two first sets are 5 reps, the last one is as many reps as possible, up to 15 reps. The number of reps during your last set determines how much you should lift at your next session:

- if you completed 15 reps, add 2 kg for upper body and 4 kg for lower body
- if you completed between 5 and 14 reps, add 1 kg for upper body and 2 kg for lower body
- if you completed less than 5 reps, remove 10% of the total weight

More information [here](https://thefitness.wiki/routines/r-fitness-basic-beginner-routine/).
