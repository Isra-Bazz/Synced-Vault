```dataviewjs
// 🏋️ Define available exercises
const exercises = ["Bench Press", "Squat", "Deadlift", "Overhead Press", "Pull-ups", "Bicep Curl", "Tricep Dip"];

// 🎯 Define goal weights for tracking
const goalWeights = {
    "Bench Press": 100,
    "Squat": 150,
    "Deadlift": 180,
    "Overhead Press": 60,
    "Pull-ups": 20,
    "Bicep Curl": 25,
    "Tricep Dip": 30
};

// 🎛️ UI Elements
const container = dv.el("div", "", { cls: "workout-container" });
const select = document.createElement("select");
const setsInput = document.createElement("input");
const repsInput = document.createElement("input");
const weightInput = document.createElement("input");
const logButton = document.createElement("button");
const graphContainer = dv.el("div", "", { cls: "graph-container" });

// Populate Dropdown
exercises.forEach(ex => {
    let option = document.createElement("option");
    option.value = ex;
    option.textContent = ex;
    select.appendChild(option);
});

// Configure Input Fields
[setsInput, repsInput, weightInput].forEach(input => {
    input.type = "number";
    input.min = "1";
    input.style.margin = "5px";
});
setsInput.placeholder = "Sets";
repsInput.placeholder = "Reps";
weightInput.placeholder = "Weight (kg)";

// Load Last Used Values from Local Storage
if (localStorage.getItem("lastWorkout")) {
    let lastWorkout = JSON.parse(localStorage.getItem("lastWorkout"));
    select.value = lastWorkout.exercise;
    setsInput.value = lastWorkout.sets;
    repsInput.value = lastWorkout.reps;
    weightInput.value = lastWorkout.weight;
}

// Configure Log Button
logButton.textContent = "Log Exercise";
logButton.style.margin = "10px";
logButton.onclick = () => {
    const selectedExercise = select.value;
    const sets = setsInput.value || "0";
    const reps = repsInput.value || "0";
    const weight = weightInput.value || "0";
    const date = new Date().toISOString().split("T")[0];

    // Save Last Used Values
    localStorage.setItem("lastWorkout", JSON.stringify({ exercise: selectedExercise, sets, reps, weight }));

    // Calculate One-Rep Max (Epley formula)
    const oneRepMax = Math.round(weight * (1 + reps / 30));

    // Format Workout Entry
    const workoutLog = `- ${date} | **${selectedExercise}**: ${sets} sets × ${reps} reps @ ${weight}kg (1RM: ${oneRepMax}kg)\n`;

    // Append to Dedicated Workout Log Note
    app.vault.adapter.append("Workout Log.md", workoutLog);

    // Clear Inputs
    setsInput.value = "";
    repsInput.value = "";
    weightInput.value = "";
};

// Append Elements
container.appendChild(select);
container.appendChild(setsInput);
container.appendChild(repsInput);
container.appendChild(weightInput);
container.appendChild(logButton);

// 📊 Progress Tracking: Fetch Workout Data from "Workout Log.md"
const workoutData = dv.pages('"Workout Log.md"')
    .flatMap(p => p.file.lists)
    .filter(entry => entry.text.match(/\d{4}-\d{2}-\d{2}/)) // Match date format
    .map(entry => {
        const match = entry.text.match(/(\d{4}-\d{2}-\d{2}) \| \*\*(.*?)\*\*: (\d+) sets × (\d+) reps @ (\d+)kg \(1RM: (\d+)kg\)/);
        return match ? { date: match[1], exercise: match[2], weight: parseInt(match[5]), oneRepMax: parseInt(match[6]) } : null;
    }).filter(entry => entry);

// 📈 Generate Progress Graph
const graphData = {};
workoutData.forEach(entry => {
    if (!graphData[entry.exercise]) graphData[entry.exercise] = [];
    graphData[entry.exercise].push({ date: entry.date, weight: entry.weight, oneRepMax: entry.oneRepMax });
});

// Display Graphs and Goal Progress
for (let [exercise, data] of Object.entries(graphData)) {
    const sortedData = data.sort((a, b) => new Date(a.date) - new Date(b.date));
    
    let graphText = `#### ${exercise} Progress\n\`\`\`chart\nx-axis: Date\ny-axis: Weight (kg)\n`;
    let oneRepMaxGraph = `\n\`\`\`chart\nx-axis: Date\ny-axis: One-Rep Max (kg)\n`;

    sortedData.forEach(point => {
        graphText += `${point.date}: ${point.weight}\n`;
        oneRepMaxGraph += `${point.date}: ${point.oneRepMax}\n`;
    });

    graphText += "```" + oneRepMaxGraph + "```";

    dv.el("pre", graphText);

    // Display Goal Progress
    if (goalWeights[exercise]) {
        const latestWeight = sortedData[sortedData.length - 1].weight;
        const goalWeight = goalWeights[exercise];
        const progressPercent = Math.min(100, Math.round((latestWeight / goalWeight) * 100));

        dv.el("p", `🎯 Goal for **${exercise}**: ${latestWeight}kg / ${goalWeight}kg (${progressPercent}%)`);
    }
}
```