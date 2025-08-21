make it look cool
tap bubbles for reps, set, muscle group and exercise 
```dataviewjs
const container = dv.el("div", "", { cls: "workout-container" });
const muscleSelector = document.createElement("select");
const exerciseSelector = document.createElement("select");
const repsInput = document.createElement("input");
const setsInput = document.createElement("input");
const weightsInput = document.createElement("input");
const logButton = document.createElement("button");
let muscleGroups;
muscleGroups = {
	Biceps: [
		"Bicep Curls",
		"Baysian Curls",
		"Incline Curls",
		"Preacher Curls",
		"Cable Hammer Curls",
	],	
	Tricep: [
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
	Shoulders: [
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
	Back: [
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
	Chest: [
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
//config of inputs only
[setsInput, repsInput, weightsInput].forEach((element) => {
	element.type = "number";
	element.min = "1";
	element.style.margin = "5px";
});
repsInput.placeholder = "Reps";
setsInput.placeholder = "Sets";
weightsInput.placeholder = "Weight in Kg"; 
//options for the selector as currently it is empty
const musclePlaceholder = document.createElement("option");
musclePlaceholder.value = "";
musclePlaceholder.textContent = "Select Muscle Group";
musclePlaceholder.disabled = true;
musclePlaceholder.selected = true;
muscleSelector.appendChild(musclePlaceholder);

for (let group in muscleGroups){
	let option = document.createElement("option");
	option.value = group;
	option.textContent = group;
	muscleSelector.appendChild(option);
}

const exercisePlaceholder = document.createElement("option");
exercisePlaceholder.value = "";
exercisePlaceholder.textContent = "Select Exercise";
exercisePlaceholder.disabled = true;
exercisePlaceholder.selected = true;
exerciseSelector.appendChild(exercisePlaceholder);
  

muscleSelector.addEventListener("change",() => {
	const selectedGroup = muscleSelector.value;
	
	exerciseSelector.innerHTML = "";
	const exercisePlaceholder = document.createElement("option");
	exercisePlaceholder.value = "";
	exercisePlaceholder.textContent = "Select Exercise";
    exercisePlaceholder.disabled = true;
    exercisePlaceholder.selected = true;
    exerciseSelector.appendChild(exercisePlaceholder); 
	
	if (selectedGroup && muscleGroups[selectedGroup]){
		muscleGroups[selectedGroup].forEach(exercise => {
			const option = document.createElement("option");
			option.value = exercise;
			option.textContent = exercise;
			exerciseSelector.appendChild(option);
		});
	};
})

logButton.textContent = "Log Workout";
container.appendChild(muscleSelector);
container.appendChild(exerciseSelector);
container.appendChild(setsInput);
container.appendChild(repsInput);
container.appendChild(weightsInput);
container.appendChild(logButton);
//wall of exercises lol
```
