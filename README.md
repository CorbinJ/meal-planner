```html
<!DOCTYPE html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meal Planner Pro</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Inter Font -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { font-family: 'Inter', sans-serif; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 h-full flex flex-col antialiased selection:bg-emerald-500 selection:text-white">

    <!-- Header -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-xs">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-emerald-500 to-teal-400 flex items-center justify-center text-white shadow-md shadow-emerald-500/20">
                    <i class="fa-solid fa-utensils text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg text-slate-900 tracking-tight leading-tight">MealPlanner <span class="text-emerald-600 font-extrabold">Pro</span></h1>
                    <p class="text-xs text-slate-500">Capture, Plan, & Shop Smarter</p>
                </div>
            </div>
            
            <!-- Navigation Tabs -->
            <nav class="hidden md:flex space-x-1 bg-slate-100 p-1 rounded-xl">
                <button onclick="switchTab('log')" id="nav-log" class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition-all text-slate-700 hover:text-slate-900">
                    <i class="fa-solid fa-camera-retro mr-2"></i>Log Meal
                </button>
                <button onclick="switchTab('history')" id="nav-history" class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition-all bg-white text-emerald-600 shadow-xs">
                    <i class="fa-solid fa-table-list mr-2"></i>Meal History
                </button>
                <button onclick="switchTab('planner')" id="nav-planner" class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition-all text-slate-700 hover:text-slate-900">
                    <i class="fa-solid fa-calendar-days mr-2"></i>Weekly Planner
                </button>
                <button onclick="switchTab('grocery')" id="nav-grocery" class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition-all text-slate-700 hover:text-slate-900">
                    <i class="fa-solid fa-basket-shopping mr-2"></i>Grocery List
                </button>
            </nav>

            <!-- Quick Action button -->
            <div class="flex items-center space-x-3">
                <button onclick="openLogModal()" class="bg-emerald-600 hover:bg-emerald-700 text-white font-medium px-4 py-2 rounded-xl text-sm shadow-sm transition-all flex items-center space-x-2">
                    <i class="fa-solid fa-plus"></i>
                    <span class="hidden sm:inline">Add Meal</span>
                </button>
            </div>
        </div>
        <!-- Mobile Nav Bar -->
        <div class="md:hidden flex border-t border-slate-100 bg-white">
            <button onclick="switchTab('log')" id="mob-nav-log" class="mobile-tab flex-1 py-3 text-center text-xs font-medium text-slate-500 border-b-2 border-transparent">
                <i class="fa-solid fa-camera-retro block text-base mb-1"></i>Log
            </button>
            <button onclick="switchTab('history')" id="mob-nav-history" class="mobile-tab flex-1 py-3 text-center text-xs font-medium text-emerald-600 border-b-2 border-emerald-600">
                <i class="fa-solid fa-table-list block text-base mb-1"></i>History
            </button>
            <button onclick="switchTab('planner')" id="mob-nav-planner" class="mobile-tab flex-1 py-3 text-center text-xs font-medium text-slate-500 border-b-2 border-transparent">
                <i class="fa-solid fa-calendar-days block text-base mb-1"></i>Planner
            </button>
            <button onclick="switchTab('grocery')" id="mob-nav-grocery" class="mobile-tab flex-1 py-3 text-center text-xs font-medium text-slate-500 border-b-2 border-transparent">
                <i class="fa-solid fa-basket-shopping block text-base mb-1"></i>Grocery
            </button>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 overflow-y-auto">

        <!-- TAB 1: LOG MEAL VIEW -->
        <section id="tab-content-log" class="tab-content hidden max-w-3xl mx-auto">
            <div class="bg-white rounded-2xl shadow-xs border border-slate-200 overflow-hidden">
                <div class="p-6 sm:p-8 border-b border-slate-100 bg-gradient-to-r from-emerald-50/50 to-teal-50/50">
                    <h2 class="text-xl font-bold text-slate-900">Log a New Culinary Creation</h2>
                    <p class="text-sm text-slate-500 mt-1">Snap a photo, record your recipe, and categorize your dish.</p>
                </div>
                <form id="meal-form" onsubmit="handleMealSubmit(event)" class="p-6 sm:p-8 space-y-6">
                    
                    <!-- Photo Capture / Upload -->
                    <div>
                        <label class="block text-sm font-semibold text-slate-700 mb-2">Meal Photo</label>
                        <div class="mt-1 flex justify-center px-6 pt-5 pb-6 border-2 border-slate-300 border-dashed rounded-xl hover:border-emerald-500 transition-colors bg-slate-50/50 relative group cursor-pointer" onclick="document.getElementById('meal-photo-input').click()">
                            <div class="space-y-2 text-center" id="photo-preview-container">
                                <div id="photo-placeholder">
                                    <div class="mx-auto w-12 h-12 rounded-full bg-emerald-100 flex items-center justify-center text-emerald-600 mb-2 group-hover:scale-110 transition-transform">
                                        <i class="fa-solid fa-camera text-xl"></i>
                                    </div>
                                    <div class="text-sm text-slate-600">
                                        <span class="font-semibold text-emerald-600 hover:text-emerald-500">Upload a photo</span> or drag and drop
                                    </div>
                                    <p class="text-xs text-slate-400">PNG, JPG, WEBP up to 10MB</p>
                                </div>
                                <img id="photo-preview" class="hidden mx-auto h-48 w-auto object-cover rounded-lg shadow-sm" alt="Meal Preview">
                            </div>
                            <input id="meal-photo-input" type="file" accept="image/*" class="sr-only" onchange="previewImage(event)">
                        </div>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <!-- Meal Name -->
                        <div>
                            <label class="block text-sm font-semibold text-slate-700 mb-2">Meal Name <span class="text-rose-500">*</span></label>
                            <input type="text" id="meal-name" required placeholder="e.g. Creamy Garlic Pesto Pasta" class="w-full px-4 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none text-slate-800 text-sm">
                        </div>

                        <!-- Category -->
                        <div>
                            <label class="block text-sm font-semibold text-slate-700 mb-2">Category <span class="text-rose-500">*</span></label>
                            <select id="meal-category" required class="w-full px-4 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none text-slate-800 text-sm bg-white">
                                <option value="Pasta">Pasta Dish</option>
                                <option value="Rice/Noodles">Rice / Noodles Dish</option>
                                <option value="Soup/Curry">Soup / Curry</option>
                                <option value="Tacos/Wraps">Tacos / Wraps</option>
                                <option value="Seafood">Seafood</option>
                                <option value="Salad/Bowl">Salad / Grain Bowl</option>
                                <option value="Meat/Poultry">Meat / Poultry</option>
                                <option value="Breakfast">Breakfast</option>
                                <option value="Dessert">Dessert</option>
                                <option value="Other">Other</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <!-- Date -->
                        <div>
                            <label class="block text-sm font-semibold text-slate-700 mb-2">Date Cooked <span class="text-rose-500">*</span></label>
                            <input type="date" id="meal-date" required class="w-full px-4 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none text-slate-800 text-sm">
                        </div>
                        
                        <!-- Rating -->
                        <div>
                            <label class="block text-sm font-semibold text-slate-700 mb-2">Rating</label>
                            <div class="flex items-center space-x-2 pt-2" id="star-rating-container">
                                <button type="button" onclick="setRating(1)" class="text-2xl text-amber-400 star-btn" data-val="1"><i class="fa-solid fa-star"></i></button>
                                <button type="button" onclick="setRating(2)" class="text-2xl text-amber-400 star-btn" data-val="2"><i class="fa-solid fa-star"></i></button>
                                <button type="button" onclick="setRating(3)" class="text-2xl text-amber-400 star-btn" data-val="3"><i class="fa-solid fa-star"></i></button>
                                <button type="button" onclick="setRating(4)" class="text-2xl text-amber-400 star-btn" data-val="4"><i class="fa-solid fa-star"></i></button>
                                <button type="button" onclick="setRating(5)" class="text-2xl text-amber-400 star-btn" data-val="5"><i class="fa-solid fa-star"></i></button>
                                <span id="rating-text" class="text-sm text-slate-500 ml-2 font-medium">5/5 stars</span>
                            </div>
                            <input type="hidden" id="meal-rating" value="5">
                        </div>
                    </div>

                    <!-- Ingredients List -->
                    <div>
                        <label class="block text-sm font-semibold text-slate-700 mb-2">Ingredients (for Shopping List)</label>
                        <p class="text-xs text-slate-500 mb-2">List ingredients with amounts (one per line or comma-separated). These will automatically populate your weekly grocery list!</p>
                        <textarea id="meal-ingredients" rows="3" placeholder="2 cups penne pasta&#10;1 cup heavy cream&#10;3 cloves garlic, minced&#10;1/2 cup parmesan cheese" class="w-full px-4 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none text-slate-800 text-sm font-mono"></textarea>
                    </div>

                    <!-- Recipe / Notes -->
                    <div>
                        <label class="block text-sm font-semibold text-slate-700 mb-2">Recipe Instructions & Notes</label>
                        <textarea id="meal-recipe" rows="4" placeholder="Step 1: Boil pasta in salted water...&#10;Step 2: Sauté garlic in olive oil..." class="w-full px-4 py-2.5 rounded-xl border border-slate-300 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none text-slate-800 text-sm"></textarea>
                    </div>

                    <!-- Form Buttons -->
                    <div class="flex items-center justify-end space-x-4 pt-4 border-t border-slate-100">
                        <button type="button" onclick="switchTab('history')" class="px-5 py-2.5 rounded-xl border border-slate-300 text-slate-700 font-medium text-sm hover:bg-slate-50 transition-colors">Cancel</button>
                        <button type="submit" class="px-6 py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-medium text-sm shadow-sm transition-all flex items-center space-x-2">
                            <i class="fa-solid fa-floppy-disk"></i>
                            <span id="submit-btn-text">Save Meal</span>
                        </button>
                    </div>
                </form>
            </div>
        </section>

        <!-- TAB 2: MEAL HISTORY / SPREADSHEET VIEW -->
        <section id="tab-content-history" class="tab-content space-y-6">
            <!-- Top stats & filters bar -->
            <div class="bg-white p-4 sm:p-6 rounded-2xl border border-slate-200 shadow-xs flex flex-col lg:flex-row justify-between items-stretch lg:items-center gap-4">
                <div class="flex flex-wrap items-center gap-3">
                    <!-- Search bar -->
                    <div class="relative flex-1 sm:w-72">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                            <i class="fa-solid fa-magnifying-glass text-sm"></i>
                        </span>
                        <input type="text" id="search-input" oninput="renderHistoryTable()" placeholder="Search meals, ingredients..." class="w-full pl-10 pr-4 py-2 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-emerald-500 outline-none">
                    </div>
                    <!-- Category Filter -->
                    <select id="filter-category" onchange="renderHistoryTable()" class="px-3 py-2 rounded-xl border border-slate-300 text-sm bg-white text-slate-700 focus:ring-2 focus:ring-emerald-500 outline-none">
                        <option value="">All Categories</option>
                        <option value="Pasta">Pasta Dish</option>
                        <option value="Rice/Noodles">Rice / Noodles Dish</option>
                        <option value="Soup/Curry">Soup / Curry</option>
                        <option value="Tacos/Wraps">Tacos / Wraps</option>
                        <option value="Seafood">Seafood</option>
                        <option value="Salad/Bowl">Salad / Grain Bowl</option>
                        <option value="Meat/Poultry">Meat / Poultry</option>
                        <option value="Breakfast">Breakfast</option>
                        <option value="Dessert">Dessert</option>
                        <option value="Other">Other</option>
                    </select>
                </div>
                
                <div class="flex items-center space-x-3">
                    <button onclick="exportDataCSV()" class="px-4 py-2 rounded-xl border border-slate-300 hover:bg-slate-50 text-slate-700 text-sm font-medium transition-colors flex items-center space-x-2">
                        <i class="fa-solid fa-file-csv text-emerald-600"></i>
                        <span>Export CSV</span>
                    </button>
                    <button onclick="openLogModal()" class="px-4 py-2 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-medium shadow-sm transition-colors flex items-center space-x-2">
                        <i class="fa-solid fa-plus"></i>
                        <span>Log Meal</span>
                    </button>
                </div>
            </div>

            <!-- Spreadsheet Table View -->
            <div class="bg-white rounded-2xl border border-slate-200 shadow-xs overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-50 border-b border-slate-200 text-xs font-semibold text-slate-500 uppercase tracking-wider">
                                <th class="py-3.5 px-4">Photo</th>
                                <th class="py-3.5 px-4">Meal Name</th>
                                <th class="py-3.5 px-4">Category</th>
                                <th class="py-3.5 px-4">Date Cooked</th>
                                <th class="py-3.5 px-4">Rating</th>
                                <th class="py-3.5 px-4">Recipe & Ingredients</th>
                                <th class="py-3.5 px-4 text-right">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="meals-table-body" class="divide-y divide-slate-100 text-sm">
                            <!-- Populated dynamically -->
                        </tbody>
                    </table>
                </div>
                <!-- Empty State -->
                <div id="empty-history" class="hidden py-16 text-center">
                    <div class="w-16 h-16 bg-emerald-50 text-emerald-500 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl">
                        <i class="fa-solid fa-bowl-food"></i>
                    </div>
                    <h3 class="text-base font-bold text-slate-800">No meals logged yet</h3>
                    <p class="text-sm text-slate-500 mt-1 mb-4">Start capturing your culinary creations to build your spreadsheet.</p>
                    <button onclick="openLogModal()" class="px-4 py-2 bg-emerald-600 text-white rounded-xl text-sm font-medium hover:bg-emerald-700">Log Your First Meal</button>
                </div>
            </div>
        </section>

        <!-- TAB 3: WEEKLY PLANNER VIEW -->
        <section id="tab-content-planner" class="tab-content hidden space-y-6">
            <!-- Planner Header & Week selector -->
            <div class="bg-white p-4 sm:p-6 rounded-2xl border border-slate-200 shadow-xs flex flex-col sm:flex-row justify-between items-center gap-4">
                <div>
                    <h2 class="text-xl font-bold text-slate-900">Weekly Meal Planner</h2>
                    <p class="text-sm text-slate-500 mt-0.5">Organize your week by assigning logged meals to specific days.</p>
                </div>
                <div class="flex items-center space-x-3">
                    <button onclick="changeWeek(-1)" class="p-2 rounded-xl border border-slate-300 hover:bg-slate-50 text-slate-600">
                        <i class="fa-solid fa-chevron-left"></i>
                    </button>
                    <span id="current-week-label" class="font-semibold text-slate-800 text-sm px-2">Week of Oct 4 - Oct 10, 2026</span>
                    <button onclick="changeWeek(1)" class="p-2 rounded-xl border border-slate-300 hover:bg-slate-50 text-slate-600">
                        <i class="fa-solid fa-chevron-right"></i>
                    </button>
                    <button onclick="generateGroceryListFromPlanner()" class="ml-2 px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-medium rounded-xl shadow-xs transition-colors flex items-center space-x-2">
                        <i class="fa-solid fa-cart-shopping"></i>
                        <span>Generate Grocery List</span>
                    </button>
                </div>
            </div>

            <!-- Planner Days Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-7 gap-4" id="planner-days-grid">
                <!-- Dynamically populated days (Mon-Sun) -->
            </div>
        </section>

        <!-- TAB 4: SMART GROCERY LIST VIEW -->
        <section id="tab-content-grocery" class="tab-content hidden space-y-6">
            <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-xs flex flex-col sm:flex-row justify-between items-stretch sm:items-center gap-4">
                <div>
                    <h2 class="text-xl font-bold text-slate-900">Smart Grocery List</h2>
                    <p class="text-sm text-slate-500 mt-1">Aggregated ingredients from your active weekly meal plan.</p>
                </div>
                <div class="flex items-center space-x-3">
                    <button onclick="addCustomGroceryItemPrompt()" class="px-4 py-2 rounded-xl border border-slate-300 hover:bg-slate-50 text-slate-700 text-sm font-medium transition-colors flex items-center space-x-2">
                        <i class="fa-solid fa-plus text-emerald-600"></i>
                        <span>Add Item</span>
                    </button>
                    <button onclick="clearCheckedGroceries()" class="px-4 py-2 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-700 text-sm font-medium transition-colors">
                        Clear Checked
                    </button>
                </div>
            </div>

            <div class="bg-white rounded-2xl border border-slate-200 shadow-xs p-6">
                <div id="grocery-list-container" class="space-y-3">
                    <!-- Populated dynamically -->
                </div>
                <div id="empty-grocery" class="hidden py-16 text-center">
                    <div class="w-16 h-16 bg-emerald-50 text-emerald-500 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl">
                        <i class="fa-solid fa-basket-shopping"></i>
                    </div>
                    <h3 class="text-base font-bold text-slate-800">Your grocery list is empty</h3>
                    <p class="text-sm text-slate-500 mt-1 mb-4">Go to the Weekly Planner and click "Generate Grocery List" or add items manually.</p>
                    <button onclick="switchTab('planner')" class="px-4 py-2 bg-emerald-600 text-white rounded-xl text-sm font-medium hover:bg-emerald-700">Go to Planner</button>
                </div>
            </div>
        </section>

    </main>

    <!-- RECIPE VIEW MODAL -->
    <div id="recipe-modal" class="fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-xs flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-xl w-full max-h-[90vh] overflow-y-auto shadow-xl border border-slate-100">
            <div id="recipe-modal-content" class="p-6 sm:p-8 space-y-6">
                <!-- Dynamically filled -->
            </div>
        </div>
    </div>

    <!-- ASSIGN MEAL TO PLANNER MODAL -->
    <div id="assign-modal" class="fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-xs flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-xl border border-slate-100 space-y-4">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-lg text-slate-900" id="assign-modal-title">Plan Meal for Day</h3>
                <button onclick="closeAssignModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <p class="text-sm text-slate-500">Choose a previously logged meal or type a custom meal name.</p>
            
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 mb-2">Select from Logged Meals</label>
                    <select id="assign-existing-select" class="w-full px-3 py-2 rounded-xl border border-slate-300 text-sm bg-white text-slate-700 focus:ring-2 focus:ring-emerald-500 outline-none">
                        <option value="">-- Choose Logged Meal --</option>
                    </select>
                </div>
                <div class="relative flex py-2 items-center">
                    <div class="flex-grow border-t border-slate-200"></div>
                    <span class="flex-shrink mx-4 text-slate-400 text-xs uppercase font-semibold">Or custom</span>
                    <div class="flex-grow border-t border-slate-200"></div>
                </div>
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 mb-2">Custom Meal Name</label>
                    <input type="text" id="assign-custom-input" placeholder="e.g. Leftover Pizza" class="w-full px-3 py-2 rounded-xl border border-slate-300 text-sm outline-none focus:ring-2 focus:ring-emerald-500">
                </div>
            </div>

            <div class="flex justify-end space-x-3 pt-2">
                <button onclick="closeAssignModal()" class="px-4 py-2 rounded-xl border border-slate-300 text-sm font-medium text-slate-700 hover:bg-slate-50">Cancel</button>
                <button onclick="confirmAssignMeal()" class="px-4 py-2 rounded-xl bg-emerald-600 text-white text-sm font-medium hover:bg-emerald-700">Assign to Day</button>
            </div>
        </div>
    </div>

    <!-- CUSTOM GROCERY ITEM MODAL -->
    <div id="grocery-modal" class="fixed inset-0 z-50 bg-slate-900/50 backdrop-blur-xs flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-sm w-full p-6 shadow-xl border border-slate-100 space-y-4">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-lg text-slate-900">Add Grocery Item</h3>
                <button onclick="closeGroceryModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 mb-2">Item Name & Amount</label>
                <input type="text" id="custom-grocery-input" placeholder="e.g. Almond milk 1 gal" class="w-full px-3 py-2 rounded-xl border border-slate-300 text-sm outline-none focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="flex justify-end space-x-3 pt-2">
                <button onclick="closeGroceryModal()" class="px-4 py-2 rounded-xl border border-slate-300 text-sm font-medium text-slate-700 hover:bg-slate-50">Cancel</button>
                <button onclick="confirmAddGroceryItem()" class="px-4 py-2 rounded-xl bg-emerald-600 text-white text-sm font-medium hover:bg-emerald-700">Add Item</button>
            </div>
        </div>
    </div>

    <!-- NOTIFICATION TOAST -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 bg-slate-900 text-white px-4 py-3 rounded-xl shadow-xl flex items-center space-x-3 text-sm">
        <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-message">Action successful!</span>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // --- State Management ---
        let meals = JSON.parse(localStorage.getItem('mp_meals')) || [
            {
                id: 'meal-1',
                name: 'Creamy Garlic Pesto Pasta',
                category: 'Pasta',
                date: '2026-10-05',
                rating: 5,
                photo: 'https://placehold.co/600x400/10b981/ffffff?text=Pesto+Pasta',
                ingredients: '2 cups penne pasta\n1 cup heavy cream\n3 cloves garlic, minced\n1/2 cup parmesan cheese\n3 tbsp basil pesto',
                recipe: '1. Boil penne pasta in salted water until al dente.\n2. In a skillet, sauté minced garlic in olive oil.\n3. Stir in heavy cream and pesto, simmer for 5 minutes.\n4. Toss pasta in sauce and top with parmesan cheese.'
            },
            {
                id: 'meal-2',
                name: 'Shrimp & Veggie Stir Fry Noodles',
                category: 'Rice/Noodles',
                date: '2026-10-06',
                rating: 4,
                photo: 'https://placehold.co/600x400/0ea5e9/ffffff?text=Noodles',
                ingredients: '8oz egg noodles\n1 lb peeled shrimp\n2 cups broccoli florets\n1 bell pepper, sliced\n3 tbsp soy sauce\n1 tbsp sesame oil',
                recipe: '1. Cook noodles according to package instructions.\n2. Stir fry shrimp in sesame oil until pink, remove.\n3. Stir fry broccoli and bell pepper until tender-crisp.\n4. Combine noodles, shrimp, and veggies with soy sauce.'
            }
        ];

        let weeklyPlans = JSON.parse(localStorage.getItem('mp_weekly_plans')) || {
            '2026-W41': {
                'Monday': [{ type: 'logged', id: 'meal-1', name: 'Creamy Garlic Pesto Pasta' }],
                'Tuesday': [],
                'Wednesday': [{ type: 'logged', id: 'meal-2', name: 'Shrimp & Veggie Stir Fry Noodles' }],
                'Thursday': [],
                'Friday': [{ type: 'custom', name: 'Homemade Margherita Pizza' }],
                'Saturday': [],
                'Sunday': []
            }
        };

        let groceryList = JSON.parse(localStorage.getItem('mp_grocery_list')) || [
            { id: 'g-1', text: '2 cups penne pasta', checked: false, source: 'Creamy Garlic Pesto Pasta' },
            { id: 'g-2', text: '1 cup heavy cream', checked: true, source: 'Creamy Garlic Pesto Pasta' },
            { id: 'g-3', text: '8oz egg noodles', checked: false, source: 'Shrimp & Veggie Stir Fry Noodles' }
        ];

        let currentWeekKey = '2026-W41';
        let currentEditingMealId = null;
        let activeAssignDay = null;
        let base64ImageCache = '';

        // --- Initialization ---
        window.addEventListener('DOMContentLoaded', () => {
            // Set default date to today
            document.getElementById('meal-date').valueAsDate = new Date();
            renderHistoryTable();
            renderWeeklyPlanner();
            renderGroceryList();
        });

        // --- Tab Navigation ---
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`tab-content-${tabId}`).classList.remove('hidden');

            // Desktop tab buttons
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-white', 'text-emerald-600', 'shadow-xs');
                btn.classList.add('text-slate-700');
            });
            const activeBtn = document.getElementById(`nav-${tabId}`);
            if (activeBtn) {
                activeBtn.classList.remove('text-slate-700');
                activeBtn.classList.add('bg-white', 'text-emerald-600', 'shadow-xs');
            }

            // Mobile tab buttons
            document.querySelectorAll('.mobile-tab').forEach(btn => {
                btn.classList.remove('text-emerald-600', 'border-emerald-600');
                btn.classList.add('text-slate-500', 'border-transparent');
            });
            const activeMob = document.getElementById(`mob-nav-${tabId}`);
            if (activeMob) {
                activeMob.classList.remove('text-slate-500', 'border-transparent');
                activeMob.classList.add('text-emerald-600', 'border-emerald-600');
            }

            if (tabId === 'history') renderHistoryTable();
            if (tabId === 'planner') renderWeeklyPlanner();
            if (tabId === 'grocery') renderGroceryList();
        }

        function openLogModal() {
            currentEditingMealId = null;
            document.getElementById('meal-form').reset();
            document.getElementById('meal-date').valueAsDate = new Date();
            document.getElementById('photo-preview').classList.add('hidden');
            document.getElementById('photo-placeholder').classList.remove('hidden');
            base64ImageCache = '';
            document.getElementById('submit-btn-text').innerText = 'Save Meal';
            setRating(5);
            switchTab('log');
        }

        // --- Toast Notification ---
        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            const msgEl = document.getElementById('toast-message');
            const iconEl = document.getElementById('toast-icon');
            
            msgEl.innerText = message;
            if(type === 'success') {
                iconEl.className = 'fa-solid fa-circle-check text-emerald-400';
            } else {
                iconEl.className = 'fa-solid fa-circle-exclamation text-amber-400';
            }

            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3500);
        }

        // --- Image Preview Handler ---
        function previewImage(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    base64ImageCache = e.target.result;
                    const preview = document.getElementById('photo-preview');
                    preview.src = base64ImageCache;
                    preview.classList.remove('hidden');
                    document.getElementById('photo-placeholder').classList.add('hidden');
                }
                reader.readAsDataURL(file);
            }
        }

        // --- Star Rating ---
        function setRating(val) {
            document.getElementById('meal-rating').value = val;
            document.getElementById('rating-text').innerText = `${val}/5 stars`;
            const buttons = document.querySelectorAll('.star-btn');
            buttons.forEach(btn => {
                const bVal = parseInt(btn.getAttribute('data-val'));
                if(bVal <= val) {
                    btn.classList.remove('text-slate-300');
                    btn.classList.add('text-amber-400');
                } else {
                    btn.classList.remove('text-amber-400');
                    btn.classList.add('text-slate-300');
                }
            });
        }

        // --- Handle Meal Submit ---
        function handleMealSubmit(e) {
            e.preventDefault();
            const name = document.getElementById('meal-name').value.trim();
            const category = document.getElementById('meal-category').value;
            const date = document.getElementById('meal-date').value;
            const rating = parseInt(document.getElementById('meal-rating').value);
            const ingredients = document.getElementById('meal-ingredients').value.trim();
            const recipe = document.getElementById('meal-recipe').value.trim();

            let photo = base64ImageCache;
            if (!photo) {
                // Fallback default placeholder based on category
                photo = `https://placehold.co/600x400/10b981/ffffff?text=${encodeURIComponent(name)}`;
            }

            if (currentEditingMealId) {
                // Edit existing
                const index = meals.findIndex(m => m.id === currentEditingMealId);
                if (index !== -1) {
                    meals[index] = {
                        ...meals[index],
                        name, category, date, rating, ingredients, recipe,
                        photo: base64ImageCache ? base64ImageCache : meals[index].photo
                    };
                }
                showToast('Meal successfully updated!');
                currentEditingMealId = null;
            } else {
                // Create new
                const newMeal = {
                    id: 'meal-' + Date.now(),
                    name, category, date, rating, photo, ingredients, recipe
                };
                meals.unshift(newMeal);
                showToast('Meal successfully logged and saved!');
            }

            localStorage.setItem('mp_meals', JSON.stringify(meals));
            switchTab('history');
        }

        // --- Render History Table ---
        function renderHistoryTable() {
            const tbody = document.getElementById('meals-table-body');
            const emptyState = document.getElementById('empty-history');
            const searchTerm = document.getElementById('search-input').value.toLowerCase();
            const categoryFilter = document.getElementById('filter-category').value;

            tbody.innerHTML = '';

            const filtered = meals.filter(m => {
                const matchesSearch = m.name.toLowerCase().includes(searchTerm) || 
                                      (m.ingredients && m.ingredients.toLowerCase().includes(searchTerm)) ||
                                      (m.recipe && m.recipe.toLowerCase().includes(searchTerm));
                const matchesCategory = categoryFilter === '' || m.category === categoryFilter;
                return matchesSearch && matchesCategory;
            });

            if (filtered.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            filtered.forEach(m => {
                const tr = document.createElement('tr');
                tr.className = 'hover:bg-slate-50/80 transition-colors border-b border-slate-100';

                // Category badge color mapping
                let badgeColor = 'bg-emerald-50 text-emerald-700 border-emerald-200';
                if(m.category.includes('Rice')) badgeColor = 'bg-sky-50 text-sky-700 border-sky-200';
                if(m.category.includes('Soup')) badgeColor = 'bg-amber-50 text-amber-700 border-amber-200';
                if(m.category.includes('Tacos')) badgeColor = 'bg-rose-50 text-rose-700 border-rose-200';
                if(m.category.includes('Seafood')) badgeColor = 'bg-indigo-50 text-indigo-700 border-indigo-200';

                tr.innerHTML = `
                    <td class="py-3 px-4">
                        <img src="${m.photo}" alt="${m.name}" class="w-12 h-12 object-cover rounded-xl shadow-xs border border-slate-200">
                    </td>
                    <td class="py-3 px-4 font-semibold text-slate-900">${m.name}</td>
                    <td class="py-3 px-4">
                        <span class="px-2.5 py-1 rounded-full text-xs font-medium border ${badgeColor}">${m.category}</span>
                    </td>
                    <td class="py-3 px-4 text-slate-600 text-xs">${m.date}</td>
                    <td class="py-3 px-4 text-amber-400">
                        ${'★'.repeat(m.rating)}${'☆'.repeat(5 - m.rating)}
                    </td>
                    <td class="py-3 px-4 text-slate-500 text-xs max-w-xs truncate">
                        ${m.ingredients ? m.ingredients.replace(/\n/g, ', ') : 'No ingredients listed'}
                    </td>
                    <td class="py-3 px-4 text-right space-x-2">
                        <button onclick="viewRecipeModal('${m.id}')" title="View Recipe" class="p-2 text-slate-400 hover:text-emerald-600 transition-colors"><i class="fa-solid fa-book-open"></i></button>
                        <button onclick="editMeal('${m.id}')" title="Edit Meal" class="p-2 text-slate-400 hover:text-sky-600 transition-colors"><i class="fa-solid fa-pen-to-square"></i></button>
                        <button onclick="deleteMeal('${m.id}')" title="Delete Meal" class="p-2 text-slate-400 hover:text-rose-600 transition-colors"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        // --- Recipe Modal ---
        function viewRecipeModal(id) {
            const m = meals.find(item => item.id === id);
            if(!m) return;

            const content = document.getElementById('recipe-modal-content');
            content.innerHTML = `
                <div class="flex justify-between items-start">
                    <div>
                        <span class="px-2.5 py-1 rounded-full text-xs font-medium bg-emerald-50 text-emerald-700 border border-emerald-200">${m.category}</span>
                        <h2 class="text-2xl font-bold text-slate-900 mt-2">${m.name}</h2>
                        <p class="text-xs text-slate-500 mt-0.5">Cooked on ${m.date} • Rating: ${m.rating}/5 stars</p>
                    </div>
                    <button onclick="closeRecipeModal()" class="text-slate-400 hover:text-slate-600 p-1"><i class="fa-solid fa-xmark text-xl"></i></button>
                </div>
                
                <img src="${m.photo}" alt="${m.name}" class="w-full h-64 object-cover rounded-xl shadow-md border border-slate-200">

                <div>
                    <h4 class="text-xs font-semibold uppercase tracking-wider text-slate-400 mb-2">Ingredients</h4>
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 font-mono text-sm text-slate-700 whitespace-pre-line">${m.ingredients || 'No ingredients listed.'}</div>
                </div>

                <div>
                    <h4 class="text-xs font-semibold uppercase tracking-wider text-slate-400 mb-2">Recipe & Instructions</h4>
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 text-sm text-slate-700 whitespace-pre-line">${m.recipe || 'No recipe instructions provided.'}</div>
                </div>

                <div class="flex justify-end pt-4 border-t border-slate-100">
                    <button onclick="closeRecipeModal()" class="px-5 py-2.5 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-sm font-medium">Close</button>
                </div>
            `;
            document.getElementById('recipe-modal').classList.remove('hidden');
        }

        function closeRecipeModal() {
            document.getElementById('recipe-modal').classList.add('hidden');
        }

        // --- Edit / Delete Meal ---
        function editMeal(id) {
            const m = meals.find(item => item.id === id);
            if(!m) return;

            currentEditingMealId = m.id;
            document.getElementById('meal-name').value = m.name;
            document.getElementById('meal-category').value = m.category;
            document.getElementById('meal-date').value = m.date;
            setRating(m.rating);
            document.getElementById('meal-ingredients').value = m.ingredients || '';
            document.getElementById('meal-recipe').value = m.recipe || '';

            base64ImageCache = m.photo;
            const preview = document.getElementById('photo-preview');
            preview.src = m.photo;
            preview.classList.remove('hidden');
            document.getElementById('photo-placeholder').classList.add('hidden');

            document.getElementById('submit-btn-text').innerText = 'Update Meal';
            switchTab('log');
        }

        function deleteMeal(id) {
            if(confirm('Are you sure you want to delete this logged meal?')) {
                meals = meals.filter(m => m.id !== id);
                localStorage.setItem('mp_meals', JSON.stringify(meals));
                renderHistoryTable();
                showToast('Meal deleted successfully.', 'info');
            }
        }

        // --- Export CSV ---
        function exportDataCSV() {
            if (meals.length === 0) {
                showToast('No meals to export!', 'error');
                return;
            }
            let csv = 'ID,Name,Category,Date,Rating,Ingredients,Recipe\n';
            meals.forEach(m => {
                const ingClean = (m.ingredients || '').replace(/\n/g, ' | ').replace(/"/g, '""');
                const recClean = (m.recipe || '').replace(/\n/g, ' | ').replace(/"/g, '""');
                csv += `"${m.id}","${m.name}","${m.category}","${m.date}","${m.rating}","${ingClean}","${recClean}"\n`;
            });
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.setAttribute('href', url);
            a.setAttribute('download', `meal_history_${new Date().toISOString().slice(0,10)}.csv`);
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            showToast('Meal history exported to CSV!');
        }

        // --- Weekly Planner Logic ---
        const daysOfWeek = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];

        function changeWeek(direction) {
            // Simple week key increment/decrement simulation for demo
            let weekNum = parseInt(currentWeekKey.split('-W')[1]);
            weekNum += direction;
            if(weekNum < 1) weekNum = 52;
            if(weekNum > 52) weekNum = 1;
            currentWeekKey = `2026-W${weekNum < 10 ? '0'+weekNum : weekNum}`;
            document.getElementById('current-week-label').innerText = `Week ${weekNum} (2026)`;
            renderWeeklyPlanner();
        }

        function renderWeeklyPlanner() {
            const grid = document.getElementById('planner-days-grid');
            grid.innerHTML = '';

            if(!weeklyPlans[currentWeekKey]) {
                weeklyPlans[currentWeekKey] = {
                    'Monday': [], 'Tuesday': [], 'Wednesday': [], 'Thursday': [], 'Friday': [], 'Saturday': [], 'Sunday': []
                };
            }

            daysOfWeek.forEach(day => {
                const dayPlan = weeklyPlans[currentWeekKey][day] || [];
                const col = document.createElement('div');
                col.className = 'bg-white rounded-2xl border border-slate-200 shadow-xs flex flex-col overflow-hidden';

                let itemsHtml = '';
                dayPlan.forEach((item, idx) => {
                    itemsHtml += `
                        <div class="bg-emerald-50/80 border border-emerald-200/60 rounded-xl p-2.5 text-xs text-slate-800 flex items-center justify-between group">
                            <span class="font-medium truncate mr-2"><i class="fa-solid fa-utensils text-emerald-600 mr-1.5"></i>${item.name}</span>
                            <button onclick="removeMealFromPlan('${day}', ${idx})" class="text-slate-400 hover:text-rose-600 transition-colors"><i class="fa-solid fa-xmark"></i></button>
                        </div>
                    `;
                });

                col.innerHTML = `
                    <div class="bg-slate-50 px-4 py-3 border-b border-slate-200 flex justify-between items-center">
                        <span class="font-bold text-sm text-slate-800">${day}</span>
                        <button onclick="openAssignModal('${day}')" class="w-7 h-7 rounded-lg bg-white border border-slate-300 text-slate-600 hover:bg-emerald-600 hover:text-white hover:border-emerald-600 transition-colors flex items-center justify-center text-xs shadow-xs">
                            <i class="fa-solid fa-plus"></i>
                        </button>
                    </div>
                    <div class="p-3 flex-1 space-y-2 min-h-[140px] flex flex-col justify-between">
                        <div class="space-y-2">
                            ${itemsHtml.length > 0 ? itemsHtml : '<p class="text-xs text-slate-400 italic text-center py-6">No meals planned</p>'}
                        </div>
                        <button onclick="openAssignModal('${day}')" class="w-full py-1.5 border border-dashed border-slate-300 hover:border-emerald-500 rounded-xl text-xs text-slate-500 hover:text-emerald-600 transition-colors">
                            + Add Meal
                        </button>
                    </div>
                `;
                grid.appendChild(col);
            });
        }

        function openAssignModal(day) {
            activeAssignDay = day;
            document.getElementById('assign-modal-title').innerText = `Plan Meal for ${day}`;
            document.getElementById('assign-custom-input').value = '';

            const select = document.getElementById('assign-existing-select');
            select.innerHTML = '<option value="">-- Choose Logged Meal --</option>';
            meals.forEach(m => {
                const opt = document.createElement('option');
                opt.value = m.id;
                opt.text = `${m.name} (${m.category})`;
                select.appendChild(opt);
            });

            document.getElementById('assign-modal').classList.remove('hidden');
        }

        function closeAssignModal() {
            document.getElementById('assign-modal').classList.add('hidden');
            activeAssignDay = null;
        }

        function confirmAssignMeal() {
            const existingId = document.getElementById('assign-existing-select').value;
            const customName = document.getElementById('assign-custom-input').value.trim();

            let mealToAdd = null;
            if(existingId) {
                const found = meals.find(m => m.id === existingId);
                if(found) {
                    mealToAdd = { type: 'logged', id: found.id, name: found.name };
                }
            } else if(customName) {
                mealToAdd = { type: 'custom', name: customName };
            }

            if(!mealToAdd) {
                showToast('Please select a logged meal or enter a custom name.', 'error');
                return;
            }

            if(!weeklyPlans[currentWeekKey]) {
                weeklyPlans[currentWeekKey] = { 'Monday': [], 'Tuesday': [], 'Wednesday': [], 'Thursday': [], 'Friday': [], 'Saturday': [], 'Sunday': [] };
            }

            weeklyPlans[currentWeekKey][activeAssignDay].push(mealToAdd);
            localStorage.setItem('mp_weekly_plans', JSON.stringify(weeklyPlans));
            closeAssignModal();
            renderWeeklyPlanner();
            showToast(`Meal added to ${activeAssignDay}!`);
        }

        function removeMealFromPlan(day, idx) {
            if(weeklyPlans[currentWeekKey] && weeklyPlans[currentWeekKey][day]) {
                weeklyPlans[currentWeekKey][day].splice(idx, 1);
                localStorage.setItem('mp_weekly_plans', JSON.stringify(weeklyPlans));
                renderWeeklyPlanner();
                showToast('Meal removed from plan.', 'info');
            }
        }

        // --- Smart Grocery List Generation ---
        function generateGroceryListFromPlanner() {
            const currentPlan = weeklyPlans[currentWeekKey];
            if(!currentPlan) {
                showToast('No meals planned for this week!', 'error');
                return;
            }

            let newItems = [];
            let countAdded = 0;

            daysOfWeek.forEach(day => {
                const dayMeals = currentPlan[day] || [];
                dayMeals.forEach(item => {
                    if(item.type === 'logged') {
                        const loggedMeal = meals.find(m => m.id === item.id);
                        if(loggedMeal && loggedMeal.ingredients) {
                            const lines = loggedMeal.ingredients.split('\n');
                            lines.forEach(line => {
                                const clean = line.trim();
                                if(clean) {
                                    newItems.push({
                                        id: 'g-' + Math.random().toString(36).substring(2, 9),
                                        text: clean,
                                        checked: false,
                                        source: loggedMeal.name
                                    });
                                    countAdded++;
                                }
                            });
                        }
                    } else if(item.type === 'custom') {
                        newItems.push({
                            id: 'g-' + Math.random().toString(36).substring(2, 9),
                            text: `Ingredients for ${item.name}`,
                            checked: false,
                            source: item.name
                        });
                        countAdded++;
                    }
                });
            });

            if(newItems.length === 0) {
                showToast('No ingredients found in planned meals.', 'info');
                return;
            }

            // Merge or replace
            groceryList = [...newItems, ...groceryList];
            localStorage.setItem('mp_grocery_list', JSON.stringify(groceryList));
            switchTab('grocery');
            showToast(`Generated grocery list with ${countAdded} items!`);
        }

        function renderGroceryList() {
            const container = document.getElementById('grocery-list-container');
            const emptyState = document.getElementById('empty-grocery');
            container.innerHTML = '';

            if(groceryList.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            groceryList.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = `flex items-center justify-between p-3.5 rounded-xl border transition-all ${item.checked ? 'bg-slate-50 border-slate-200 opacity-60 line-through' : 'bg-white border-slate-200 shadow-xs'}`;
                
                div.innerHTML = `
                    <label class="flex items-center space-x-3 cursor-pointer flex-1">
                        <input type="checkbox" ${item.checked ? 'checked' : ''} onchange="toggleGroceryItem('${item.id}')" class="w-4 h-4 rounded text-emerald-600 focus:ring-emerald-500 border-slate-300">
                        <span class="text-sm font-medium text-slate-800">${item.text}</span>
                        ${item.source ? `<span class="text-xs bg-emerald-50 text-emerald-700 px-2 py-0.5 rounded-full border border-emerald-200 font-normal">from ${item.source}</span>` : ''}
                    </label>
                    <button onclick="deleteGroceryItem('${item.id}')" class="text-slate-400 hover:text-rose-600 transition-colors p-1"><i class="fa-solid fa-trash text-xs"></i></button>
                `;
                container.appendChild(div);
            });
        }

        function toggleGroceryItem(id) {
            const item = groceryList.find(g => g.id === id);
            if(item) {
                item.checked = !item.checked;
                localStorage.setItem('mp_grocery_list', JSON.stringify(groceryList));
                renderGroceryList();
            }
        }

        function deleteGroceryItem(id) {
            groceryList = groceryList.filter(g => g.id !== id);
            localStorage.setItem('mp_grocery_list', JSON.stringify(groceryList));
            renderGroceryList();
        }

        function clearCheckedGroceries() {
            groceryList = groceryList.filter(g => !g.checked);
            localStorage.setItem('mp_grocery_list', JSON.stringify(groceryList));
            renderGroceryList();
            showToast('Checked items cleared.', 'info');
        }

        function addCustomGroceryItemPrompt() {
            document.getElementById('custom-grocery-input').value = '';
            document.getElementById('grocery-modal').classList.remove('hidden');
        }

        function closeGroceryModal() {
            document.getElementById('grocery-modal').classList.add('hidden');
        }

        function confirmAddGroceryItem() {
            const val = document.getElementById('custom-grocery-input').value.trim();
            if(!val) return;

            groceryList.unshift({
                id: 'g-' + Date.now(),
                text: val,
                checked: false,
                source: 'Manual Add'
            });
            localStorage.setItem('mp_grocery_list', JSON.stringify(groceryList));
            closeGroceryModal();
            renderGroceryList();
            showToast('Grocery item added!');
        }
    </script>
</body>
</html>
```
