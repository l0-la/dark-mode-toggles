<!-- # dark-mode-toggles
second image toggle not working -->

<!-- First toggle -->
<div  class="ml-4 whitespace-nowrap">
      		<input type="checkbox" id="theme_{{forloop.counter}}" class="toggle-input" checked>
      			<label for="theme_{{forloop.counter}}" class="inline-block w-8 h-8 align-middle">
        			<img src="https://cdn.shopify.com/s/files/1/0602/3000/9086/files/CoterieWebSymbols-04.png?v=1648444367"  alt="Dark mode" class="toggle-icon">
      			</label>
</div>
<!-- Second toggle for mobile menu -->
<div  class="ml-4 whitespace-nowrap">
      		<input type="checkbox" id="theme_{{forloop.counter}}" class="toggle-input" checked>
      			<label for="theme_{{forloop.counter}}" class="inline-block w-8 h-8 align-middle">
        			<img src="https://cdn.shopify.com/s/files/1/0602/3000/9086/files/CoterieWebSymbols-04.png?v=1648444367"  alt="Dark mode" class="toggle-icon">
      			</label>
</div>
<!-- Style sheet -->
toggle {
  position: inline-block;
  margin-bottom: 24px;
  user-select: none;
}

.content:hover .toggle-icon {
  animation: wiggle 1s linear;
}

.toggle-icon {
  width: 28px;
  user-select: none;
}

.toggle-input {
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
  user-select: none;
}

.toggle-label {
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border: 3px solid var(--text-main);
  padding: 4px;
  border-radius: 50px;
  width: 100px;
  margin: 0 auto;
  background-color: var(--text-bg);
  transition: all 0.3s ease;
  user-select: none;
}

.toggle-label:hover {
  background-color: var(--shadow);
}

.toggle-label:active {
  transform: scale(0.95);
}

<!-- Javascript -->

  <!-- toogle for dark mode -->
<script type="text/javascript">
const page = document.querySelector('body');
const toggle = page.querySelector('.toggle-input');
const toggleIcon = page.querySelector('.toggle-icon');

// set theme and localStorage on page load
setCheckedState();

function setCheckedState() {
  // checks if localStorage has a "checked" value set at all
  if (!(localStorage.checked === undefined)) {
    // if it does, it sets the state of the toggle accordingly
    toggle.checked = isTrue(localStorage.getItem('checked'));
    // after setting the toggle state, the theme is adjusted according to the checked state
    toggleTheme();
  }
}

function toggleTheme() {
  // Toggle theme based on state of checkbox
  replaceClass();
  // replace icons on page
  toggleIconTheme();
  // set the value of the "checked" key in localStorage
  updateLocalStorage();
}

function replaceClass() {
  if (toggle.checked) {
    page.classList.replace('light', 'dark');
  } else {
    page.classList.replace('dark', 'light');
  }
}

function toggleIconTheme() {
  // Replace icons not able to be targeted by css variables
  if (page.classList.contains('light')) {
    toggleIcon.src = 'https://cdn.shopify.com/s/files/1/0602/3000/9086/files/CoterieWebSymbols-04.png?v=1648444367';
    toggleIcon.alt = 'Switch to Dark Mode';
  } else {
    toggleIcon.src = 'https://cdn.shopify.com/s/files/1/0602/3000/9086/files/CoterieWebSymbols-05.png?v=1648444378';
    toggleIcon.alt = 'Switch to Light Mode';
  }
}

function updateLocalStorage() {
  localStorage.setItem('checked', toggle.checked);
}

function isTrue(value) {
  // convert string to boolean
  return value === 'true';
}

// Toggle theme any time the state of the checkbox changes
toggle.addEventListener('change', toggleTheme);


