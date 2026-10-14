<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>HisabKitab — Daily Expense & Budget Tracker</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter & JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@500;600;700&display=swap" rel="stylesheet">
  <!-- Phosphor Icons -->
  <script src="https://unpkg.com/@phosphor-icons/web"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
          colors: {
            emerald: {
              450: '#10b981',
            }
          },
          animation: {
            'blob': 'blob 12s infinite alternate ease-in-out',
          },
          keyframes: {
            blob: {
              '0%': { transform: 'translate(0px, 0px) scale(1)' },
              '33%': { transform: 'translate(40px, -50px) scale(1.15)' },
              '66%': { transform: 'translate(-30px, 30px) scale(0.9)' },
              '100%': { transform: 'translate(20px, -20px) scale(1.05)' },
            }
          }
        }
      }
    }
  </script>
  <style>
    /* Custom scrollbars & transitions */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: transparent;
    }
    ::-webkit-scrollbar-thumb {
      background: rgba(100, 116, 139, 0.25);
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: rgba(71, 85, 105, 0.45);
    }

    /* Hide scrollbar for horizontal pill lists */
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }

    /* Smooth SVG ring transition */
    .donut-segment {
      transition: stroke-dasharray 0.5s cubic-bezier(0.4, 0, 0.2, 1), stroke-dashoffset 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    }

    /* Official Light Pastel & Subtle Geometric Background */
    .aurora-bg {
      background-color: #f8fafc;
      background-image: 
        radial-gradient(at 0% 0%, rgba(224, 242, 254, 0.75) 0px, transparent 50%),
        radial-gradient(at 100% 0%, rgba(238, 242, 255, 0.75) 0px, transparent 50%),
        radial-gradient(at 100% 100%, rgba(209, 250, 229, 0.55) 0px, transparent 50%),
        radial-gradient(at 0% 100%, rgba(254, 243, 199, 0.55) 0px, transparent 50%),
        url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%2364748b' fill-opacity='0.04' fill-rule='evenodd'%3E%3Cpath d='M0 40L40 0H20L0 20M40 40V20L20 40'/%3E%3C/g%3E%3C/svg%3E");
      background-attachment: fixed;
    }
    .dark .aurora-bg {
      background-color: #0f172a;
      background-image: 
        radial-gradient(at 10% 10%, rgba(56, 189, 248, 0.08) 0px, transparent 55%),
        radial-gradient(at 90% 15%, rgba(99, 102, 241, 0.08) 0px, transparent 55%),
        radial-gradient(at 80% 90%, rgba(16, 185, 129, 0.06) 0px, transparent 55%),
        url("data:image/svg+xml,%3Csvg width='40' height='40' viewBox='0 0 40 40' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%2394a3b8' fill-opacity='0.04' fill-rule='evenodd'%3E%3Cpath d='M0 40L40 0H20L0 20M40 40V20L20 40'/%3E%3C/g%3E%3C/svg%3E");
      background-attachment: fixed;
    }

    /* Clean Official Frosted Card Effect */
    .glass-card {
      background: rgba(255, 255, 255, 0.92);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(226, 232, 240, 0.95);
      box-shadow: 0 4px 20px -2px rgba(15, 23, 42, 0.04), 0 2px 6px -1px rgba(15, 23, 42, 0.02);
    }
    .dark .glass-card {
      background: rgba(30, 41, 59, 0.80);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(51, 65, 85, 0.8);
      box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
    }

    @media print {
/* ... existing code ... -->
      .no-print {
        display: none !important;
      }
    }
  </style>
</head>
<body class="aurora-bg text-slate-800 dark:text-slate-100 font-sans antialiased selection:bg-sky-500 selection:text-white transition-colors duration-300 min-h-screen flex flex-col lg:flex-row relative overflow-x-hidden">

  <!-- ======================= SOFT PASTEL AMBIENT BACKGROUND ORBS ======================= -->
  <div class="fixed inset-0 overflow-hidden pointer-events-none z-0">
    <div class="absolute -top-28 -left-28 w-96 h-96 bg-sky-200/45 dark:bg-sky-500/10 rounded-full blur-3xl animate-blob"></div>
    <div class="absolute top-1/3 -right-28 w-96 h-96 bg-indigo-200/40 dark:bg-indigo-500/10 rounded-full blur-3xl animate-blob" style="animation-delay: 3s;"></div>
    <div class="absolute -bottom-28 left-1/4 w-96 h-96 bg-emerald-200/40 dark:bg-teal-500/10 rounded-full blur-3xl animate-blob" style="animation-delay: 6s;"></div>
  </div>

  <!-- ======================= DESKTOP SIDEBAR ======================= -->
  <aside class="hidden lg:flex lg:flex-col lg:w-72 lg:fixed lg:inset-y-0 glass-card border-r border-slate-200/90 dark:border-slate-800 z-30 select-none">
    <!-- Brand Logo -->
    <div class="p-6 flex items-center justify-between border-b border-slate-200/70 dark:border-slate-800">
      <div class="flex items-center gap-3">
        <div class="w-11 h-11 rounded-2xl bg-gradient-to-tr from-sky-600 to-indigo-600 flex items-center justify-center text-white shadow-md shadow-sky-500/20 ring-2 ring-sky-100 dark:ring-slate-700">
          <i class="ph-bold ph-wallet text-2xl"></i>
        </div>
        <div>
          <h1 class="font-extrabold text-lg tracking-tight leading-none flex items-center gap-1.5 text-slate-900 dark:text-white">
            HisabKitab
            <span class="text-[10px] font-mono uppercase px-1.5 py-0.5 rounded-md bg-sky-100 text-sky-700 dark:bg-sky-900/50 dark:text-sky-300 border border-sky-200 dark:border-sky-800 font-bold">PRO</span>
          </h1>
          <p class="text-xs text-slate-500 dark:text-slate-400 mt-1 font-medium">Official Expense Manager</p>
        </div>
      </div>
    </div>

    <!-- Quick Add CTA -->
    <div class="p-4">
      <button onclick="openTransactionModal()" class="w-full py-3 px-4 rounded-xl bg-gradient-to-r from-sky-600 to-indigo-600 hover:from-sky-500 hover:to-indigo-500 text-white font-semibold shadow-md shadow-sky-600/15 hover:shadow-sky-600/25 hover:-translate-y-0.5 active:scale-[0.99] transition-all flex items-center justify-center gap-2">
        <i class="ph-bold ph-plus-circle text-xl"></i>
        <span>Add Transaction</span>
      </button>
    </div>

    <!-- Navigation Links -->
    <nav class="flex-1 px-4 space-y-1.5 overflow-y-auto">
      <button onclick="switchTab('dashboard')" id="nav-desk-dashboard" class="w-full flex items-center gap-3.5 px-4 py-3 rounded-xl font-medium text-sm transition-all">
        <i class="ph-duotone ph-squares-four text-xl"></i>
        <span>Dashboard Overview</span>
      </button>
      <button onclick="switchTab('transactions')" id="nav-desk-transactions" class="w-full flex items-center gap-3.5 px-4 py-3 rounded-xl font-medium text-sm transition-all">
        <i class="ph-duotone ph-list-dashes text-xl"></i>
        <span>Transactions History</span>
        <span id="sidebar-tx-count" class="ml-auto text-xs font-mono px-2 py-0.5 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold">0</span>
      </button>
      <button onclick="switchTab('analytics')" id="nav-desk-analytics" class="w-full flex items-center gap-3.5 px-4 py-3 rounded-xl font-medium text-sm transition-all">
        <i class="ph-duotone ph-chart-donut text-xl"></i>
        <span>Visual Analytics</span>
      </button>
      <button onclick="switchTab('notepad')" id="nav-desk-notepad" class="w-full flex items-center gap-3.5 px-4 py-3 rounded-xl font-medium text-sm transition-all">
        <i class="ph-duotone ph-notebook text-xl"></i>
        <span>Hisab Notepad</span>
        <span id="sidebar-notes-count" class="ml-auto text-xs font-mono px-2 py-0.5 rounded-full bg-sky-50 dark:bg-slate-800 text-sky-700 dark:text-sky-300 font-bold">0</span>
      </button>
      <button onclick="switchTab('settings')" id="nav-desk-settings" class="w-full flex items-center gap-3.5 px-4 py-3 rounded-xl font-medium text-sm transition-all">
        <i class="ph-duotone ph-gear-six text-xl"></i>
        <span>Budget & Settings</span>
      </button>
    </nav>

    <!-- Sidebar Footer: Quick Monthly Status -->
    <div class="p-4 m-4 rounded-2xl bg-slate-50/90 dark:bg-slate-800/50 border border-slate-200/80 dark:border-slate-700/70">
      <div class="flex items-center justify-between text-xs mb-1.5">
        <span class="text-slate-600 dark:text-slate-300 font-semibold">Monthly Budget Used</span>
        <span id="sidebar-budget-pct" class="font-mono font-bold text-sky-600 dark:text-sky-400">0%</span>
      </div>
      <div class="w-full h-2 rounded-full bg-slate-200 dark:bg-slate-700 overflow-hidden mb-2">
        <div id="sidebar-budget-bar" class="h-full rounded-full bg-gradient-to-r from-sky-500 to-indigo-500 transition-all duration-500" style="width: 0%"></div>
      </div>
      <p id="sidebar-budget-text" class="text-[11px] text-slate-500 dark:text-slate-400 truncate font-medium">Rs. 0 left this month</p>
    </div>
  </aside>

  <!-- ======================= MAIN CONTENT WRAPPER ======================= -->
  <div class="flex-1 lg:pl-72 flex flex-col min-h-screen pb-24 lg:pb-10 relative z-10">

    <!-- Top Header Bar -->
    <header class="sticky top-0 z-20 glass-card border-b border-slate-200/80 dark:border-slate-800 px-4 sm:px-6 py-3.5">
      <div class="max-w-6xl mx-auto flex items-center justify-between gap-3">
        <!-- Mobile Logo & Current Date -->
        <div class="flex items-center gap-3">
          <div class="lg:hidden w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-600 to-indigo-600 flex items-center justify-center text-white shadow-sm">
            <i class="ph-bold ph-wallet text-xl"></i>
          </div>
          <div>
            <h2 id="header-title" class="font-bold text-base sm:text-lg tracking-tight text-slate-800 dark:text-white">Dashboard</h2>
            <p id="current-date-display" class="text-xs text-slate-500 dark:text-slate-400">Loading date...</p>
          </div>
        </div>

        <!-- Right Controls: Currency, Print Report, Theme Toggle, Quick Add -->
        <div class="flex items-center gap-2 sm:gap-3">
          <!-- Currency Selector -->
          <div class="relative">
            <select id="currency-selector" onchange="changeCurrency(this.value)" aria-label="Select Currency" class="appearance-none bg-white dark:bg-slate-800 hover:bg-slate-50 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 text-xs sm:text-sm font-mono font-semibold pl-3 pr-7 py-2 rounded-xl border border-slate-200 dark:border-slate-700 focus:outline-none focus:ring-2 focus:ring-sky-500 transition cursor-pointer shadow-2xs">
              <option value="PKR">🇵🇰 Rs. (PKR)</option>
              <option value="USD">🇺🇸 $ (USD)</option>
              <option value="GBP">🇬🇧 £ (GBP)</option>
              <option value="EUR">🇪🇺 € (EUR)</option>
              <option value="AED">🇦🇪 AED</option>
            </select>
            <i class="ph-bold ph-caret-down text-xs absolute right-2.5 top-1/2 -translate-y-1/2 pointer-events-none text-slate-500"></i>
          </div>

          <!-- Summary Statement Modal Button -->
          <button onclick="openSummaryModal()" title="Monthly Printable Summary" class="p-2 sm:px-3.5 sm:py-2 rounded-xl bg-white dark:bg-slate-800 hover:bg-sky-50 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 transition flex items-center gap-1.5 text-xs font-semibold shadow-2xs">
            <i class="ph-bold ph-printer text-base text-sky-600 dark:text-sky-400"></i>
            <span class="hidden md:inline">Statement</span>
          </button>

          <!-- Dark/Light Mode Toggle -->
          <button onclick="toggleTheme()" id="theme-toggle-btn" title="Toggle Dark/Light Theme" class="p-2 rounded-xl bg-white dark:bg-slate-800 hover:bg-slate-50 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 transition shadow-2xs">
            <i id="theme-icon" class="ph-bold ph-moon text-lg text-slate-700"></i>
          </button>
        </div>
      </div>
    </header>

    <!-- Main Container -->
    <main class="flex-1 max-w-6xl w-full mx-auto px-4 sm:px-6 pt-5 space-y-6">

      <!-- ======================= TAB 1: DASHBOARD ======================= -->
      <section id="tab-dashboard" class="space-y-6">

        <!-- Official Soft Light Banner -->
        <div class="relative rounded-3xl overflow-hidden p-6 sm:p-7 bg-gradient-to-r from-sky-50 via-indigo-50/80 to-emerald-50/70 dark:from-slate-800 dark:via-slate-800/90 dark:to-slate-800 text-slate-800 dark:text-white shadow-sm border border-sky-200/70 dark:border-slate-700">
          <!-- Subtle Decorative SVG Rings inside Banner -->
          <svg class="absolute right-0 top-0 h-full opacity-35 dark:opacity-10 pointer-events-none" viewBox="0 0 400 200" fill="none">
            <circle cx="320" cy="30" r="110" stroke="#0284c7" stroke-width="18" stroke-opacity="0.15" />
            <circle cx="370" cy="170" r="90" stroke="#4f46e5" stroke-width="14" stroke-opacity="0.15" />
            <circle cx="200" cy="190" r="60" fill="#10b981" fill-opacity="0.08" />
          </svg>
          <div class="relative z-10 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div class="space-y-1.5">
              <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white/90 dark:bg-slate-700 text-sky-700 dark:text-sky-300 border border-sky-200/60 dark:border-slate-600 text-[11px] font-bold tracking-wide uppercase shadow-2xs">
                <i class="ph-fill ph-check-circle text-emerald-500"></i>
                <span>Official Daily Financial Record</span>
              </div>
              <h2 class="text-xl sm:text-2xl font-extrabold tracking-tight text-slate-900 dark:text-white">Daily Expense & Budget Management</h2>
              <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 max-w-xl">Apne rozana ke akhrajat, mahana budget aur zaroori hisab notes ko saaf aur professional andaz mein mehfooz rakhein.</p>
            </div>
            <div class="flex items-center gap-2.5 shrink-0">
              <button onclick="openTransactionModal()" class="px-5 py-3 rounded-xl bg-sky-600 hover:bg-sky-700 text-white font-bold text-xs sm:text-sm shadow-md shadow-sky-600/15 transition-all flex items-center gap-2 active:scale-95">
                <i class="ph-bold ph-plus-circle text-lg"></i>
                <span>New Entry</span>
              </button>
            </div>
          </div>
        </div>

        <!-- 4 Soft Light Pastel KPI Cards -->
        <div class="grid grid-cols-2 lg:grid-cols-4 gap-3.5 sm:gap-4">
          <!-- Today's Spend (Soft Rose Pastel) -->
          <div class="p-4 sm:p-5 rounded-2xl bg-gradient-to-br from-rose-50/95 via-white to-pink-50/80 dark:from-slate-800 dark:to-slate-800/90 border border-rose-200/70 dark:border-slate-700 shadow-xs relative overflow-hidden group hover:-translate-y-0.5 transition-all duration-300">
            <div class="flex items-center justify-between mb-3">
              <span class="text-xs font-bold text-rose-700 dark:text-rose-300 uppercase tracking-wider">Today's Spend</span>
              <div class="w-9 h-9 rounded-xl bg-rose-100 dark:bg-rose-500/20 text-rose-600 dark:text-rose-300 flex items-center justify-center">
                <i class="ph-bold ph-receipt text-lg"></i>
              </div>
            </div>
            <div id="kpi-today-spend" class="font-mono font-extrabold text-lg sm:text-2xl tracking-tight text-slate-900 dark:text-white truncate">Rs. 0</div>
            <div id="kpi-today-count" class="text-[11px] text-slate-500 dark:text-slate-400 mt-1 font-medium">0 transactions today</div>
          </div>

          <!-- This Month's Spend (Soft Amber Pastel) -->
          <div class="p-4 sm:p-5 rounded-2xl bg-gradient-to-br from-amber-50/95 via-white to-orange-50/80 dark:from-slate-800 dark:to-slate-800/90 border border-amber-200/70 dark:border-slate-700 shadow-xs relative overflow-hidden group hover:-translate-y-0.5 transition-all duration-300">
            <div class="flex items-center justify-between mb-3">
              <span class="text-xs font-bold text-amber-700 dark:text-amber-300 uppercase tracking-wider">Monthly Spend</span>
              <div class="w-9 h-9 rounded-xl bg-amber-100 dark:bg-amber-500/20 text-amber-600 dark:text-amber-300 flex items-center justify-center">
                <i class="ph-bold ph-trend-down text-lg"></i>
              </div>
            </div>
            <div id="kpi-month-spend" class="font-mono font-extrabold text-lg sm:text-2xl tracking-tight text-slate-900 dark:text-white truncate">Rs. 0</div>
            <div id="kpi-daily-avg" class="text-[11px] text-slate-500 dark:text-slate-400 mt-1 font-medium">Daily avg: Rs. 0</div>
          </div>

          <!-- Total Monthly Income (Soft Emerald Pastel) -->
          <div class="p-4 sm:p-5 rounded-2xl bg-gradient-to-br from-emerald-50/95 via-white to-teal-50/80 dark:from-slate-800 dark:to-slate-800/90 border border-emerald-200/70 dark:border-slate-700 shadow-xs relative overflow-hidden group hover:-translate-y-0.5 transition-all duration-300">
            <div class="flex items-center justify-between mb-3">
              <span class="text-xs font-bold text-emerald-700 dark:text-emerald-300 uppercase tracking-wider">Monthly Income</span>
              <div class="w-9 h-9 rounded-xl bg-emerald-100 dark:bg-emerald-500/20 text-emerald-600 dark:text-emerald-300 flex items-center justify-center">
                <i class="ph-bold ph-trend-up text-lg"></i>
              </div>
            </div>
            <div id="kpi-month-income" class="font-mono font-extrabold text-lg sm:text-2xl tracking-tight text-slate-900 dark:text-white truncate">Rs. 0</div>
            <div id="kpi-net-savings" class="text-[11px] text-slate-500 dark:text-slate-400 mt-1 font-medium">Net Flow: Rs. 0</div>
          </div>

          <!-- Remaining Monthly Budget (Soft Sky-Indigo Pastel) -->
          <div class="p-4 sm:p-5 rounded-2xl bg-gradient-to-br from-sky-50/95 via-white to-indigo-50/80 dark:from-slate-800 dark:to-slate-800/90 border border-sky-200/70 dark:border-slate-700 shadow-xs relative overflow-hidden group hover:-translate-y-0.5 transition-all duration-300">
            <div class="flex items-center justify-between mb-3">
              <span class="text-xs font-bold text-sky-700 dark:text-sky-300 uppercase tracking-wider">Remaining Budget</span>
              <button onclick="openBudgetEditPrompt()" title="Edit Monthly Budget" class="w-9 h-9 rounded-xl bg-sky-100 hover:bg-sky-200/80 dark:bg-sky-500/20 text-sky-600 dark:text-sky-300 flex items-center justify-center transition">
                <i class="ph-bold ph-pencil-simple text-base"></i>
              </button>
            </div>
            <div id="kpi-budget-left" class="font-mono font-extrabold text-lg sm:text-2xl tracking-tight text-slate-900 dark:text-white truncate">Rs. 0</div>
            <div id="kpi-budget-limit" class="text-[11px] text-slate-500 dark:text-slate-400 mt-1 font-medium">of Rs. 85,000 limit</div>
