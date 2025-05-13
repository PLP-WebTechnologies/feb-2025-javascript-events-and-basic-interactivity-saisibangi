/*JavaScript Event Handling & Interactive Elements Assignment*/
/*index.html*/
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JS Event Assignment</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Interactive Button -->
  <section>
    <button id="magicButton">Click Me!</button>
  </section>
  <!-- Image Gallery -->
  <section>
    <h2>Image Gallery</h2>
    <div id="gallery">
      <img src="https://via.placeholder.com/300x200?text=Image+1" alt="Image 1" class="gallery-img active">
      <img src="https://via.placeholder.com/300x200?text=Image+2" alt="Image 2" class="gallery-img">
      <img src="https://via.placeholder.com/300x200?text=Image+3" alt="Image 3" class="gallery-img">
    </div>
    <button id="prevBtn">Previous</button>
    <button id="nextBtn">Next</button>
  </section>
  <!-- Tabs -->
  <section>
    <h2>Tabs</h2>
    <div class="tabs">
      <button class="tab-button active" data-tab="tab1">Tab 1</button>
      <button class="tab-button" data-tab="tab2">Tab 2</button>
      <button class="tab-button" data-tab="tab3">Tab 3</button>
    </div>
    <div class="tab-content" id="tab1">Content for Tab 1</div>
    <div class="tab-content hidden" id="tab2">Content for Tab 2</div>
    <div class="tab-content hidden" id="tab3">Content for Tab 3</div>
  </section>
  <!-- Form -->
  <section>
    <h2>Contact Form</h2>
    <form id="contactForm">
      <div>
        <label for="name">Name:</label>
        <input type="text" id="name" required>
        <span class="error" id="nameError"></span>
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" required>
        <span class="error" id="emailError"></span>
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" required>
        <span class="error" id="passwordError"></span>
      </div>
      <button type="submit">Submit</button>
    </form>
  </section>

  <script src="script.js"></script>
</body>
</html>

/*style.css*/
body {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

button {
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

button:hover {
  background-color: #ddd;
  transform: scale(1.05);
}

#magicButton {
  background-color: #6200ea;
  color: white;
  border: none;
  border-radius: 5px;
}

#gallery {
  position: relative;
  height: 200px;
  margin-bottom: 20px;
}

.gallery-img {
  position: absolute;
  width: 300px;
  height: 200px;
  opacity: 0;
  transition: opacity 0.5s;
}

.gallery-img.active {
  opacity: 1;
}

.tabs {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}

.tab-button {
  background: #f0f0f0;
  border: none;
  padding: 10px;
}

.tab-button.active {
  background: #6200ea;
  color: white;
}

.tab-content {
  padding: 20px;
  border: 1px solid #ddd;
}

.tab-content.hidden {
  display: none;
}

form div {
  margin-bottom: 15px;
}

input {
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}

.error {
  color: red;
  font-size: 0.8em;
}
/*script.js*/
const magicButton = document.getElementById('magicButton');

magicButton.addEventListener('click', () => {
  magicButton.textContent = magicButton.textContent === 'Click Me!' ? 'Clicked!' : 'Click Me!';
  magicButton.style.backgroundColor = magicButton.style.backgroundColor === 'rgb(98, 0, 234)' ? '#ff5722' : '#6200ea';
});

magicButton.addEventListener('mouseover', () => {
  magicButton.style.transform = 'scale(1.1)';
});
magicButton.addEventListener('mouseout', () => {
  magicButton.style.transform = 'scale(1)';
});

document.addEventListener('keypress', (e) => {
  console.log(`Key pressed: ${e.key}`);
});

// Bonus: Secret double-click action
magicButton.addEventListener('dblclick', () => {
  alert('Secret Action: You found the double-click surprise!');
});

const galleryImages = document.querySelectorAll('.gallery-img');
const prevBtn = document.getElementById('prevBtn');
const nextBtn = document.getElementById('nextBtn');
let currentImage = 0;

function showImage(index) {
  galleryImages.forEach((img, i) => {
    img.classList.toggle('active', i === index);
  });
}

prevBtn.addEventListener('click', () => {
  currentImage = (currentImage - 1 + galleryImages.length) % galleryImages.length;
  showImage(currentImage);
});

nextBtn.addEventListener('click', () => {
  currentImage = (currentImage + 1) % galleryImages.length;
  showImage(currentImage);
});

const tabButtons = document.querySelectorAll('.tab-button');
const tabContents = document.querySelectorAll('.tab-content');

tabButtons.forEach(button => {
  button.addEventListener('click', () => {
    tabButtons.forEach(btn => btn.classList.remove('active'));
    button.classList.add('active');
    tabContents.forEach(content => content.classList.add('hidden'));
    document.getElementById(button.dataset.tab).classList.remove('hidden');
  });
});
const form = document.getElementById('contactForm');
const nameInput = document.getElementById('name');
const emailInput = document.getElementById('email');
const passwordInput = document.getElementById('password');
const nameError = document.getElementById('nameError');
const emailError = document.getElementById('emailError');
const passwordError = document.getElementById('passwordError');

nameInput.addEventListener('input', () => {
  nameError.textContent = nameInput.value.trim() ? '' : 'Name is required';
});

emailInput.addEventListener('input', () => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  emailError.textContent = emailRegex.test(emailInput.value) ? '' : 'Invalid email format';
});

passwordInput.addEventListener('input', () => {
  passwordError.textContent = passwordInput.value.length >= 8 ? '' : 'Password must be at least 8 characters';
});

form.addEventListener('submit', (e) => {
  e.preventDefault();
  let valid = true;

  if (!nameInput.value.trim()) {
    nameError.textContent = 'Name is required';
    valid = false;
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(emailInput.value)) {
    emailError.textContent = 'Invalid email format';
    valid = false;
  }

  if (passwordInput.value.length < 8) {
    passwordError.textContent = 'Password must be at least 8 characters';
    valid = false;
  }

  if (valid) {
    alert('Form submitted successfully!');
    form.reset();
  }
});
