<!DOCTYPE html>
<html lang="en" class="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Wallpaper Hub</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* Custom styles for smooth theme transitions */
    html, body {
      transition: background-color 0.3s ease, color 0.3s ease;
    }
    .dark .bg-gray-100 { background-color: #1f2937; }
    .dark .bg-white { background-color: #374151; }
    .dark .text-gray-900 { color: #e5e7eb; }
    .dark .bg-gray-800 { background-color: #111827; }
    .dark .text-blue-600 { color: #60a5fa; }
    .dark .bg-blue-600 { background-color: #2563eb; }
    .dark .hover\:bg-blue-700:hover { background-color: #1d4ed8; }
    .dark .text-white { color: #d1d5db; }
  </style>
</head>
<body class="bg-gray-100 font-sans">
  <header class="bg-blue-600 text-white py-4">
    <div class="container mx-auto flex justify-between items-center px-4">
      <div>
        <h1 class="text-3xl font-bold">Wallpaper Hub</h1>
        <p class="mt-2">Explore and upload stunning wallpapers</p>
      </div>
      <button id="themeToggle" class="bg-gray-200 text-gray-900 px-4 py-2 rounded hover:bg-gray-300 dark:bg-gray-700 dark:text-white dark:hover:bg-gray-600">
        Toggle Dark Mode
      </button>
    </div>
  </header>

  <main class="container mx-auto py-8">
    <!-- Upload Section -->
    <section class="mb-8">
      <div class="bg-white p-6 rounded-lg shadow-md">
        <h2 class="text-2xl font-semibold mb-4 text-gray-900">Upload Your Wallpaper</h2>
        <input type="file" id="wallpaperUpload" accept="image/*" class="mb-4 p-2 border rounded">
        <button id="uploadBtn" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">Upload</button>
      </div>
    </section>

    <!-- Wallpaper Grid -->
    <section id="wallpaperGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <!-- Sample Wallpapers (placeholders) -->
      <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <img src="https://source.unsplash.com/random/400x300?nature" alt="Nature Wallpaper" class="w-full h-48 object-cover">
        <div class="p-4">
          <h3 class="text-lg font-semibold text-gray-900">Nature</h3>
          <button class="mt-2 text-blue-600 hover:underline">Download</button>
        </div>
      </div>
      <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <img src="https://source.unsplash.com/random/400x300?city" alt="City Wallpaper" class="w-full h-48 object-cover">
        <div class="p-4">
          <h3 class="text-lg font-semibold text-gray-900">City</h3>
          <button class="mt-2 text-blue-600 hover:underline">Download</button>
        </div>
      </div>
      <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <img src="https://source.unsplash.com/random/400x300?abstract" alt="Abstract Wallpaper" class="w-full h-48 object-cover">
        <div class="p-4">
          <h3 class="text-lg font-semibold text-gray-900">Abstract</h3>
          <button class="mt-2 text-blue-600 hover:underline">Download</button>
        </div>
      </div>
    </section>
  </main>

  <footer class="bg-gray-800 text-white py-4">
    <div class="container mx-auto text-center">
      <p>&copy; 2025 Wallpaper Hub. All rights reserved.</p>
    </div>
  </footer>

  <script>
    // Theme toggle functionality
    const themeToggle = document.getElementById('themeToggle');
    const htmlElement = document.documentElement;

    // Load saved theme from localStorage
    if (localStorage.getItem('theme') === 'dark') {
      htmlElement.classList.add('dark');
      themeToggle.textContent = 'Switch to Light Mode';
    } else {
      htmlElement.classList.add('light');
      themeToggle.textContent = 'Switch to Dark Mode';
    }

    // Toggle theme on button click
    themeToggle.addEventListener('click', () => {
      if (htmlElement.classList.contains('light')) {
        htmlElement.classList.remove('light');
        htmlElement.classList.add('dark');
        localStorage.setItem('theme', 'dark');
        themeToggle.textContent = 'Switch to Light Mode';
      } else {
        htmlElement.classList.remove('dark');
        htmlElement.classList.add('light');
        localStorage.setItem('theme', 'light');
        themeToggle.textContent = 'Switch to Dark Mode';
      }
    });

    // Existing upload and download functionality
    const uploadInput = document.getElementById('wallpaperUpload');
    const uploadBtn = document.getElementById('uploadBtn');
    const wallpaperGrid = document.getElementById('wallpaperGrid');

    uploadBtn.addEventListener('click', () => {
      const file = uploadInput.files[0];
      if (file && file.type.startsWith('image/')) {
        const reader = new FileReader();
        reader.onload = function(e) {
          const wallpaperCard = document.createElement('div');
          wallpaperCard.className = 'bg-white rounded-lg shadow-md overflow-hidden dark:bg-gray-700';
          wallpaperCard.innerHTML = `
            <img src="${e.target.result}" alt="Uploaded Wallpaper" class="w-full h-48 object-cover">
            <div class="p-4">
              <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Uploaded Wallpaper</h3>
              <button class="mt-2 text-blue-600 hover:underline dark:text-blue-400">Download</button>
            </div>
          `;
          wallpaperGrid.prepend(wallpaperCard);
          uploadInput.value = ''; // Reset input
        };
        reader.readAsDataURL(file);
      } else {
        alert('Please select a valid image file.');
      }
    });

    // Handle download button clicks
    wallpaperGrid.addEventListener('click', (e) => {
      if (e.target.tagName === 'BUTTON' && e.target.textContent === 'Download') {
        const img = e.target.parentElement.previousElementSibling;
        const link = document.createElement('a');
        link.href = img.src;
        link.download = img.alt.replace(' ', '_') + '.jpg';
        link.click();
      }
    });
  </script>
</body>
</html>
