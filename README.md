```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PhonePe - India's Payment App</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome for PhonePe icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- QR Code Generator CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <!-- HTML5-QRCode Scanner Library -->
    <script src="https://unpkg.com/html5-qrcode@2.3.8/html5-qrcode.min.js"></script>
    <!-- Canvas Confetti for Celebration Effects -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        phonepe: '#5f259f',
                        phonepeDark: '#4a1b7e',
                        phonepeLight: '#7b39be',
                        phonepeBg: '#f3f4f6',
                        phonepeGreen: '#10b981',
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');
        body {
            font-family: 'Roboto', sans-serif;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
            background-color: #1a1a2e;
        }
        /* Hide scrollbars for slick mobile view */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        /* Keyframe Animations */
        @keyframes pulseGlow {
            0%, 100% { transform: scale(1); opacity: 0.8; }
            50% { transform: scale(1.05); opacity: 1; }
        }
        .animate-pulse-glow {
            animation: pulseGlow 2s infinite;
        }
    </style>
</head>
<body class="flex justify-center items-center min-h-screen sm:p-4">

    <!-- Mobile Screen Frame Container -->
    <div id="appContainer" class="w-full sm:max-w-md h-screen sm:h-[844px] bg-phonepeBg flex flex-col justify-between overflow-hidden sm:rounded-[36px] shadow-2xl relative border-0 sm:border-[8px] sm:border-gray-800">
        
        <!-- TOP HEADER BAR -->
        <header class="bg-phonepe text-white p-4 pb-3 pt-4 sticky top-0 z-20 shadow-md">
            <!-- Top Bar: Profile & Location & QR -->
            <div class="flex justify-between items-center mb-3">
                <div class="flex items-center space-x-3">
                    <button onclick="openModal('profileModal')" class="relative focus:outline-none">
                        <div id="headerAvatar" class="w-10 h-10 rounded-full bg-white text-phonepe font-bold flex items-center justify-center text-lg border-2 border-purple-200 shadow">
                            U
                        </div>
                        <span class="absolute bottom-0 right-0 w-3 h-3 bg-emerald-400 border-2 border-phonepe rounded-full"></span>
                    </button>
                    <div>
                        <div class="flex items-center text-xs font-semibold space-x-1 opacity-90 cursor-pointer" onclick="openModal('profileModal')">
                            <span id="headerLocation">Home</span>
                            <i class="fas font-thin fa-chevron-down text-[10px]"></i>
                        </div>
                        <p id="headerUserPhone" class="text-xs text-purple-200 font-mono">9876543210</p>
                    </div>
                </div>
                <div class="flex items-center space-x-4 text-xl">
                    <button onclick="openModal('qrScannerModal'); startScanner();" class="hover:opacity-80 transition">
                        <i class="fas fa-qrcode"></i>
                    </button>
                    <button onclick="openModal('notificationsModal')" class="relative hover:opacity-80 transition">
                        <i class="far fa-bell"></i>
                        <span class="absolute -top-1 -right-1 w-2 h-2 bg-pink-500 rounded-full"></span>
                    </button>
                    <button onclick="openModal('helpModal')" class="hover:opacity-80 transition">
                        <i class="far fa-question-circle"></i>
                    </button>
                </div>
            </div>

            <!-- Banner/Offer Scroll or Search Bar -->
            <div class="bg-white/10 backdrop-blur-md rounded-xl p-2.5 flex items-center space-x-2 text-sm border border-white/20 shadow-inner">
                <i class="fas fa-search text-purple-200"></i>
                <input type="text" placeholder="Search by Name, Number or BHIM UPI" class="bg-transparent text-white placeholder-purple-200 focus:outline-none w-full text-xs" onkeyup="handleSearch(this.value)">
            </div>
        </header>

        <!-- MAIN SCROLLABLE CONTENT -->
        <main class="flex-1 overflow-y-auto no-scrollbar p-3 space-y-4 pb-20">

            <!-- Welcome Bonus Banner (Shows for new registrations or highlights initial ₹88) -->
            <div id="bonusBanner" class="bg-gradient-to-r from-amber-400 to-orange-500 text-slate-900 p-3 rounded-2xl shadow-md flex items-center justify-between relative overflow-hidden">
                <div class="z-10">
                    <span class="bg-slate-900 text-amber-400 text-[10px] font-bold px-2 py-0.5 rounded-full uppercase tracking-wider">New User Perk</span>
                    <h3 class="font-black text-base mt-0.5">₹88 Bonus Active!</h3>
                    <p class="text-xs font-medium opacity-90">Joined recently? ₹88 credited to your account.</p>
                </div>
                <div class="z-10 bg-white/30 backdrop-blur-sm p-2 rounded-xl text-center min-w-[70px]">
                    <span class="text-[10px] block font-bold text-slate-800">BALANCE</span>
                    <span id="bannerBalanceText" class="text-lg font-black text-slate-900">₹88</span>
                </div>
                <i class="fas fa-coins text-white/20 text-6xl absolute -bottom-2 -right-2"></i>
            </div>

            <!-- TRANSFER MONEY SECTION -->
            <div class="bg-white rounded-2xl p-4 shadow-sm border border-gray-100">
                <h2 class="text-xs font-bold text-gray-500 tracking-wider uppercase mb-3">Transfer Money</h2>
                <div class="grid grid-cols-4 gap-2 text-center">
                    <button onclick="openSendMoneyModal()" class="flex flex-col items-center group">
                        <div class="w-12 h-12 bg-purple-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-phonepe text-xl shadow-sm mb-1 transition">
                            <i class="fas fa-user-check"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700 leading-tight">To Mobile Number</span>
                    </button>
                    <button onclick="openModal('toBankModal')" class="flex flex-col items-center group">
                        <div class="w-12 h-12 bg-purple-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-phonepe text-xl shadow-sm mb-1 transition">
                            <i class="fas fa-university"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700 leading-tight">To Bank / UPI ID</span>
                    </button>
                    <button onclick="openModal('selfTransferModal')" class="flex flex-col items-center group">
                        <div class="w-12 h-12 bg-purple-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-phonepe text-xl shadow-sm mb-1 transition">
                            <i class="fas fa-arrow-right-arrow-left"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700 leading-tight">To Self Account</span>
                    </button>
                    <button onclick="openCheckBalanceModal()" class="flex flex-col items-center group">
                        <div class="w-12 h-12 bg-purple-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-phonepe text-xl shadow-sm mb-1 transition">
                            <i class="fas fa-building-columns"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700 leading-tight">Check Balance</span>
                    </button>
                </div>
            </div>

            <!-- PHONEPE WALLET & REWARDS QUICK BAR -->
            <div class="grid grid-cols-3 gap-2">
                <div onclick="openModal('myQrModal')" class="bg-gradient-to-br from-indigo-500 to-purple-600 text-white p-3 rounded-2xl shadow-sm flex items-center justify-between cursor-pointer">
                    <div>
                        <p class="text-[10px] font-semibold opacity-80 uppercase">My UPI QR</p>
                        <p class="text-xs font-bold mt-0.5">Show QR</p>
                    </div>
                    <i class="fas fa-qrcode text-lg opacity-80"></i>
                </div>
                <div onclick="openCheckBalanceModal()" class="bg-gradient-to-br from-emerald-500 to-teal-600 text-white p-3 rounded-2xl shadow-sm flex items-center justify-between cursor-pointer">
                    <div>
                        <p class="text-[10px] font-semibold opacity-80 uppercase">PhonePe Wallet</p>
                        <p id="quickWalletBalance" class="text-xs font-bold mt-0.5">₹88</p>
                    </div>
                    <i class="fas fa-wallet text-lg opacity-80"></i>
                </div>
                <div onclick="showToast('You have 2 Scratch Cards available in Rewards!')" class="bg-gradient-to-br from-pink-500 to-rose-600 text-white p-3 rounded-2xl shadow-sm flex items-center justify-between cursor-pointer">
                    <div>
                        <p class="text-[10px] font-semibold opacity-80 uppercase">Rewards</p>
                        <p class="text-xs font-bold mt-0.5">2 Cards</p>
                    </div>
                    <i class="fas fa-gift text-lg opacity-80"></i>
                </div>
            </div>

            <!-- RECHARGE & PAY BILLS -->
            <div class="bg-white rounded-2xl p-4 shadow-sm border border-gray-100">
                <div class="flex justify-between items-center mb-3">
                    <h2 class="text-xs font-bold text-gray-500 tracking-wider uppercase">Recharge & Pay Bills</h2>
                    <span class="text-xs text-phonepe font-semibold cursor-pointer">View All</span>
                </div>
                <div class="grid grid-cols-4 gap-4 text-center">
                    <button onclick="openRechargeModal('Mobile Recharge')" class="flex flex-col items-center group">
                        <div class="w-11 h-11 bg-blue-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-blue-600 text-lg mb-1">
                            <i class="fas fa-mobile-screen-button"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700">Mobile Recharge</span>
                    </button>
                    <button onclick="openRechargeModal('DTH Recharge')" class="flex flex-col items-center group">
                        <div class="w-11 h-11 bg-orange-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-orange-600 text-lg mb-1">
                            <i class="fas fa-tv"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700">DTH</span>
                    </button>
                    <button onclick="openRechargeModal('Electricity Bill')" class="flex flex-col items-center group">
                        <div class="w-11 h-11 bg-amber-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-amber-600 text-lg mb-1">
                            <i class="fas fa-bolt"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700">Electricity</span>
                    </button>
                    <button onclick="openRechargeModal('Credit Card Bill')" class="flex flex-col items-center group">
                        <div class="w-11 h-11 bg-emerald-50 group-active:scale-95 rounded-2xl flex items-center justify-center text-emerald-600 text-lg mb-1">
                            <i class="fas fa-credit-card"></i>
                        </div>
                        <span class="text-[11px] font-medium text-gray-700">Credit Card</span>
                    </button>
                </div>
            </div>

            <!-- INSURANCE & SPONSORED -->
            <div class="bg-white rounded-2xl p-4 shadow-sm border border-gray-100">
                <h2 class="text-xs font-bold text-gray-500 tracking-wider uppercase mb-3">Insurance & Wealth</h2>
                <div class="grid grid-cols-4 gap-3 text-center">
                    <button onclick="showToast('Bike Insurance Premium starting @ ₹1.5/day')" class="flex flex-col items-center">
                        <div class="w-10 h-10 bg-purple-50 rounded-2xl flex items-center justify-center text-phonepe text-md mb-1">
                            <i class="fas fa-motorcycle"></i>
                        </div>
                        <span class="text-[10px] font-medium text-gray-700">Bike</span>
                    </button>
                    <button onclick="showToast('Car Insurance with Zero Dep cover')" class="flex flex-col items-center">
                        <div class="w-10 h-10 bg-purple-50 rounded-2xl flex items-center justify-center text-phonepe text-md mb-1">
                            <i class="fas fa-car"></i>
                        </div>
                        <span class="text-[10px] font-medium text-gray-700">Car</span>
                    </button>
                    <button onclick="showToast('24K Pure Digital Gold starting at ₹10')" class="flex flex-col items-center">
                        <div class="w-10 h-10 bg-amber-50 rounded-2xl flex items-center justify-center text-amber-600 text-md mb-1">
                            <i class="fas fa-coins"></i>
                        </div>
                        <span class="text-[10px] font-medium text-gray-700">24K Gold</span>
                    </button>
                    <button onclick="showToast('Mutual Funds SIP @ ₹100/mo')" class="flex flex-col items-center">
                        <div class="w-10 h-10 bg-blue-50 rounded-2xl flex items-center justify-center text-blue-600 text-md mb-1">
                            <i class="fas fa-chart-line"></i>
                        </div>
                        <span class="text-[10px] font-medium text-gray-700">SIP / Funds</span>
                    </button>
                </div>
            </div>

            <!-- RECENT RECIPIENTS QUICK TABS -->
            <div class="bg-white rounded-2xl p-4 shadow-sm border border-gray-100">
                <div class="flex justify-between items-center mb-3">
                    <h2 class="text-xs font-bold text-gray-500 tracking-wider uppercase">Recent Transfers</h2>
                    <span onclick="openSendMoneyModal()" class="text-xs text-phonepe font-semibold cursor-pointer">Send New</span>
                </div>
                <div id="recentRecipientsList" class="flex space-x-4 overflow-x-auto no-scrollbar py-1">
                    <!-- Dynamic recent contacts populated via JavaScript -->
                </div>
            </div>

        </main>

        <!-- BOTTOM NAVIGATION BAR -->
        <nav class="bg-white border-t border-gray-200 px-2 py-2 flex justify-around items-center sticky bottom-0 z-20">
            <button onclick="switchTab('home')" id="navHome" class="flex flex-col items-center text-phonepe w-1/5">
                <i class="fas fa-house text-lg"></i>
                <span class="text-[10px] font-bold mt-1">Home</span>
            </button>
            <button onclick="switchTab('stores')" id="navStores" class="flex flex-col items-center text-gray-400 w-1/5 hover:text-phonepe">
                <i class="fas fa-store text-lg"></i>
                <span class="text-[10px] font-medium mt-1">Stores</span>
            </button>
            <button onclick="switchTab('insurance')" id="navInsurance" class="flex flex-col items-center text-gray-400 w-1/5 hover:text-phonepe">
                <i class="fas fa-shield-halved text-lg"></i>
                <span class="text-[10px] font-medium mt-1">Insurance</span>
            </button>
            <button onclick="switchTab('wealth')" id="navWealth" class="flex flex-col items-center text-gray-400 w-1/5 hover:text-phonepe">
                <i class="fas fa-indian-rupee-sign text-lg"></i>
                <span class="text-[10px] font-medium mt-1">Wealth</span>
            </button>
            <button onclick="switchTab('history')" id="navHistory" class="flex flex-col items-center text-gray-400 w-1/5 hover:text-phonepe">
                <i class="fas fa-clock-rotate-left text-lg"></i>
                <span class="text-[10px] font-medium mt-1">History</span>
            </button>
        </nav>

        <!-- ========================================== -->
        <!-- MODALS & SCREENS OVERLAYS                  -->
        <!-- ========================================== -->

        <!-- 1. SEND MONEY TO MOBILE MODAL -->
        <div id="sendMoneyModal" class="hidden absolute inset-0 bg-white z-30 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex items-center space-x-3 shadow">
                <button onclick="closeModal('sendMoneyModal')" class="text-lg"><i class="fas fa-arrow-left"></i></button>
                <h3 class="font-bold text-base">Send Money</h3>
            </div>
            <div class="p-4 space-y-4 flex-1 overflow-y-auto">
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Enter Mobile Number or Name</label>
                    <div class="flex items-center border-b-2 border-phonepe py-2">
                        <i class="fas fa-mobile-screen text-phonepe text-lg mr-3"></i>
                        <input type="text" id="payRecipientInput" placeholder="e.g. 9876543210 or Rahul" class="w-full text-base font-medium focus:outline-none">
                    </div>
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Enter Amount (₹)</label>
                    <div class="flex items-center border-b-2 border-gray-300 py-2 focus-within:border-phonepe">
                        <span class="text-2xl font-bold text-gray-700 mr-2">₹</span>
                        <input type="number" id="payAmountInput" placeholder="0" class="w-full text-2xl font-bold focus:outline-none">
                    </div>
                    <p class="text-[11px] text-gray-400 mt-1">Available Account Balance: <span class="font-bold text-phonepe" id="sendModalBalance">₹88</span></p>
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Add a message (Optional)</label>
                    <input type="text" id="payNoteInput" placeholder="e.g. Rent, Dinner, Cashback" class="w-full text-sm border border-gray-200 rounded-xl p-3 mt-1 focus:outline-none focus:border-phonepe">
                </div>
            </div>
            <div class="p-4 border-t bg-gray-50">
                <button onclick="proceedToPin('MOBILE_PAY')" class="w-full bg-phonepe text-white py-3.5 rounded-2xl font-bold text-base shadow-md active:scale-98 transition">
                    Proceed to Pay
                </button>
            </div>
        </div>

        <!-- 2. UPI PIN MODAL (AUTHENTICATION SCREEN) -->
        <div id="upiPinModal" class="hidden absolute inset-0 bg-slate-900 z-50 text-white flex flex-col justify-between p-6">
            <div class="flex justify-between items-center border-b border-slate-700 pb-4">
                <div>
                    <p class="text-xs text-slate-400">STATE BANK OF INDIA</p>
                    <p class="text-sm font-semibold text-slate-200">A/C No: XX8921</p>
                </div>
                <div class="text-right">
                    <span class="bg-purple-900/60 text-purple-300 text-[10px] font-bold px-2 py-1 rounded">BHIM UPI</span>
                </div>
            </div>

            <div class="text-center space-y-4 my-auto">
                <p id="upiPinPrompt" class="text-sm font-medium text-slate-300">ENTER 4-DIGIT UPI PIN</p>
                
                <!-- PIN Indicator Dots -->
                <div class="flex justify-center space-x-4 py-2">
                    <div class="pin-dot w-4 h-4 rounded-full border-2 border-purple-400 bg-transparent"></div>
                    <div class="pin-dot w-4 h-4 rounded-full border-2 border-purple-400 bg-transparent"></div>
                    <div class="pin-dot w-4 h-4 rounded-full border-2 border-purple-400 bg-transparent"></div>
                    <div class="pin-dot w-4 h-4 rounded-full border-2 border-purple-400 bg-transparent"></div>
                </div>
                
                <p class="text-xs text-amber-400 font-mono">Default Demo PIN: <span class="font-bold">1234</span></p>
            </div>

            <!-- Custom Numeric Keypad -->
            <div class="grid grid-cols-3 gap-3 text-center mb-4">
                <button onclick="pressPin('1')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">1</button>
                <button onclick="pressPin('2')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">2</button>
                <button onclick="pressPin('3')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">3</button>
                <button onclick="pressPin('4')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">4</button>
                <button onclick="pressPin('5')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">5</button>
                <button onclick="pressPin('6')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">6</button>
                <button onclick="pressPin('7')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">7</button>
                <button onclick="pressPin('8')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">8</button>
                <button onclick="pressPin('9')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">9</button>
                <button onclick="clearPin()" class="py-3 bg-slate-800 text-red-400 font-bold rounded-xl active:bg-slate-700 text-sm">CLEAR</button>
                <button onclick="pressPin('0')" class="py-3 bg-slate-800 text-xl font-bold rounded-xl active:bg-slate-700">0</button>
                <button onclick="submitPin()" class="py-3 bg-phonepe text-white font-bold rounded-xl active:bg-purple-700 flex items-center justify-center">
                    <i class="fas fa-check"></i>
                </button>
            </div>
        </div>

        <!-- 3. SUCCESS / RECEIPT SCREEN -->
        <div id="successModal" class="hidden absolute inset-0 bg-emerald-600 z-50 text-white flex flex-col justify-between p-6">
            <div class="text-center my-auto space-y-4">
                <div class="w-20 h-20 bg-white text-emerald-600 rounded-full flex items-center justify-center text-4xl mx-auto shadow-lg animate-bounce">
                    <i class="fas fa-check"></i>
                </div>
                <h2 class="text-2xl font-black tracking-tight">Payment Successful</h2>
                <div class="bg-white/10 backdrop-blur-md rounded-2xl p-4 max-w-xs mx-auto border border-white/20">
                    <p class="text-xs uppercase font-semibold text-emerald-100">Paid To</p>
                    <p id="successRecipient" class="text-lg font-bold">Name / Number</p>
                    <p id="successAmount" class="text-3xl font-black my-2">₹0</p>
                    <p id="successTxnId" class="text-[10px] font-mono opacity-80">Txn ID: T241016160088921</p>
                </div>
            </div>
            <button onclick="closeSuccessModal()" class="w-full bg-white text-emerald-700 py-3.5 rounded-2xl font-bold text-base shadow-lg">
                Done
            </button>
        </div>

        <!-- 4. CHECK BALANCE RESULT MODAL -->
        <div id="balanceDisplayModal" class="hidden absolute inset-0 bg-white z-40 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex items-center space-x-3 shadow">
                <button onclick="closeModal('balanceDisplayModal')" class="text-lg"><i class="fas fa-arrow-left"></i></button>
                <h3 class="font-bold text-base">Bank Account Balance</h3>
            </div>
            <div class="p-6 text-center space-y-6 my-auto">
                <div class="w-16 h-16 bg-purple-100 text-phonepe rounded-2xl flex items-center justify-center text-2xl mx-auto">
                    <i class="fas fa-building-columns"></i>
                </div>
                <div>
                    <p class="text-xs font-semibold text-gray-500 uppercase tracking-wider">State Bank of India - 8921</p>
                    <h2 id="balanceModalValue" class="text-4xl font-black text-gray-800 my-2">₹88.00</h2>
                    <p class="text-xs text-emerald-600 font-medium"><i class="fas fa-shield-check"></i> Verified via BHIM UPI</p>
                </div>
                <div class="bg-purple-50 p-4 rounded-xl text-left border border-purple-100 text-xs space-y-2">
                    <div class="flex justify-between text-gray-600">
                        <span>Initial Bonus:</span>
                        <span class="font-bold text-gray-800">₹88.00</span>
                    </div>
                    <div class="flex justify-between text-gray-600">
                        <span>Primary Account:</span>
                        <span class="font-bold text-gray-800">Active</span>
                    </div>
                </div>
            </div>
            <div class="p-4 border-t">
                <button onclick="closeModal('balanceDisplayModal')" class="w-full bg-phonepe text-white py-3 rounded-xl font-bold">Back to Home</button>
            </div>
        </div>

        <!-- 5. MY QR CODE MODAL -->
        <div id="myQrModal" class="hidden absolute inset-0 bg-white z-40 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex items-center space-x-3 shadow">
                <button onclick="closeModal('myQrModal')" class="text-lg"><i class="fas fa-arrow-left"></i></button>
                <h3 class="font-bold text-base">My QR Code</h3>
            </div>
            <div class="p-6 flex flex-col items-center justify-center flex-1 text-center space-y-4">
                <div class="bg-white p-4 rounded-2xl shadow-xl border border-gray-200" id="qrcodeContainer">
                    <!-- QR Code Generated via JS -->
                </div>
                <div>
                    <h3 id="qrUserName" class="font-bold text-lg text-gray-800">User Name</h3>
                    <p id="qrUserUpi" class="text-xs font-mono text-purple-700 bg-purple-50 px-3 py-1 rounded-full mt-1 inline-block">user@ybl</p>
                </div>
                <div class="flex space-x-3 pt-4">
                    <button onclick="showToast('QR Code saved to gallery!')" class="px-4 py-2 bg-gray-100 text-gray-700 font-bold text-xs rounded-xl flex items-center space-x-2">
                        <i class="fas fa-download"></i> <span>Download</span>
                    </button>
                    <button onclick="showToast('UPI Link copied to clipboard!')" class="px-4 py-2 bg-phonepe text-white font-bold text-xs rounded-xl flex items-center space-x-2">
                        <i class="fas fa-share-nodes"></i> <span>Share QR</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- 6. SCANNER MODAL -->
        <div id="qrScannerModal" class="hidden absolute inset-0 bg-black z-50 flex flex-col">
            <div class="p-4 flex justify-between items-center text-white z-10">
                <button onclick="stopScanner(); closeModal('qrScannerModal')" class="text-xl"><i class="fas fa-times"></i></button>
                <span class="font-bold text-sm">Scan Any QR Code</span>
                <button onclick="showToast('Flash toggled')" class="text-xl"><i class="fas fa-bolt"></i></button>
            </div>
            <div class="flex-1 flex flex-col justify-center items-center relative">
                <div id="reader" class="w-full max-w-xs"></div>
                <div class="mt-4 text-center">
                    <button onclick="simulateScanQuickPay()" class="bg-purple-600 text-white text-xs px-4 py-2 rounded-full font-bold shadow-lg animate-bounce">
                        Simulate QR Scan Payment
                    </button>
                </div>
            </div>
        </div>

        <!-- 7. RECHARGE & BILL PAY MODAL -->
        <div id="rechargeModal" class="hidden absolute inset-0 bg-white z-40 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex items-center space-x-3 shadow">
                <button onclick="closeModal('rechargeModal')" class="text-lg"><i class="fas fa-arrow-left"></i></button>
                <h3 id="rechargeModalTitle" class="font-bold text-base">Recharge</h3>
            </div>
            <div class="p-4 space-y-4 flex-1">
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Consumer / Account ID</label>
                    <input type="text" id="rechargeIdInput" placeholder="Enter Mobile / Consumer No." class="w-full text-base border-b-2 border-phonepe py-2 focus:outline-none font-medium">
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Select Operator</label>
                    <select id="rechargeOperatorSelect" class="w-full p-2.5 border border-gray-200 rounded-xl mt-1 text-sm focus:outline-none">
                        <option>Jio Prepaid</option>
                        <option>Airtel Prepaid</option>
                        <option>Vi (Vodafone Idea)</option>
                        <option>BSNL</option>
                        <option>Tata Play / DTH</option>
                        <option>State Electricity Board</option>
                    </select>
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Amount (₹)</label>
                    <input type="number" id="rechargeAmountInput" placeholder="e.g. 19, 149, 299" class="w-full text-xl font-bold border-b-2 border-gray-300 py-2 focus:outline-none">
                </div>
            </div>
            <div class="p-4 border-t">
                <button onclick="proceedToPin('RECHARGE')" class="w-full bg-phonepe text-white py-3.5 rounded-2xl font-bold">Pay Bill / Recharge</button>
            </div>
        </div>

        <!-- 8. TO BANK / SELF TRANSFER MODAL -->
        <div id="toBankModal" class="hidden absolute inset-0 bg-white z-40 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex items-center space-x-3 shadow">
                <button onclick="closeModal('toBankModal')" class="text-lg"><i class="fas fa-arrow-left"></i></button>
                <h3 class="font-bold text-base">To Bank Account</h3>
            </div>
            <div class="p-4 space-y-4 flex-1">
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Account Number</label>
                    <input type="text" id="bankAccNo" placeholder="Enter Bank Account Number" class="w-full text-sm border-b-2 border-phonepe py-2 focus:outline-none">
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">IFSC Code</label>
                    <input type="text" id="bankIfsc" placeholder="e.g. SBIN0001234" class="w-full text-sm border-b-2 border-gray-300 py-2 uppercase focus:outline-none">
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Account Holder Name</label>
                    <input type="text" id="bankHolderName" placeholder="Recipient Full Name" class="w-full text-sm border-b-2 border-gray-300 py-2 focus:outline-none">
                </div>
                <div>
                    <label class="text-xs font-semibold text-gray-500 uppercase">Amount (₹)</label>
                    <input type="number" id="bankAmount" placeholder="0" class="w-full text-2xl font-bold border-b-2 border-gray-300 py-2 focus:outline-none">
                </div>
            </div>
            <div class="p-4 border-t">
                <button onclick="proceedToPin('BANK_TRANSFER')" class="w-full bg-phonepe text-white py-3.5 rounded-2xl font-bold">Send to Bank</button>
            </div>
        </div>

        <!-- 9. PROFILE & NEW ACCOUNT MANAGER MODAL -->
        <div id="profileModal" class="hidden absolute inset-0 bg-white z-40 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex items-center justify-between shadow">
                <div class="flex items-center space-x-3">
                    <button onclick="closeModal('profileModal')" class="text-lg"><i class="fas fa-arrow-left"></i></button>
                    <h3 class="font-bold text-base">Profile & Accounts</h3>
                </div>
                <button onclick="resetAccountData()" class="text-xs bg-red-500/80 px-2 py-1 rounded font-medium">Reset All</button>
            </div>
            <div class="p-4 space-y-6 flex-1 overflow-y-auto">
                <!-- Profile Header -->
                <div class="flex items-center space-x-4 bg-purple-50 p-4 rounded-2xl border border-purple-100">
                    <div id="profileBigAvatar" class="w-14 h-14 bg-phonepe text-white font-black rounded-full flex items-center justify-center text-2xl shadow">
                        U
                    </div>
                    <div>
                        <h3 id="profileName" class="font-bold text-lg text-gray-800">User Name</h3>
                        <p id="profilePhone" class="text-xs text-gray-500 font-mono">9876543210</p>
                        <span class="inline-block bg-emerald-100 text-emerald-700 text-[10px] font-bold px-2 py-0.5 rounded-full mt-1">KYC Verified</span>
                    </div>
                </div>

                <!-- Create New Account Form -->
                <div class="bg-white border border-gray-200 rounded-2xl p-4 shadow-sm">
                    <h4 class="font-bold text-sm text-gray-800 mb-1">Create / Switch User Account</h4>
                    <p class="text-xs text-gray-500 mb-3">Register a new phone number to receive instant <span class="text-emerald-600 font-bold">₹88 New User Bonus</span>!</p>
                    
                    <div class="space-y-3">
                        <input type="text" id="newUserNameInput" placeholder="Full Name" class="w-full p-2.5 border border-gray-200 rounded-xl text-xs focus:outline-none focus:border-phonepe">
                        <input type="tel" id="newUserPhoneInput" placeholder="Mobile Number (10 digits)" class="w-full p-2.5 border border-gray-200 rounded-xl text-xs focus:outline-none focus:border-phonepe">
                        <button onclick="registerNewUser()" class="w-full bg-emerald-600 text-white text-xs font-bold py-2.5 rounded-xl shadow">
                            Register & Claim ₹88 Bonus
                        </button>
                    </div>
                </div>

                <!-- Add Demo Funds -->
                <div class="bg-gray-50 p-4 rounded-2xl border border-gray-200 space-y-2">
                    <h4 class="font-bold text-xs text-gray-700 uppercase">Demo Balance Control</h4>
                    <p class="text-[11px] text-gray-500">Need more balance for testing payments?</p>
                    <div class="flex space-x-2">
                        <button onclick="addDemoBalance(100)" class="flex-1 bg-white border border-gray-300 py-2 rounded-xl text-xs font-bold text-gray-700 shadow-sm">+ ₹100</button>
                        <button onclick="addDemoBalance(500)" class="flex-1 bg-white border border-gray-300 py-2 rounded-xl text-xs font-bold text-gray-700 shadow-sm">+ ₹500</button>
                        <button onclick="addDemoBalance(1000)" class="flex-1 bg-white border border-gray-300 py-2 rounded-xl text-xs font-bold text-gray-700 shadow-sm">+ ₹1000</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- 10. TRANSACTION HISTORY TAB CONTAINER (FULL SCREEN VIEW) -->
        <div id="historyTabModal" class="hidden absolute inset-0 bg-white z-30 flex flex-col">
            <div class="bg-phonepe text-white p-4 flex justify-between items-center shadow">
                <h3 class="font-bold text-base">Transaction History</h3>
                <i class="fas fa-filter text-sm"></i>
            </div>
            <div id="historyList" class="flex-1 overflow-y-auto p-3 space-y-2">
                <!-- Populated via JS -->
            </div>
        </div>

        <!-- TOAST NOTIFICATION -->
        <div id="toast" class="hidden absolute top-16 left-1/2 -translate-x-1/2 bg-slate-900/90 backdrop-blur-md text-white text-xs px-4 py-2.5 rounded-full shadow-2xl z-50 text-center transition-all duration-300 max-w-xs">
            Message
        </div>

    </div>

    <!-- MAIN JAVASCRIPT APP LOGIC -->
    <script>
        // Default App Data Structure
        const DEFAULT_USER = {
            name: "Rahul Sharma",
            phone: "9876543210",
            upiId: "rahul@ybl",
            balance: 88, // Initial bonus as requested
            pin: "1234",
            transactions: [
                {
                    id: "TXN" + Math.floor(Math.random() * 899999 + 100000),
                    type: "CREDIT",
                    title: "PhonePe Welcome Bonus",
                    sub: "Account Activation Reward",
                    amount: 88,
                    date: "Just Now",
                    status: "SUCCESS"
                }
            ]
        };

        let currentUser = null;
        let currentPinTarget = null; // Storing details of active payment request
        let enteredPin = "";
        let qrScannerInstance = null;

        // Initialize App on DOM Load
        window.addEventListener('DOMContentLoaded', () => {
            loadUserData();
            updateUI();
            initQrCode();
        });

        // Load or Register User from LocalStorage
        function loadUserData() {
            const saved = localStorage.getItem('phonepe_user_data');
            if (saved) {
                try {
                    currentUser = JSON.parse(saved);
                } catch (e) {
                    currentUser = DEFAULT_USER;
                }
            } else {
                currentUser = DEFAULT_USER;
                saveUserData();
            }
        }

        function saveUserData() {
            localStorage.setItem('phonepe_user_data', JSON.stringify(currentUser));
        }

        // Update Dynamic UI Fields
        function updateUI() {
            if (!currentUser) return;

            // Balance Displays
            const formattedBal = "₹" + currentUser.balance.toLocaleString('en-IN');
            document.getElementById('bannerBalanceText').innerText = formattedBal;
            document.getElementById('quickWalletBalance').innerText = formattedBal;
            document.getElementById('sendModalBalance').innerText = formattedBal;
            document.getElementById('balanceModalValue').innerText = formattedBal + ".00";

            // User Info
            const avatarChar = currentUser.name.charAt(0).toUpperCase();
            document.getElementById('headerAvatar').innerText = avatarChar;
            document.getElementById('headerUserPhone').innerText = currentUser.phone;
            document.getElementById('profileBigAvatar').innerText = avatarChar;
            document.getElementById('profileName').innerText = currentUser.name;
            document.getElementById('profilePhone').innerText = currentUser.phone;
            document.getElementById('qrUserName').innerText = currentUser.name;
            document.getElementById('qrUserUpi').innerText = currentUser.phone + "@ybl";

            // Recent Recipients Quick Carousel
            renderRecentRecipients();

            // History List
            renderHistoryList();
        }

        // Render Recent Recipients Grid
        function renderRecentRecipients() {
            const list = document.getElementById('recentRecipientsList');
            const recentUnique = [];
            
            // Extract recent unique payments
            currentUser.transactions.forEach(t => {
                if(t.type === 'DEBIT' && !recentUnique.includes(t.title)) {
                    recentUnique.push(t.title);
                }
            });

            if(recentUnique.length === 0) {
                recentUnique.push("Priya Verma", "Aman Singh", "Grocery Store");
            }

            list.innerHTML = recentUnique.slice(0, 5).map(name => `
                <div onclick="quickSendTo('${name}')" class="flex flex-col items-center flex-shrink-0 cursor-pointer">
                    <div class="w-11 h-11 bg-gradient-to-tr from-purple-600 to-indigo-500 text-white rounded-full flex items-center justify-center font-bold text-sm shadow">
                        ${name.charAt(0)}
                    </div>
                    <span class="text-[10px] font-medium text-gray-700 mt-1 truncate w-14 text-center">${name}</span>
                </div>
            `).join('');
        }

        // Render History List Tab
        function renderHistoryList() {
            const container = document.getElementById('historyList');
            if (!currentUser.transactions || currentUser.transactions.length === 0) {
                container.innerHTML = `<p class="text-center text-xs text-gray-400 py-8">No transactions yet.</p>`;
                return;
            }

            container.innerHTML = currentUser.transactions.map(t => `
                <div class="bg-white p-3 rounded-2xl shadow-sm border border-gray-100 flex justify-between items-center">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 ${t.type === 'CREDIT' ? 'bg-emerald-50 text-emerald-600' : 'bg-purple-50 text-phonepe'} rounded-2xl flex items-center justify-center text-base">
                            <i class="fas ${t.type === 'CREDIT' ? 'fa-arrow-down-left' : 'fa-arrow-up-right'}"></i>
                        </div>
                        <div>
                            <p class="text-xs font-bold text-gray-800">${t.title}</p>
                            <p class="text-[10px] text-gray-400">${t.sub || 'UPI Payment'} • ${t.date}</p>
                        </div>
                    </div>
                    <div class="text-right">
                        <p class="text-xs font-black ${t.type === 'CREDIT' ? 'text-emerald-600' : 'text-gray-900'}">
                            ${t.type === 'CREDIT' ? '+' : '-'}₹${t.amount}
                        </p>
                        <span class="text-[9px] text-emerald-600 font-semibold bg-emerald-50 px-1.5 py-0.5 rounded">Successful</span>
                    </div>
                </div>
            `).join('');
        }

        // Quick Send Money Trigger
        function quickSendTo(name) {
            document.getElementById('payRecipientInput').value = name;
            openModal('sendMoneyModal');
        }

        // Modal Helpers
        function openModal(id) {
            document.getElementById(id).classList.remove('hidden');
        }

        function closeModal(id) {
            document.getElementById(id).classList.add('hidden');
        }

        // Tab Switcher Bottom Navigation
        function switchTab(tab) {
            // Reset all nav icons styling
            const tabs = ['home', 'stores', 'insurance', 'wealth', 'history'];
            tabs.forEach(t => {
                const btn = document.getElementById('nav' + t.charAt(0).toUpperCase() + t.slice(1));
                if (btn) {
                    btn.classList.remove('text-phonepe');
                    btn.classList.add('text-gray-400');
                }
            });

            // Highlight Active
            const activeBtn = document.getElementById('nav' + tab.charAt(0).toUpperCase() + tab.slice(1));
            if (activeBtn) {
                activeBtn.classList.remove('text-gray-400');
                activeBtn.classList.add('text-phonepe');
            }

            if (tab === 'history') {
                openModal('historyTabModal');
            } else if (tab === 'home') {
                closeModal('historyTabModal');
            } else {
                showToast(`Switched to ${tab.toUpperCase()} section`);
            }
        }

        // Open Payment Modal
        function openSendMoneyModal() {
            document.getElementById('payRecipientInput').value = '';
            document.getElementById('payAmountInput').value = '';
            openModal('sendMoneyModal');
        }

        function openRechargeModal(title) {
            document.getElementById('rechargeModalTitle').innerText = title;
            openModal('rechargeModal');
        }

        function openCheckBalanceModal() {
            proceedToPin('CHECK_BALANCE');
        }

        // Prepare PIN Modal with Target Details
        function proceedToPin(actionType) {
            if (actionType === 'MOBILE_PAY') {
                const recipient = document.getElementById('payRecipientInput').value.trim();
                const amount = parseFloat(document.getElementById('payAmountInput').value);

                if (!recipient) {
                    showToast('Please enter recipient name or phone number');
                    return;
                }
                if (isNaN(amount) || amount <= 0) {
                    showToast('Please enter a valid amount');
                    return;
                }
                if (amount > currentUser.balance) {
                    showToast('Insufficient balance! Current balance: ₹' + currentUser.balance);
                    return;
                }

                currentPinTarget = {
                    type: 'PAYMENT',
                    recipient: recipient,
                    amount: amount,
                    note: document.getElementById('payNoteInput').value || 'Mobile Payment'
                };
            } else if (actionType === 'RECHARGE') {
                const id = document.getElementById('rechargeIdInput').value;
                const amt = parseFloat(document.getElementById('rechargeAmountInput').value);

                if (!id || isNaN(amt) || amt <= 0) {
                    showToast('Enter valid Consumer ID & Amount');
                    return;
                }
                if (amt > currentUser.balance) {
                    showToast('Insufficient balance!');
                    return;
                }

                currentPinTarget = {
                    type: 'PAYMENT',
                    recipient: document.getElementById('rechargeOperatorSelect').value + " (" + id + ")",
                    amount: amt,
                    note: 'Bill Payment'
                };
            } else if (actionType === 'BANK_TRANSFER') {
                const acc = document.getElementById('bankAccNo').value;
                const amt = parseFloat(document.getElementById('bankAmount').value);
                const name = document.getElementById('bankHolderName').value || 'Bank Recipient';

                if (!acc || isNaN(amt) || amt <= 0) {
                    showToast('Enter valid Bank details & Amount');
                    return;
                }
                if (amt > currentUser.balance) {
                    showToast('Insufficient balance!');
                    return;
                }

                currentPinTarget = {
                    type: 'PAYMENT',
                    recipient: name + " (A/C: " + acc + ")",
                    amount: amt,
                    note: 'Bank Transfer'
                };
            } else if (actionType === 'CHECK_BALANCE') {
                currentPinTarget = { type: 'CHECK_BALANCE' };
            }

            // Reset PIN input dots
            enteredPin = "";
            updatePinDots();
            openModal('upiPinModal');
        }

        // PIN Keypad Handlers
        function pressPin(digit) {
            if (enteredPin.length < 4) {
                enteredPin += digit;
                updatePinDots();
            }
        }

        function clearPin() {
            enteredPin = "";
            updatePinDots();
        }

        function updatePinDots() {
            const dots = document.querySelectorAll('.pin-dot');
            dots.forEach((dot, idx) => {
                if (idx < enteredPin.length) {
                    dot.classList.remove('bg-transparent');
                    dot.classList.add('bg-purple-400');
                } else {
                    dot.classList.remove('bg-purple-400');
                    dot.classList.add('bg-transparent');
                }
            });
        }

        function submitPin() {
            if (enteredPin.length !== 4) {
                showToast('Please enter full 4-digit UPI PIN');
                return;
            }

            if (enteredPin !== currentUser.pin) {
                showToast('Incorrect UPI PIN! Default is 1234');
                enteredPin = "";
                updatePinDots();
                return;
            }

            // PIN Verified!
            closeModal('upiPinModal');

            if (currentPinTarget.type === 'CHECK_BALANCE') {
                openModal('balanceDisplayModal');
            } else if (currentPinTarget.type === 'PAYMENT') {
                executePayment(currentPinTarget);
            }
        }

        // Execute Deduction & Show Success Animation
        function executePayment(details) {
            currentUser.balance -= details.amount;

            // Add Record
            const txn = {
                id: "TXN" + Math.floor(Math.random() * 899999 + 100000),
                type: "DEBIT",
                title: details.recipient,
                sub: details.note,
                amount: details.amount,
                date: "Just Now",
                status: "SUCCESS"
            };

            currentUser.transactions.unshift(txn);
            saveUserData();
            updateUI();

            // Populate Success Screen
            document.getElementById('successRecipient').innerText = details.recipient;
            document.getElementById('successAmount').innerText = "₹" + details.amount;
            document.getElementById('successTxnId').innerText = "Txn ID: " + txn.id;

            openModal('successModal');

            // Trigger Confetti Celebration
            if (typeof confetti === 'function') {
                confetti({
                    particleCount: 80,
                    spread: 60,
                    origin: { y: 0.6 }
                });
            }

            // Close inputs
            closeModal('sendMoneyModal');
            closeModal('rechargeModal');
            closeModal('toBankModal');
        }

        function closeSuccessModal() {
            closeModal('successModal');
        }

        // Generate QR Code dynamically
        function initQrCode() {
            const container = document.getElementById('qrcodeContainer');
            if (container) {
                container.innerHTML = "";
                new QRCode(container, {
                    text: `upi://pay?pa=${currentUser.phone}@ybl&pn=${encodeURIComponent(currentUser.name)}&cu=INR`,
                    width: 160,
                    height: 160,
                    colorDark: "#5f259f",
                    colorLight: "#ffffff"
                });
            }
        }

        // Scanner Functions
        function startScanner() {
            try {
                if (!qrScannerInstance) {
                    qrScannerInstance = new Html5Qrcode("reader");
                }
                qrScannerInstance.start(
                    { facingMode: "environment" },
                    { fps: 10, qrbox: 200 },
                    (decodedText) => {
                        stopScanner();
                        closeModal('qrScannerModal');
                        simulateScanQuickPay();
                    },
                    (errorMessage) => { /* ignore frame errors */ }
                ).catch(err => console.log(err));
            } catch(e) {
                console.log(e);
            }
        }

        function stopScanner() {
            if (qrScannerInstance) {
                qrScannerInstance.stop().then(() => {
                    qrScannerInstance.clear();
                }).catch(err => console.log(err));
            }
        }

        function simulateScanQuickPay() {
            stopScanner();
            closeModal('qrScannerModal');
            document.getElementById('payRecipientInput').value = "Merchant Store / QR Pay";
            document.getElementById('payAmountInput').value = "50";
            openModal('sendMoneyModal');
        }

        // New User Registration with ₹88 Bonus logic
        function registerNewUser() {
            const name = document.getElementById('newUserNameInput').value.trim();
            const phone = document.getElementById('newUserPhoneInput').value.trim();

            if (!name || phone.length < 10) {
                showToast('Enter valid Name & 10-digit Phone Number');
                return;
            }

            currentUser = {
                name: name,
                phone: phone,
                upiId: phone + "@ybl",
                balance: 88, // New Account Bonus Guarantee
                pin: "1234",
                transactions: [
                    {
                        id: "TXN" + Math.floor(Math.random() * 899999 + 100000),
                        type: "CREDIT",
                        title: "PhonePe Bonus",
                        sub: "New Account Bonus Credited",
                        amount: 88,
                        date: "Just Now",
                        status: "SUCCESS"
                    }
                ]
            };

            saveUserData();
            updateUI();
            initQrCode();
            closeModal('profileModal');
            showToast('Account Created! ₹88 Bonus Added to Balance 🎉');
        }

        // Add Demo Funds
        function addDemoBalance(amount) {
            currentUser.balance += amount;
            currentUser.transactions.unshift({
                id: "TXN" + Math.floor(Math.random() * 899999 + 100000),
                type: "CREDIT",
                title: "Added Demo Cash",
                sub: "Self Deposit",
                amount: amount,
                date: "Just Now",
                status: "SUCCESS"
            });
            saveUserData();
            updateUI();
            showToast(`₹${amount} added successfully!`);
        }

        // Reset App Data
        function resetAccountData() {
            localStorage.removeItem('phonepe_user_data');
            loadUserData();
            updateUI();
            initQrCode();
            closeModal('profileModal');
            showToast('Account data reset to default!');
        }

        // Toast Helper
        function showToast(msg) {
            const toast = document.getElementById('toast');
            toast.innerText = msg;
            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3000);
        }

        // Simple Search Simulation
        function handleSearch(val) {
            if(val.length > 2) {
                showToast(`Searching for "${val}"...`);
            }
        }
    </script>
</body>
</html>
```
