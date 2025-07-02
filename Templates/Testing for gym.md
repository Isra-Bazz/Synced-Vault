```dataviewjs 
const container = dv.el("div", "", { cls: "workout-container" });
const muscleSelector = document.createElement("select");
const exerciseSelector = document.createElement("select");
const repsInput = document.createElement("input");
const setsInput = document.createElement("input");
const weightsInput = document.createElement("input");
const logButton = document.createElement("button");

//config of inputs only
[setsInput, repsInput, weightsInput].forEach((element) => {
  input.type = "number";
  input.min = "1";
  input.style.margin = "5px";
});
repsInput.placeholder = "Reps";
setsInput.placeholder = "Sets";
weightsInput.placeholder = "Weight in Kg";

//options for the selector as currently it is empty
for (let group in muscleGroups){
  let option = document.createElement("option");
  option.value = element;
  option.textContent = element;
  muscleSelector.appendChild(option);
}

muscleGroupsSelect.addEventListener("change",() => {
  const selectedGroup = muscleSelector.value;

  exerciseSelector.innerHTML = '<option value="">Select Exercise</option>'

  if (selectedGroup && muscleGroups[selectedGroup]){
    muscleGroups[selectedGroup].forEach(exercise => {
      const option = document.createElement("option");
      option.value = exercise;
      option.textContent = exercise;
      exerciseSelector.appendChild(option);
    });
  };
})

//wall of exercises lol

muscleGroups = {
  bicepExercises: [
    "Bicep Curls",
    "Baysian Curls",
    "Incline Curls",
    "Preacher Curls",
    "Cable Hammer Curls",
  ],
  tricepExercises: [
    "Close-Grip Bench Press",
    "Dips (bodyweight or assisted)",
    "Overhead Dumbbell Tricep Extension",
    "Skull Crushers (EZ Bar)",
    "Tricep Rope Pushdown",
    "Straight Bar Pushdown",
    "Single-Arm Overhead Cable Extension",
    "Dumbbell Kickback",
    "Bench Dips",
    "Cable Tricep Extension (reverse grip)",
  ],
  shoulderExercises: [
    "Overhead Barbell Press",
    "Seated Dumbbell Shoulder Press",
    "Lateral Raises",
    "Front Dumbbell Raise",
    "Rear Delt Fly (dumbbell or machine)",
    "Arnold Press",
    "Cable Lateral Raise",
    "Barbell Upright Row",
    "Face Pulls",
    "Single-Arm Cable Rear Delt Row",
  ],
  backExercises: [
    "Pull-ups",
    "Deadlifts",
    "Barbell Rows",
    "Dumbbell Rows",
    "Lat Pulldown",
    "Seated Cable Row",
    "Chest-Supported Row (machine or free weights)",
    "T-Bar Row",
    "Face Pulls (rear delts and traps)",
    "Straight-Arm Pulldown",
  ],
  chestExercises: [
    "Barbell Bench Press",
    "Incline Dumbbell Press",
    "Flat Dumbbell Press",
    "Cable Crossover",
    "Chest Dips (leaning forward)",
    "Incline Cable Fly",
    "Pec Deck Machine",
    "Push-ups (weighted if needed)",
    "Machine Chest Press",
    "Dumbbell Pullover",
  ],
};
```
