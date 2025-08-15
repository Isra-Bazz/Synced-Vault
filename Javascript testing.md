```dataviewjs
const container = dv.el('div', '',{ cls: 'workout-container'});
const repsInput = document.createElement('input');
const setsInput = document.createElement('input');
const weightsInput = document.createElement('input');

//config of inputs only
[setsInput, repsInput, weightsInput].forEach(input => {
    input.type = 'number';
    input.min = '1';
    input.style.margin = '5px';
});
repsInput.placeholder = 'Reps';
setsInput.placeholder = 'Sets';
weightsInput.placeholder = 'Weight in Kg';
[setsInput, repsInput, weightsInput].forEach(input => container.appendChild(input));

```
