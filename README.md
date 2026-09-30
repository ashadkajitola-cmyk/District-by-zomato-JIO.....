<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Betting Platform Pro Max</title>
    <style>
        :root {
            --primary: #1e3c72;
            --secondary: #2a5298;
            --accent: #ff9800;
            --bg: #f0f4f8;
            --white: #ffffff;
            --text: #222222;
            --danger: #e74c3c;
            --success: #2ecc71;
            --border: #dcdcdc;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--bg); color: var(--text); padding-bottom: 60px; font-size: 16px; }
        
        header { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: var(--white); padding: 20px 25px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 4px 20px rgba(0,0,0,0.2); }
        header h1 { font-size: 1.5rem; font-weight: 800; letter-spacing: 0.5px; }
        .user-info { display: flex; gap: 15px; align-items: center; font-size: 1rem; }
        .wallet-badge { background: var(--accent); color: #000; padding: 8px 16px; border-radius: 30px; font-weight: bold; font-size: 1.05rem; box-shadow: 0 3px 6px rgba(0,0,0,0.15); }
        
        .container { max-width: 950px; margin: 25px auto; padding: 0 15px; display: flex; flex-direction: column; gap: 20px; }
        .card { background: var(--white); border-radius: 14px; padding: 25px; box-shadow: 0 6px 18px rgba(0,0,0,0.06); }
        
        h2 { font-size: 1.5rem; margin-bottom: 12px; color: var(--primary); font-weight: 700; }
        h3 { font-size: 1.25rem; margin-bottom: 10px; color: #333; font-weight: 700; }
        
        .btn { background: var(--secondary); color: var(--white); border: none; padding: 14px 20px; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 1.05rem; transition: 0.2s; box-shadow: 0 3px 6px rgba(0,0,0,0.1); width: 100%; text-align: center; display: inline-block; }
        .btn:hover { opacity: 0.92; transform: translateY(-2px); }
        .btn-danger { background: var(--danger); }
        .btn-success { background: var(--success); }
        .btn-warning { background: var(--accent); color: #000; }
        .btn-primary { background: var(--secondary); color: var(--white); }
        
        input, select, textarea { width: 100%; padding: 14px 16px; margin: 8px 0 18px 0; border: 2px solid var(--border); border-radius: 8px; font-size: 1.05rem; background: #fff; }
        input:focus, select:focus { border-color: var(--secondary); outline: none; }
        label { font-weight: 700; font-size: 0.95rem; color: #444; display: block; margin-top: 5px; }
        
        .tabs { display: flex; gap: 8px; margin-bottom: 15px; background: #e2e8f0; padding: 6px; border-radius: 10px; flex-wrap: wrap; }
        .tab-btn { flex: 1; min-width: 120px; padding: 12px; background: transparent; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; color: #555; transition: 0.2s; font-size: 0.95rem; text-align: center; }
        .tab-btn.active { background: var(--white); color: var(--primary); box-shadow: 0 3px 8px rgba(0,0,0,0.1); }
        
        .match-card { border: 2px solid var(--border); border-radius: 12px; padding: 20px; margin-bottom: 18px; background: var(--white); box-shadow: 0 3px 8px rgba(0,0,0,0.03); }
        .series-title-bar { background: #e8f4fd; color: #1a5276; padding: 10px 15px; border-radius: 8px; font-weight: bold; font-size: 1.05rem; margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center; }
        .match-row { display: flex; justify-content: space-between; align-items: center; margin: 15px 0; }
        .team-box { font-size: 1.25rem; font-weight: 800; display: flex; align-items: center; gap: 10px; color: var(--primary); }
        .vs-text { font-weight: 800; color: #777; font-size: 1.1rem; text-align: center; display: flex; flex-direction: column; align-items: center; gap: 4px; }
        .match-format-green { background: var(--success); color: #fff; padding: 3px 10px; border-radius: 20px; font-size: 0.8rem; font-weight: bold; letter-spacing: 0.5px; }
        
        .toss-display-box {
            background: #fff3cd; color: #856404; border: 1px solid #ffeeba;
            padding: 8px 12px; border-radius: 6px; font-size: 0.95rem; font-weight: bold; margin: 10px 0; text-align: center;
        }

        .result-display-box {
            background: #f8d7da; color: #721c24; border: 1px solid #f5c6cb;
            padding: 8px 12px; border-radius: 6px; font-size: 0.95rem; font-weight: bold; margin: 10px 0; text-align: center;
        }

        .plan-card-item {
            background: #fff; border: 2px solid var(--border); border-radius: 12px;
            padding: 16px 20px; display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 12px; box-shadow: 0 2px 6px rgba(0,0,0,0.03); transition: 0.2s; flex-wrap: wrap; gap: 15px;
        }
        .plan-card-item:hover { border-color: var(--secondary); }
        .plan-info-group { display: flex; gap: 25px; align-items: center; flex-wrap: wrap; }
        .plan-price-tag { font-size: 1.6rem; font-weight: 900; color: var(--primary); letter-spacing: -0.5px; }
        .plan-meta-col { display: flex; flex-direction: column; }
        .plan-meta-label { font-size: 0.75rem; color: #777; font-weight: bold; letter-spacing: 0.5px; }
        .plan-meta-val { font-size: 1.05rem; color: #333; font-weight: 700; line-height: 1.5; }

        .physical-ticket {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 50%, #ff9800 100%);
            color: #fff; border-radius: 16px; padding: 22px; margin-bottom: 24px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.25); border: 2px dashed rgba(255,255,255,0.7);
        }
        .ticket-header { display: flex; justify-content: space-between; align-items: center; font-size: 0.95rem; text-transform: uppercase; letter-spacing: 1px; border-bottom: 1px solid rgba(255,255,255,0.4); padding-bottom: 10px; margin-bottom: 14px; font-weight: bold; }
        .ticket-teams-title { font-size: 1.8rem; font-weight: 900; letter-spacing: 1px; text-align: center; margin: 12px 0; text-shadow: 2px 2px 6px rgba(0,0,0,0.3); }
        .ticket-footer { display: flex; justify-content: space-between; align-items: center; background: rgba(255,255,255,0.95); color: #333; padding: 12px 16px; border-radius: 8px; font-size: 0.95rem; font-weight: bold; }

        .message-item {
            background: #fff; border: 2px solid var(--border); border-radius: 10px;
            padding: 16px; margin-bottom: 12px; cursor: pointer; transition: 0.2s; box-shadow: 0 2px 5px rgba(0,0,0,0.03);
        }
        .message-item:hover { border-color: var(--primary); background: #f8fafc; }
        .message-header-bar { display: flex; justify-content: space-between; align-items: center; font-weight: bold; color: var(--primary); font-size: 1.1rem; }

        .hidden { display: none !important; }
        .flex-row { display: flex; gap: 12px; }
        .flex-row > * { flex: 1; }
        
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); display: flex; justify-content: center; align-items: center; z-index: 1000; overflow-y: auto; padding: 20px; }
        .modal-content { background: var(--white); padding: 30px; border-radius: 16px; width: 100%; max-width: 650px; position: relative; max-height: 90vh; overflow-y: auto; box-shadow: 0 10px 30px rgba(0,0,0,0.3); }
        .close-modal { position: absolute; top: 15px; right: 20px; font-size: 1.8rem; cursor: pointer; color: #666; font-weight: bold; }
    </style>
</head>
<body>

    <header>
        <h1>🏏 Cricket Schedule & Betting Pro</h1>
        <div class="user-info">
            <span id="displayNumber" style="font-weight: 700;">Login करें</span>
            <span class="wallet-badge">Wallet: ₹<span id="displayWallet">0</span></span>
            <button class="btn btn-danger" onclick="logout()" style="padding: 8px 16px; font-size: 0.9rem; width: auto;">Logout</button>
        </div>
    </header>

    <div class="container">
        <!-- Login Section -->
        <div id="loginSection" class="card">
            <h2>🔐 Login / Register</h2>
            <p id="deviceLimitInfo" style="font-size:0.95rem; color:#555; margin-bottom:15px;"></p>
            <label>Mobile Number:</label>
            <input type="text" id="loginMobileInput" placeholder="Enter 10-digit mobile number">
            <label>6-Digit UPI PIN:</label>
            <input type="password" id="loginUpiPinInput" maxlength="6" placeholder="Enter 6-digit UPI PIN">
            <button class="btn" onclick="handleLogin()">Login to Dashboard</button>
        </div>

        <!-- Main Dashboard -->
        <div id="mainDashboard" class="hidden">
            
            <div id="activeSubStatusBox" class="card" style="border-left: 6px solid var(--primary); background: #f8fafc;">
                <h3>✨ Active Subscription Status</h3>
                <div id="subStatusContent" style="margin-top: 10px; font-size: 1.05rem; font-weight: 600; color: #1e3c72;">No Plan</div>
            </div>

            <!-- Subscription Hub Card -->
            <div class="card" style="border-left: 6px solid var(--accent); background: #fffbeb;">
                <h3>📦 Subscription Plans Hub</h3>
                <p style="font-size: 0.95rem; color: #555; margin-bottom: 15px;">Apna match schedule create karne ke liye ya discount/cashback paane ke liye niche diye gaye plans mein se koi plan select karke <b>Buy</b> karein:</p>
                <div id="subPlansList" style="margin-bottom: 5px;"></div>
            </div>

            <div class="card" style="border-left: 6px solid var(--success);">
                <h3>💳 Instant Wallet Recharge (Transaction ID / UTR)</h3>
                <p style="font-size: 0.95rem; color: #555; margin-bottom: 12px;">Payment ki Transaction ID / UTR number yahan dalein. <b>(Note: Sim card par active mobile recharge hona zaroori hai, Wi-Fi users allow nahi hain. Har 29 din me sirf 1 baar reward milega).</b></p>
                <label>Full Transaction ID / UTR:</label>
                <input type="text" id="txFullInput" placeholder="Enter transaction reference ID">
                <button class="btn btn-success" onclick="submitInstantRecharge()">Confirm & Get ₹210 Instantly</button>
            </div>

            <div class="card" style="border-left: 6px solid var(--secondary);">
                <h3>📂 Creator & Schedule Panel</h3>
                <p style="font-size: 0.95rem; color: #555; margin-bottom: 12px;">Apna match schedule create karne ke liye panel open karein (Active subscription zaroori hai).</p>
                <button class="btn" onclick="openCreatorDashboard()">Open Creator Panel</button>
            </div>

            <div id="adminMainControlCard" class="card hidden" style="border-left: 6px solid var(--danger); background: #fdfefe;">
                <h3 style="color: var(--danger);">👑 Master Website Admin Control Center</h3>
                <p style="font-size: 0.95rem; color: #555; margin-bottom: 15px;">Yahan se aap saare matches, tickets aur subscription plans ko manage kar sakte hain.</p>
                <div>
                    <button class="btn btn-danger" style="width: 100%;" onclick="openMasterAdminPanel()">⚙️ Manage Matches, Tickets & Plans</button>
                </div>
            </div>

            <div class="card">
                <h3>🔍 6-Digit Code Verification</h3>
                <div class="flex-row">
                    <input type="text" id="verifyCodeInput" maxlength="6" placeholder="Enter 6-digit match code">
                    <button class="btn" onclick="verifyMatchCode()" style="height: 52px; margin-top: 8px;">Check Code</button>
                </div>
                <div id="verifyResult" style="margin-top: 12px;"></div>
            </div>

            <!-- Top Navigation Tabs -->
            <div class="tabs">
                <button class="tab-btn active" onclick="switchTab('international', event)">🌍 Matches</button>
                <button class="tab-btn" onclick="switchTab('apna', event)">👤 Apna</button>
                <button class="tab-btn" onclick="switchTab('activeTickets', event)">🎟️ Tickets & Betting</button>
                <button class="tab-btn" onclick="switchTab('myPurchased', event)">📦 History</button>
                <button class="tab-btn" onclick="switchTab('messages', event)">📥 Messages</button>
            </div>

            <!-- Tab Content Sections -->
            <div id="internationalTabContent" class="tab-content card">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px;">
                    <h2>International Matches</h2>
                    <button id="adminCreateMatchBtn" class="btn btn-success hidden" style="width: auto;" onclick="openInternationalMatchModal()">+ Create Match</button>
                </div>
                <div id="internationalMatchesList" style="margin-top: 15px;"></div>
            </div>

            <div id="apnaTabContent" class="tab-content card hidden">
                <h2>Apna Schedule (User Created)</h2>
                <div id="apnaMatchesList" style="margin-top: 15px;"></div>
            </div>

            <div id="activeTicketsTabContent" class="tab-content card hidden">
                <h2>Active Ticket District & Store</h2>
                <div id="activeTicketsList" style="margin-top: 15px;"></div>
            </div>

            <div id="myPurchasedTabContent" class="tab-content card hidden">
                <h2>All Purchased Tickets & Betting Store</h2>
                <div id="myPurchasedList" style="margin-top: 15px;"></div>
            </div>

            <div id="messagesTabContent" class="tab-content card hidden">
                <h2>📥 Messages Inbox</h2>
                <p style="font-size:0.95rem; color:#555; margin-bottom:15px;">Yahan aapke subscription recharges ke messages dikhenge. Details dekhne ke liye message par click karein.</p>
                <div id="messagesInboxList"></div>
            </div>

        </div>
    </div>

    <!-- Jio Style Recharge Confirmation Modal -->
    <div id="jioCheckoutModal" class="modal hidden">
        <div class="modal-content" style="max-width: 480px; padding: 25px;">
            <span class="close-modal" onclick="closeJioModal()">&times;</span>
            <div style="display:flex; justify-content:space-between; align-items:center; border-bottom:1px solid #eee; padding-bottom:12px; margin-bottom:15px;">
                <h3 style="color:#111; font-size:1.3rem;">Recharge</h3>
                <span id="jioModalMobile" style="color:#666; font-weight:bold;"></span>
            </div>
            <div style="font-size: 2.2rem; font-weight: 900; color: #111; margin-bottom: 4px;" id="jioModalPrice">₹0</div>
            <div style="color: #ff9800; font-weight: bold; font-size: 0.95rem; margin-bottom: 20px;" id="jioModalTag">PRO SUBSCRIPTION PACK</div>

            <div style="background:#f8fafc; border:1px solid var(--border); border-radius:12px; padding:15px; margin-bottom:20px;">
                <h4 style="font-size: 1.05rem; color: #333; margin-bottom: 12px; border-bottom:1px solid #ddd; padding-bottom:6px;">Plan details</h4>
                <div style="display:flex; justify-content:space-between; margin-bottom:10px; font-size:0.95rem;">
                    <span style="color:#666;">Pack validity</span>
                    <strong id="jioModalValidity" style="color:#222;">30 Days</strong>
                </div>
                <div style="display:flex; justify-content:space-between; margin-bottom:10px; font-size:0.95rem;">
                    <span style="color:#666;">Free Tickets</span>
                    <strong id="jioModalFreeTkt" style="color:#222;">0</strong>
                </div>
                <div style="display:flex; justify-content:space-between; margin-bottom:10px; font-size:0.95rem;">
                    <span style="color:#666;">Discount / Cashback</span>
                    <strong id="jioModalPerks" style="color:#222;">-</strong>
                </div>
            </div>

            <label>Enter 6-Digit UPI PIN:</label>
            <input type="password" id="jioUpiPinInput" maxlength="6" placeholder="Enter 6-digit UPI PIN">

            <button class="btn btn-primary" style="background:#1932ff; border-radius:30px; font-size:1.1rem; padding:16px; margin-top:10px;" id="jioPayBtn" onclick="confirmJioPayment()">Pay ₹0</button>
        </div>
    </div>

    <!-- Modals -->
    <div id="creatorModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeCreatorModal()">&times;</span>
            <div id="subscriptionRequiredView">
                <h3 style="color: var(--danger);">📢 Subscription Required</h3>
                <p style="font-size:0.95rem; color:#555; margin-bottom:15px;">Apna match schedule create karne ke liye pehle subscription plan active karein.</p>
            </div>
            <div id="creatorActionView" class="hidden">
                <h3 style="color: var(--success);">👤 Creator Panel (Schedule Only)</h3>
                <p style="font-size: 1rem; color: #333; margin-bottom: 15px; font-weight: bold;">✔ Aapke paas active subscription hai. Aap match schedule create kar sakte hain:</p>
                <button class="btn" onclick="openMatchModal()">🏏 Create Match Schedule Only</button>
            </div>
        </div>
    </div>

    <div id="matchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeMatchModal()">&times;</span>
            <h2 id="matchModalTitle">🏏 Create Match Schedule</h2>
            <input type="hidden" id="editingMatchId" value="">
            
            <label>Series Type:</label>
            <select id="matchSeriesType" onchange="toggleSeriesInput('match')">
                <option value="existing">Existing Series (Auto-select)</option>
                <option value="new">New Series (Enter Name)</option>
            </select>

            <div id="matchExistingSeriesContainer">
                <label>Select Existing Series:</label>
                <select id="matchExistingSeriesSelect"></select>
            </div>

            <div id="matchNewSeriesContainer" class="hidden">
                <label>New Series Name:</label>
                <input type="text" id="matchSeriesName" placeholder="e.g., Local League 2026">
            </div>

            <div class="flex-row">
                <div><label>Team 1 Name:</label><input type="text" id="matchTeam1" placeholder="Team A" oninput="updateTossTeamDropdowns('match')"></div>
                <div><label>Team 2 Name:</label><input type="text" id="matchTeam2" placeholder="Team B" oninput="updateTossTeamDropdowns('match')"></div>
            </div>

            <div class="flex-row">
                <div><label>Match Format:</label><input type="text" id="matchFormat" placeholder="4TH T20I"></div>
                <div><label>Date & Time:</label><input type="text" id="matchDateTime" placeholder="WED, 17 DEC, 2026 | 7 PM"></div>
            </div>

            <label>Venue (Stadium Name):</label>
            <input type="text" id="matchVenue" placeholder="EKANA STADIUM, LUCKNOW">

            <label>Gate Open Time:</label>
            <input type="text" id="matchGateTime" placeholder="Gate Opens: 2 Hours Before">

            <label>6-Digit Security Code:</label>
            <input type="text" id="matchCode6" maxlength="6" placeholder="6 digit code">

            <!-- Toss Section -->
            <fieldset style="border: 2px dashed var(--accent); padding: 15px; border-radius: 8px; margin-bottom: 18px;">
                <legend style="font-weight: bold; color: #b78103; padding: 0 6px;">🪙 Toss Details</legend>
                <label>Toss Winner Team:</label>
                <select id="matchTossWinner">
                    <option value="">Toss kisne jeeta?</option>
                </select>
                <label>Toss Choice:</label>
                <select id="matchTossChoice">
                    <option value="">Kya faisla kiya?</option>
                    <option value="Batting">Batting</option>
                    <option value="Bowling">Bowling</option>
                </select>
            </fieldset>

            <label>Result / Winner Status:</label>
            <select id="matchResultStatus" onchange="toggleResultMarginInput('match')">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <div id="matchResultMarginContainer" class="hidden">
                <label>Result Margin (e.g., 5 Runs / 6 Wickets):</label>
                <input type="text" id="matchResultMargin" placeholder="e.g., 6 Wickets se jeeta">
            </div>

            <button class="btn btn-success" style="margin-top:10px;" onclick="saveMatchSchedule(false)">Save & Publish Match</button>
        </div>
    </div>

    <div id="internationalMatchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeInternationalMatchModal()">&times;</span>
            <h2 id="intModalTitle">🌍 Create International Match (Admin Only)</h2>
            <input type="hidden" id="editingIntMatchId" value="">
            
            <label>Series Type:</label>
            <select id="intSeriesType" onchange="toggleSeriesInput('int')">
                <option value="existing">Existing Series (Auto-select)</option>
                <option value="new">New Series (Enter Name)</option>
            </select>

            <div id="intExistingSeriesContainer">
                <label>Select Existing Series:</label>
                <select id="intExistingSeriesSelect"></select>
            </div>

            <div id="intNewSeriesContainer" class="hidden">
                <label>New Series Name:</label>
                <input type="text" id="intSeriesName" placeholder="IND vs SA Series">
            </div>

            <div class="flex-row">
                <div><label>Team 1:</label><input type="text" id="intTeam1" placeholder="IND" oninput="updateTossTeamDropdowns('int')"></div>
                <div><label>Team 2:</label><input type="text" id="intTeam2" placeholder="SA" oninput="updateTossTeamDropdowns('int')"></div>
            </div>

            <div class="flex-row">
                <div><label>Match Format:</label><input type="text" id="intFormat" placeholder="4TH T20I"></div>
                <div><label>Date & Time:</label><input type="text" id="intDateTime" placeholder="WED, 17 DEC, 2026 | 7 PM"></div>
            </div>

            <label>Venue:</label>
            <input type="text" id="intVenue" placeholder="Stadium Name">

            <label>Gate Open Time:</label>
            <input type="text" id="intGateTime" placeholder="Gate Opens info">

            <div class="flex-row">
                <div><label>Ticket Price (₹):</label><input type="number" id="intPrice" placeholder="200"></div>
                <div><label>Ticket Limit:</label><input type="number" id="intLimit" placeholder="100"></div>
            </div>

            <label>6-Digit Security Code:</label>
            <input type="text" id="intCode6" maxlength="6" placeholder="6 digit code">

            <!-- Toss Section -->
            <fieldset style="border: 2px dashed var(--accent); padding: 15px; border-radius: 8px; margin-bottom: 18px;">
                <legend style="font-weight: bold; color: #b78103; padding: 0 6px;">🪙 Toss Details</legend>
                <label>Toss Winner Team:</label>
                <select id="intTossWinner">
                    <option value="">Toss kisne jeeta?</option>
                </select>
                <label>Toss Choice:</label>
                <select id="intTossChoice">
                    <option value="">Kya faisla kiya?</option>
                    <option value="Batting">Batting</option>
                    <option value="Bowling">Bowling</option>
                </select>
            </fieldset>

            <label>Result Status:</label>
            <select id="intResultStatus" onchange="toggleResultMarginInput('int')">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <div id="intResultMarginContainer" class="hidden">
                <label>Result Margin (e.g., 5 Runs / 6 Wickets):</label>
                <input type="text" id="intResultMargin" placeholder="e.g., 5 Runs se jeeta">
            </div>

            <button class="btn btn-success" style="margin-top:10px;" onclick="saveMatchSchedule(true)">Publish International Match</button>
        </div>
    </div>

    <!-- Betting Modal -->
    <div id="bettingModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeBettingModal()">&times;</span>
            <h3 style="color: var(--primary);">🎲 Place Your Bet (Satta Lagayein)</h3>
            <p id="betMatchInfo" style="font-size: 1rem; color: #555; margin-bottom: 15px; font-weight: bold;"></p>
            
            <label>Select Ticket to Use (1 Ticket = 1 Bet):</label>
            <select id="betTicketSelect">
                <option value="">Apni Active Ticket Chunein</option>
            </select>

            <label>Select Team to Win:</label>
            <select id="betSelectedTeam">
                <option value="">Team Chunein</option>
            </select>

            <label>Bet Amount (₹):</label>
            <input type="number" id="betAmountInput" placeholder="Enter amount to bet">

            <label>Enter 6-Digit UPI PIN:</label>
            <input type="password" id="betUpiPinInput" maxlength="6" placeholder="Enter 6-digit UPI PIN">

            <button class="btn btn-warning" onclick="confirmPlaceBet()">Place Bet Now</button>
        </div>
    </div>

    <!-- Message Detail Modal -->
    <div id="messageDetailModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeMessageDetailModal()">&times;</span>
            <h3 style="color: var(--success); margin-bottom: 15px;">✅ Recharge Safal Raha</h3>
            <div id="messageDetailContent" style="font-size: 1.05rem; line-height: 1.6; color: #333;"></div>
            <button class="btn btn-danger" style="margin-top: 20px;" id="deleteMsgModalBtn">Delete Message</button>
        </div>
    </div>

    <div id="masterAdminModal" class="modal hidden">
        <div class="modal-content" style="max-width: 750px;">
            <span class="close-modal" onclick="closeMasterAdminPanel()">&times;</span>
            <h2>⚙️ Master Admin Panel</h2>
            
            <div class="tabs" style="margin-bottom:15px;">
                <button class="tab-btn active" onclick="switchAdminSubTab('matches', event)">Matches</button>
                <button class="tab-btn" onclick="switchAdminSubTab('tickets', event)">All Tickets & Bets</button>
                <button class="tab-btn" onclick="switchAdminSubTab('plans', event)">Subscriptions</button>
            </div>

            <div id="adminTabMatches" class="admin-sub-tab"><div id="adminAllMatchesList"></div></div>
            <div id="adminTabTickets" class="admin-sub-tab hidden"><div id="adminAllTicketsList"></div></div>
            <div id="adminTabPlans" class="admin-sub-tab hidden">
                <div id="adminPlansList" style="margin-bottom: 15px;"></div>
                <hr style="margin: 15px 0;">
                <h3>Add New Subscription Plan</h3>
                <label>Plan ID:</label><input type="text" id="newPlanId" placeholder="e.g., special_pro">
                <label>Plan Name:</label><input type="text" id="newPlanName" placeholder="e.g., 30 Days Pro Plan">
                <div class="flex-row">
                    <div><label>Price (₹):</label><input type="number" id="newPlanPrice" placeholder="299"></div>
                    <div><label>Duration Days:</label><input type="number" id="newPlanDays" placeholder="30"></div>
                </div>
                <div class="flex-row">
                    <div><label>Free Tickets Count:</label><input type="number" id="newPlanFreeTickets" placeholder="4"></div>
                    <div><label>Ticket Discount (%):</label><input type="number" id="newPlanDiscount" placeholder="35"></div>
                </div>
                <div>
                    <label>Betting Cashback/Commission (% or multiplier info, e.g. 6 for 6x):</label>
                    <input type="number" id="newPlanCashback" placeholder="e.g., 6 (for 6x payout)">
                </div>
                <button class="btn btn-success" onclick="addNewSubscriptionPlan()">Add New Plan</button>
            </div>
        </div>
    </div>

    <script>
        const DEFAULT_ADMIN = "7355055313";
        
        let db = JSON.parse(localStorage.getItem('cricket_pro_db')) || {
            users: {},
            matches: [],
            tickets: [],
            bets: [],
            messages: [],
            usedTransactions: [],
            userRechargeTimestamps: {}, 
            settings: {
                adminNumber: DEFAULT_ADMIN,
                maxDevices: 15,
                plans: [
                    { id: '30days_plan', name: '30 Days Pro Plan', price: 299, durationDays: 30, freeTickets: 4, discountPercent: 35, cashbackPercent: 6 }
                ]
            },
            deviceSessions: {}
        };

        db.settings.adminNumber = DEFAULT_ADMIN;
        db.settings.maxDevices = 15;
        if (!db.userRechargeTimestamps) db.userRechargeTimestamps = {};
        if (!db.messages) db.messages = [];
        if (!db.bets) db.bets = [];

        let currentMobile = localStorage.getItem('cricket_pro_current_mobile') || null;
        let deviceId = localStorage.getItem('cricket_pro_device_id') || 'dev_' + Math.random().toString(36).substring(2,9);
        localStorage.setItem('cricket_pro_device_id', deviceId);

        let activeBetMatchId = null;
        let pendingCheckoutPlanId = null;

        function saveDB() {
            localStorage.setItem('cricket_pro_db', JSON.stringify(db));
        }

        window.onload = function() {
            if (!db.users[db.settings.adminNumber]) {
                db.users[db.settings.adminNumber] = { wallet: 0, subscription: null, freeTicketsLeft: 0, upiPin: "123456" };
            }
            if (currentMobile && db.users[currentMobile]) {
                showDashboard();
            } else {
                currentMobile = null;
                showLogin();
            }
        };

        function showLogin() {
            document.getElementById('loginSection').classList.remove('hidden');
            document.getElementById('mainDashboard').classList.add('hidden');
            let infoEl = document.getElementById('deviceLimitInfo');
            if(infoEl) infoEl.innerText = `(Max ${db.settings.maxDevices} numbers allowed per device)`;
        }

        function showDashboard() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('mainDashboard').classList.remove('hidden');
            
            let isAdmin = (currentMobile === db.settings.adminNumber);
            if (isAdmin) {
                document.getElementById('adminCreateMatchBtn').classList.remove('hidden');
                document.getElementById('adminMainControlCard').classList.remove('hidden');
            } else {
                document.getElementById('adminCreateMatchBtn').classList.add('hidden');
                document.getElementById('adminMainControlCard').classList.add('hidden');
            }

            updateHeader();
            renderSubscriptionStatusBox();
            renderSubscriptionPlansHub();
            renderMatches();
            renderActiveTickets();
            renderMyPurchasedTickets();
            renderMessagesInbox();
        }

        function handleLogin() {
            let mobile = document.getElementById('loginMobileInput').value.trim();
            let upiPin = document.getElementById('loginUpiPinInput').value.trim();

            if (!mobile || mobile.length < 10) { alert("Kripya sahi 10-digit mobile number enter karein!"); return; }
            if (!upiPin || upiPin.length !== 6) { alert("Kripya 6-digit ka valid UPI PIN enter karein!"); return; }

            if (!db.deviceSessions[deviceId]) db.deviceSessions[deviceId] = [];
            let activeNumbers = db.deviceSessions[deviceId];
            
            if (!activeNumbers.includes(mobile)) {
                if (activeNumbers.length >= db.settings.maxDevices) {
                    alert(`Is device par maximum ${db.settings.maxDevices} numbers hi allow hain!`);
                    return;
                }
                activeNumbers.push(mobile);
            }

            if (!db.users[mobile]) {
                let initialWallet = (mobile === db.settings.adminNumber) ? 0 : 200;
                db.users[mobile] = { wallet: initialWallet, subscription: null, freeTicketsLeft: 0, upiPin: upiPin };
            } else {
                if (!db.users[mobile].upiPin) {
                    db.users[mobile].upiPin = upiPin;
                } else if (db.users[mobile].upiPin !== upiPin) {
                    alert("Galat UPI PIN! Kripya sahi UPI PIN enter karein.");
                    return;
                }
            }

            currentMobile = mobile;
            localStorage.setItem('cricket_pro_current_mobile', currentMobile);
            saveDB();
            showDashboard();
        }

        function logout() {
            currentMobile = null;
            localStorage.removeItem('cricket_pro_current_mobile');
            showLogin();
        }

        function updateHeader() {
            document.getElementById('displayNumber').innerText = currentMobile;
            let user = db.users[currentMobile];
            document.getElementById('displayWallet').innerText = user ? user.wallet : 0;
        }

        function submitInstantRecharge() {
            let txInput = document.getElementById('txFullInput').value.trim();
            if (!txInput || txInput.length < 6) { alert("Kripya valid Transaction ID / UTR enter karein!"); return; }

            let hasCarrierRecharge = confirm("System verification check: Kya aapke is mobile number (" + currentMobile + ") par sim card mein active mobile recharge maujood hai? (OK = Haan, Cancel = Nahi / Wi-Fi user)");
            if (!hasCarrierRecharge) {
                alert("Recharge failed! Aapka mobile number active carrier recharge ke bina verified nahi ho saka.");
                return;
            }

            if (!db.usedTransactions) db.usedTransactions = [];
            if (db.usedTransactions.includes(txInput)) { alert("Yeh Transaction ID pehle hi use ki ja chuki hai!"); return; }

            let now = new Date().getTime();
            let lastRechargeTime = db.userRechargeTimestamps[currentMobile] || 0;
            let twentyNineDaysInMs = 29 * 24 * 60 * 60 * 1000;

            if (now - lastRechargeTime < twentyNineDaysInMs) {
                let remainingDays = Math.ceil((twentyNineDaysInMs - (now - lastRechargeTime)) / (1000 * 60 * 60 * 24));
                alert(`Aap pichle 29 dino me recharge kar chuke hain. Aap agla recharge ${remainingDays} dino ke baad kar sakte hain.`);
                return;
            }

            db.usedTransactions.push(txInput);
            db.userRechargeTimestamps[currentMobile] = now;

            if (!db.users[currentMobile]) db.users[currentMobile] = { wallet: 0, subscription: null, freeTicketsLeft: 0 };
            db.users[currentMobile].wallet += 210;

            saveDB();
            updateHeader();
            document.getElementById('txFullInput').value = '';
            alert("Transaction successfully confirm ho gayi! Aapke wallet mein ₹210 turant add kar diye gaye hain.");
        }

        function checkUserHasActiveSub() {
            let isAdmin = (currentMobile === db.settings.adminNumber);
            if (isAdmin) return true;
            let user = db.users[currentMobile];
            if (user && user.subscription) {
                return new Date().getTime() < user.subscription.expiresAt;
            }
            return false;
        }

        function renderSubscriptionStatusBox() {
            let content = document.getElementById('subStatusContent');
            let user = db.users[currentMobile];
            let isAdmin = (currentMobile === db.settings.adminNumber);

            if (isAdmin) {
                content.innerHTML = `Role: Master Website Admin (Full Unlimited Access)`;
                return;
            }

            if (user && user.subscription && checkUserHasActiveSub()) {
                let sub = user.subscription;
                let now = new Date().getTime();
                let diffMs = sub.expiresAt - now;
                let diffHrs = Math.floor(diffMs / (1000 * 60 * 60));
                let diffDays = Math.floor(diffHrs / 24);
                
                let timeLeftText = diffDays > 0 ? `${diffDays} Days` : `${diffHrs} Hours`;
                let cashbackInfo = sub.cashbackPercent ? ` + Betting Multiplier: <b>${sub.cashbackPercent}x Payout</b>` : '';
                let discountInfo = sub.discountPercent ? ` + Discount: <b>${sub.discountPercent}%</b>` : '';
                content.innerHTML = `Plan Price: <b>₹${sub.planPrice}</b> &nbsp;|&nbsp; Remaining: <b>${timeLeftText}</b> &nbsp;|&nbsp; Free Tickets: <b>${user.freeTicketsLeft || 0}</b>${discountInfo}${cashbackInfo}`;
            } else {
                content.innerHTML = `No Plan`;
            }
        }

        function renderSubscriptionPlansHub() {
            let listHTML = '';
            db.settings.plans.forEach((plan) => {
                let validityText = plan.durationDays ? `${plan.durationDays} Days` : 'Active';
                let perkText = [];
                if (plan.freeTickets) perkText.push(`${plan.freeTickets} Free Tickets`);
                if (plan.discountPercent) perkText.push(`${plan.discountPercent}% Discount`);
                if (plan.cashbackPercent) perkText.push(`${plan.cashbackPercent}x Betting Payout`);
                let perksDesc = perkText.length > 0 ? perkText.join(' + ') : 'Standard Plan';

                listHTML += `
                    <div class="plan-card-item">
                        <div class="plan-info-group">
                            <div class="plan-price-tag">₹${plan.price}</div>
                            <div class="plan-meta-col">
                                <span class="plan-meta-label">Plan Details & Perks</span>
                                <span class="plan-meta-val">₹${plan.price} Plan<br><span style="color:var(--primary); font-size:0.95rem;">${perksDesc}</span></span>
                            </div>
                            <div class="plan-meta-col">
                                <span class="plan-meta-label">Validity</span>
                                <span class="plan-meta-val">${validityText}</span>
                            </div>
                        </div>
                        <button class="btn btn-primary" style="width: auto; padding: 10px 24px; font-size: 1rem;" onclick="openJioCheckoutModal('${plan.id}')">Buy</button>
                    </div>
                `;
            });
            document.getElementById('subPlansList').innerHTML = listHTML;
        }

        function openJioCheckoutModal(planId) {
            let planObj = db.settings.plans.find(p => p.id === planId);
            if (!planObj) return;
            pendingCheckoutPlanId = planId;

            document.getElementById('jioModalMobile').innerText = currentMobile;
            document.getElementById('jioModalPrice').innerText = `₹${planObj.price}`;
            document.getElementById('jioModalValidity').innerText = `${planObj.durationDays || 30} Days`;
            document.getElementById('jioModalFreeTkt').innerText = `${planObj.freeTickets || 0} Free Tickets`;
            
            let perksArr = [];
            if (planObj.discountPercent) perksArr.push(`${planObj.discountPercent}% Discount`);
            if (planObj.cashbackPercent) perksArr.push(`${planObj.cashbackPercent}x Payout`);
            document.getElementById('jioModalPerks').innerText = perksArr.length > 0 ? perksArr.join(' + ') : 'Standard';

            document.getElementById('jioPayBtn').innerText = `Pay ₹${planObj.price}`;
            document.getElementById('jioUpiPinInput').value = '';
            document.getElementById('jioCheckoutModal').classList.remove('hidden');
        }

        function closeJioModal() {
            document.getElementById('jioCheckoutModal').classList.add('hidden');
            pendingCheckoutPlanId = null;
        }

        function confirmJioPayment() {
            let pinInput = document.getElementById('jioUpiPinInput').value.trim();
            if (!pinInput || pinInput.length !== 6) { alert("Kripya 6-digit UPI PIN enter karein!"); return; }

            let user = db.users[currentMobile];
            if (user.upiPin && user.upiPin !== pinInput) { alert("Galat UPI PIN enter kiya gaya hai!"); return; }

            let planObj = db.settings.plans.find(p => p.id === pendingCheckoutPlanId);
            if (!planObj) { closeJioModal(); return; }

            if (user.wallet < planObj.price) { alert("Wallet me balance kam hai! Pehle Transaction ID daal kar ₹210 add karein."); return; }

            user.wallet -= planObj.price;
            let adminMob = db.settings.adminNumber;
            if (!db.users[adminMob]) db.users[adminMob] = { wallet: 0, subscription: null, freeTicketsLeft: 0 };
            db.users[adminMob].wallet += planObj.price;

            let now = new Date().getTime();
            let durationDays = planObj.durationDays || 30;
            let expiresAt = now + (durationDays * 24 * 3600 * 1000);

            user.subscription = {
                planId: planObj.id,
                planPrice: planObj.price,
                expiresAt: expiresAt,
                discountPercent: planObj.discountPercent || 0,
                cashbackPercent: planObj.cashbackPercent || 0
            };
            user.freeTicketsLeft = (user.freeTicketsLeft || 0) + (planObj.freeTickets || 0);

            let passId = generate12DigitPassId();
            let purchaseDateStr = new Date(now).toLocaleString();
            let expiryDateStr = new Date(expiresAt).toLocaleString();

            let msgObj = {
                id: 'msg_' + Date.now(),
                mobile: currentMobile,
                price: planObj.price,
                validityDays: durationDays,
                freeTickets: planObj.freeTickets || 0,
                discountPercent: planObj.discountPercent || 0,
                cashbackPercent: planObj.cashbackPercent || 0,
                passId: passId,
                purchaseDate: purchaseDateStr,
                expiryDate: expiryDateStr
            };

            if (!db.messages) db.messages = [];
            db.messages.unshift(msgObj);

            saveDB();
            updateHeader();
            renderSubscriptionStatusBox();
            renderMessagesInbox();
            closeJioModal();
            alert("UPI PIN Verified! Subscription successfully buy ho gaya aur message inbox mein bhej diya gaya hai.");
        }

        function generate12DigitPassId() {
            let chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
            let res = '';
            for (let i = 0; i < 12; i++) {
                res += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            return res;
        }

        function renderMessagesInbox() {
            let inboxListEl = document.getElementById('messagesInboxList');
            if (!db.messages) db.messages = [];
            let userMsgs = db.messages.filter(m => m.mobile === currentMobile);

            if (userMsgs.length === 0) {
                inboxListEl.innerHTML = '<p style="color:#666;">Aapke paas koi message nahi hai.</p>';
                return;
            }

            let html = '';
            userMsgs.forEach(msg => {
                html += `
                    <div class="message-item" onclick="openMessageDetail('${msg.id}')">
                        <div class="message-header-bar">
                            <span>recharge safal raha (₹${msg.price})</span>
                            <span style="font-size: 0.85rem; color: #666; font-weight: normal;">${msg.purchaseDate}</span>
                        </div>
                        <div style="font-size: 0.95rem; color: #555; margin-top: 5px;">Click karke poori jankari dekhein...</div>
                    </div>
                `;
            });
            inboxListEl.innerHTML = html;
        }

        function openMessageDetail(msgId) {
            let msg = db.messages.find(m => m.id === msgId);
            if (!msg) return;

            let contentHTML = `
                <p><strong>Plan Price:</strong> ₹${msg.price}</p>
                <p><strong>Mobile Number:</strong> ${msg.mobile}</p>
                <p><strong>Pass ID (12-Digit):</strong> <span style="font-family: monospace; background:#e2e8f0; padding:2px 6px; border-radius:4px;">${msg.passId}</span></p>
                <p><strong>Perks / Benefits:</strong><br>${msg.freeTickets} Free Tickets + ${msg.discountPercent}% Discount + ${msg.cashbackPercent}x Betting Payout</p>
                <p><strong>Validity:</strong> ${msg.validityDays} Days</p>
                <p><strong>Purchase Date:</strong> ${msg.purchaseDate}</p>
                <p><strong>Expiry Date:</strong> ${msg.expiryDate}</p>
            `;

            document.getElementById('messageDetailContent').innerHTML = contentHTML;
            document.getElementById('deleteMsgModalBtn').setAttribute('onclick', `deleteMessage('${msg.id}')`);
            document.getElementById('messageDetailModal').classList.remove('hidden');
        }

        function closeMessageDetailModal() {
            document.getElementById('messageDetailModal').classList.add('hidden');
        }

        function deleteMessage(msgId) {
            if (confirm("Kya aap is message ko delete karna chahte hain?")) {
                db.messages = db.messages.filter(m => m.id !== msgId);
                saveDB();
                closeMessageDetailModal();
                renderMessagesInbox();
                alert("Message successfully delete kar diya gaya hai!");
            }
        }

        function openCreatorDashboard() {
            let modal = document.getElementById('creatorModal');
            let reqView = document.getElementById('subscriptionRequiredView');
            let actView = document.getElementById('creatorActionView');

            if (checkUserHasActiveSub()) {
                reqView.classList.add('hidden');
                actView.classList.remove('hidden');
            } else {
                reqView.classList.remove('hidden');
                actView.classList.add('hidden');
            }
            modal.classList.remove('hidden');
        }

        function closeCreatorModal() { document.getElementById('creatorModal').classList.add('hidden'); }
        
        function openMatchModal() { 
            closeCreatorModal(); 
            document.getElementById('matchModalTitle').innerText = "🏏 Create Match Schedule";
            document.getElementById('editingMatchId').value = "";
            document.getElementById('matchTeam1').value = "";
            document.getElementById('matchTeam2').value = "";
            document.getElementById('matchFormat').value = "";
            document.getElementById('matchDateTime').value = "";
            document.getElementById('matchVenue').value = "";
            document.getElementById('matchGateTime').value = "";
            document.getElementById('matchCode6').value = "";
            document.getElementById('matchResultMargin').value = "";
            document.getElementById('matchResultStatus').value = "Upcoming";
            toggleResultMarginInput('match');
            populateExistingSeriesDropdown('match');
            toggleSeriesInput('match');
            updateTossTeamDropdowns('match');
            document.getElementById('matchModal').classList.remove('hidden'); 
        }
        function closeMatchModal() { document.getElementById('matchModal').classList.add('hidden'); }
        
        function openInternationalMatchModal() { 
            if (currentMobile !== db.settings.adminNumber) return;
            document.getElementById('intModalTitle').innerText = "🌍 Create International Match (Admin Only)";
            document.getElementById('editingIntMatchId').value = "";
            document.getElementById('intTeam1').value = "";
            document.getElementById('intTeam2').value = "";
            document.getElementById('intFormat').value = "";
            document.getElementById('intDateTime').value = "";
            document.getElementById('intVenue').value = "";
            document.getElementById('intGateTime').value = "";
            document.getElementById('intPrice').value = "";
            document.getElementById('intLimit').value = "";
            document.getElementById('intCode6').value = "";
            document.getElementById('intResultMargin').value = "";
            document.getElementById('intResultStatus').value = "Upcoming";
            toggleResultMarginInput('int');
            populateExistingSeriesDropdown('int');
            toggleSeriesInput('int');
            updateTossTeamDropdowns('int');
            document.getElementById('internationalMatchModal').classList.remove('hidden'); 
        }
        function closeInternationalMatchModal() { document.getElementById('internationalMatchModal').classList.add('hidden'); }

        function toggleSeriesInput(prefix) {
            let type = document.getElementById(`${prefix}SeriesType`).value;
            let existingContainer = document.getElementById(`${prefix}ExistingSeriesContainer`);
            let newContainer = document.getElementById(`${prefix}NewSeriesContainer`);

            if (type === 'existing') {
                existingContainer.classList.remove('hidden');
                newContainer.classList.add('hidden');
            } else {
                existingContainer.classList.add('hidden');
                newContainer.classList.remove('hidden');
            }
        }

        function updateTossTeamDropdowns(prefix) {
            let t1 = document.getElementById(`${prefix}Team1`).value.trim() || "Team 1";
            let t2 = document.getElementById(`${prefix}Team2`).value.trim() || "Team 2";
            let selectEl = document.getElementById(`${prefix}TossWinner`);
            
            let currentVal = selectEl.value;
            selectEl.innerHTML = `
                <option value="">Toss kisne jeeta?</option>
                <option value="${t1}">${t1}</option>
                <option value="${t2}">${t2}</option>
            `;
            selectEl.value = currentVal;
        }

        function toggleResultMarginInput(prefix) {
            let status = document.getElementById(`${prefix}ResultStatus`).value;
            let container = document.getElementById(`${prefix}ResultMarginContainer`);
            if (status === 'Team 1 Won' || status === 'Team 2 Won') {
                container.classList.remove('hidden');
            } else {
                container.classList.add('hidden');
                document.getElementById(`${prefix}ResultMargin`).value = '';
            }
        }

        function editMatch(matchId) {
            let match = db.matches.find(m => m.id === matchId);
            if (!match) return;

            if (currentMobile !== db.settings.adminNumber) {
                alert("Sirf Admin matches edit kar sakta hai!");
                return;
            }

            if (match.isInternational) {
                document.getElementById('intModalTitle').innerText = "🌍 Edit International Match";
                document.getElementById('editingIntMatchId').value = match.id;
                document.getElementById('intSeriesType').value = "new";
                toggleSeriesInput('int');
                document.getElementById('intSeriesName').value = match.seriesName;
                document.getElementById('intTeam1').value = match.team1;
                document.getElementById('intTeam2').value = match.team2;
                document.getElementById('intFormat').value = match.matchFormat;
                document.getElementById('intDateTime').value = match.dateTime;
                document.getElementById('intVenue').value = match.venue;
                document.getElementById('intGateTime').value = match.gateTime;
                document.getElementById('intPrice').value = match.price;
                document.getElementById('intLimit').value = match.limit;
                document.getElementById('intCode6').value = match.code6;
                
                updateTossTeamDropdowns('int');
                document.getElementById('intTossWinner').value = match.tossWinner || "";
                document.getElementById('intTossChoice').value = match.tossChoice || "";

                document.getElementById('intResultStatus').value = match.resultStatus || "Upcoming";
                toggleResultMarginInput('int');
                document.getElementById('intResultMargin').value = match.resultMargin || "";

                document.getElementById('internationalMatchModal').classList.remove('hidden');
            } else {
                document.getElementById('matchModalTitle').innerText = "🏏 Edit Match Schedule";
                document.getElementById('editingMatchId').value = match.id;
                document.getElementById('matchSeriesType').value = "new";
                toggleSeriesInput('match');
                document.getElementById('matchSeriesName').value = match.seriesName;
                document.getElementById('matchTeam1').value = match.team1;
                document.getElementById('matchTeam2').value = match.team2;
                document.getElementById('matchFormat').value = match.matchFormat;
                document.getElementById('matchDateTime').value = match.dateTime;
                document.getElementById('matchVenue').value = match.venue;
                document.getElementById('matchGateTime').value = match.gateTime;
                document.getElementById('matchCode6').value = match.code6;

                updateTossTeamDropdowns('match');
                document.getElementById('matchTossWinner').value = match.tossWinner || "";
                document.getElementById('matchTossChoice').value = match.tossChoice || "";

                document.getElementById('matchResultStatus').value = match.resultStatus || "Upcoming";
                toggleResultMarginInput('match');
                document.getElementById('matchResultMargin').value = match.resultMargin || "";

                document.getElementById('matchModal').classList.remove('hidden');
            }
        }

        function populateExistingSeriesDropdown(prefix) {
            let selectEl = document.getElementById(`${prefix}ExistingSeriesSelect`);
            let seriesList = [];
            db.matches.forEach(m => {
                if (m.seriesName && !seriesList.includes(m.seriesName)) {
                    seriesList.push(m.seriesName);
                }
            });

            if (seriesList.length === 0) {
                selectEl.innerHTML = '<option value="">Koi existing series nahi hai (New select karein)</option>';
                document.getElementById(`${prefix}SeriesType`).value = 'new';
                toggleSeriesInput(prefix);
            } else {
                let html = '';
                seriesList.forEach(s => {
                    html += `<option value="${s}">${s}</option>`;
                });
                selectEl.innerHTML = html;
            }
        }

        function processMatchResultPayouts(matchId, newStatus) {
            let match = db.matches.find(m => m.id === matchId);
            if (!match) return;

            match.resultStatus = newStatus;

            if (db.bets) {
                db.bets.forEach(bet => {
                    if (bet.matchId === matchId && bet.status === 'Pending') {
                        let bUser = db.users[bet.mobile];
                        let multiplier = 2; 

                        if (bUser && bUser.subscription && new Date().getTime() < bUser.subscription.expiresAt) {
                            if (bUser.subscription.cashbackPercent && bUser.subscription.cashbackPercent > 0) {
                                multiplier = bUser.subscription.cashbackPercent;
                            }
                        }

                        if (newStatus === 'Team 1 Won' && bet.team === match.team1) {
                            let winnings = bet.amount * multiplier;
                            bUser.wallet += winnings;
                            bet.status = `Won (₹${winnings})`;
                        } else if (newStatus === 'Team 2 Won' && bet.team === match.team2) {
                            let winnings = bet.amount * multiplier;
                            bUser.wallet += winnings;
                            bet.status = `Won (₹${winnings})`;
                        } else if (newStatus === 'Draw / Abandoned') {
                            bUser.wallet += bet.amount; 
                            bet.status = 'Refunded';
                        } else {
                            bet.status = 'Lost';
                        }
                    }
                });
            }
        }

        function saveMatchSchedule(isInternational) {
            if (isInternational && currentMobile !== db.settings.adminNumber) {
                alert("International match sirf Admin create kar sakta hai!");
                return;
            }

            let prefix = isInternational ? 'int' : 'match';
            let editingId = document.getElementById(isInternational ? 'editingIntMatchId' : 'editingMatchId').value;
            
            let seriesType = document.getElementById(`${prefix}SeriesType`).value;
            let seriesName = seriesType === 'existing' ? document.getElementById(`${prefix}ExistingSeriesSelect`).value : document.getElementById(`${prefix}SeriesName`).value.trim();
            let newStatus = document.getElementById(`${prefix}ResultStatus`).value;
            let resultMargin = document.getElementById(`${prefix}ResultMargin`).value.trim();
            let tossWinner = document.getElementById(`${prefix}TossWinner`).value;
            let tossChoice = document.getElementById(`${prefix}TossChoice`).value;

            if (editingId) {
                let match = db.matches.find(m => m.id === editingId);
                if (match) {
                    match.seriesName = seriesName;
                    match.team1 = document.getElementById(`${prefix}Team1`).value.trim();
                    match.team2 = document.getElementById(`${prefix}Team2`).value.trim();
                    match.matchFormat = document.getElementById(`${prefix}Format`).value.trim() || "T20I";
                    match.dateTime = document.getElementById(`${prefix}DateTime`).value.trim() || "WED, 17 DEC, 2026 | 7 PM";
                    match.venue = document.getElementById(`${prefix}Venue`).value.trim() || "STADIUM, LUCKNOW";
                    match.gateTime = document.getElementById(`${prefix}GateTime`).value.trim() || "Gate Opens: 2 Hours Before";
                    if (isInternational) {
                        match.price = Number(document.getElementById(`${prefix}Price`).value) || 0;
                        match.limit = Number(document.getElementById(`${prefix}Limit`).value) || 0;
                    }
                    match.code6 = document.getElementById(`${prefix}Code6`).value.trim();
                    match.tossWinner = tossWinner;
                    match.tossChoice = tossChoice;
                    match.resultMargin = resultMargin;

                    processMatchResultPayouts(match.id, newStatus);
                }
                alert("Match successfully update ho gaya!");
            } else {
                let matchObj = {
                    id: 'match_' + Date.now(),
                    creator: currentMobile,
                    isInternational: isInternational,
                    seriesName: seriesName,
                    team1: document.getElementById(`${prefix}Team1`).value.trim(),
                    team2: document.getElementById(`${prefix}Team2`).value.trim(),
                    matchFormat: document.getElementById(`${prefix}Format`).value.trim() || "T20I",
                    dateTime: document.getElementById(`${prefix}DateTime`).value.trim() || "WED, 17 DEC, 2026 | 7 PM",
                    venue: document.getElementById(`${prefix}Venue`).value.trim() || "STADIUM, LUCKNOW",
                    gateTime: document.getElementById(`${prefix}GateTime`).value.trim() || "Gate Opens: 2 Hours Before",
                    price: isInternational ? (Number(document.getElementById(`${prefix}Price`).value) || 0) : 0,
                    limit: isInternational ? (Number(document.getElementById(`${prefix}Limit`).value) || 0) : 0,
                    soldCount: 0,
                    code6: document.getElementById(`${prefix}Code6`).value.trim(),
                    tossWinner: tossWinner,
                    tossChoice: tossChoice,
                    resultMargin: resultMargin,
                    resultStatus: newStatus
                };

                db.matches.push(matchObj);
                processMatchResultPayouts(matchObj.id, newStatus);
                alert("Match successfully publish ho gaya!");
            }

            saveDB();
            if (isInternational) closeInternationalMatchModal();
            else closeMatchModal();
            renderMatches();
            renderActiveTickets();
        }

        function verifyMatchCode() {
            let code = document.getElementById('verifyCodeInput').value.trim();
            let resDiv = document.getElementById('verifyResult');
            let match = db.matches.find(m => m.code6 === code);

            if (!match) {
                resDiv.innerHTML = `<div class="alert-box" style="background:#fadbd8; color:#78281f; padding:12px; border-radius:8px;">Invalid 6-Digit Code!</div>`;
                return;
            }

            resDiv.innerHTML = `
                <div class="alert-box" style="background:#d4efdf; color:#145a32; padding:12px; border-radius:8px;">
                    <strong>Series:</strong> ${match.seriesName}<br>
                    <strong>Match:</strong> ${match.team1} vs ${match.team2} (${match.matchFormat})<br>
                    <strong>Venue:</strong> ${match.venue}<br>
                    <strong>Date:</strong> ${match.dateTime}
                </div>
            `;
        }

        function renderMatches() {
            let intList = document.getElementById('internationalMatchesList');
            let apnaList = document.getElementById('apnaMatchesList');

            let groupMatches = (matchesArr) => {
                let grouped = {};
                matchesArr.forEach(m => {
                    let sName = m.seriesName || 'Other Matches';
                    if (!grouped[sName]) grouped[sName] = [];
                    grouped[sName].push(m);
                });
                return grouped;
            };

            let intGrouped = groupMatches(db.matches.filter(m => m.isInternational));
            let apnaGrouped = groupMatches(db.matches.filter(m => !m.isInternational));

            let buildGroupHTML = (groupedObj) => {
                let finalHTML = '';
                for (let sName in groupedObj) {
                    finalHTML += `<div class="match-card" style="background:#f8fafc; border-left: 6px solid var(--primary); margin-bottom: 25px;"><div class="series-title-bar"><span>🏆 Series: ${sName}</span></div>`;
                    groupedObj[sName].forEach(match => {
                        let isAdmin = (currentMobile === db.settings.adminNumber);
                        let editBtnHTML = isAdmin ? `<button class="btn btn-warning" style="width:auto; padding:4px 10px; font-size:0.85rem;" onclick="editMatch('${match.id}')">✏️ Edit</button>` : '';

                        let tossHTML = '';
                        if (match.tossWinner && match.tossChoice && match.resultStatus === 'Upcoming') {
                            tossHTML = `<div class="toss-display-box">🪙 Toss: <b>${match.tossWinner}</b> won the toss and elected to <b>${match.tossChoice}</b></div>`;
                        }

                        let resultHTML = '';
                        if (match.resultStatus && match.resultStatus !== 'Upcoming') {
                            let marginText = match.resultMargin ? ` (${match.resultMargin})` : '';
                            resultHTML = `<div class="result-display-box">🏆 Result: <b>${match.resultStatus}</b>${marginText}</div>`;
                        }

                        finalHTML += `
                            <div style="background:#fff; border: 1px solid var(--border); border-radius: 10px; padding: 15px; margin-bottom: 12px;">
                                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
                                    <span style="font-size:0.85rem; background:#e2e8f0; padding:2px 8px; border-radius:4px;">Code: ${match.code6}</span>
                                    <div style="display:flex; gap:8px; align-items:center;">
                                        <span style="font-size:0.85rem; color:#666;">Status: <b>${match.resultStatus}</b></span>
                                        ${editBtnHTML}
                                    </div>
                                </div>
                                <div class="match-row">
                                    <div class="team-box">🏏 ${match.team1}</div>
                                    <div class="vs-text"><span>VS</span><span class="match-format-green">${match.matchFormat || 'T20I'}</span></div>
                                    <div class="team-box">${match.team2} 🏏</div>
                                </div>
                                ${tossHTML}
                                ${resultHTML}
                                <div style="font-size:0.95rem; color:#444; margin-bottom:6px;">📍 <strong>Venue:</strong> ${match.venue}</div>
                                <div style="font-size:0.95rem; color:#444; margin-bottom:10px;">📅 <strong>Date/Time:</strong> ${match.dateTime}</div>
                            </div>
                        `;
                    });
                    finalHTML += `</div>`;
                }
                return finalHTML;
            };

            intList.innerHTML = buildGroupHTML(intGrouped) || '<p>Koi International match nahi hai.</p>';
            apnaList.innerHTML = buildGroupHTML(apnaGrouped) || '<p>Koi apna schedule create nahi kiya gaya hai.</p>';
        }

        function buyTicket(matchId) {
            let match = db.matches.find(m => m.id === matchId);
            let user = db.users[currentMobile];

            let finalPrice = match.price;
            let hasSub = checkUserHasActiveSub();

            if (hasSub && user.freeTicketsLeft && user.freeTicketsLeft > 0) {
                user.freeTicketsLeft -= 1;
                finalPrice = 0;
            } else if (hasSub && user.subscription && user.subscription.discountPercent) {
                let disc = user.subscription.discountPercent;
                finalPrice = Math.round(match.price * (100 - disc) / 100);
            }

            if (user.wallet < finalPrice) { alert("Wallet balance kam hai!"); return; }

            user.wallet -= finalPrice;
            match.soldCount += 1;
            db.tickets.push({
                id: 'tkt_' + Date.now(),
                matchId: match.id,
                mobile: currentMobile,
                pricePaid: finalPrice,
                status: 'Active',
                usedForBet: false
            });

            saveDB();
            updateHeader();
            renderActiveTickets();
            renderMyPurchasedTickets();
            alert(finalPrice === 0 ? "Free ticket successfully claim ho gayi!" : "Ticket successfully buy ho gayi! Ab aap isse satta laga sakte hain.");
        }

        function openBettingModal(matchId) {
            activeBetMatchId = matchId;
            let match = db.matches.find(m => m.id === matchId);
            if (!match) return;

            // Check if user has active unused tickets for this match
            let availableTickets = db.tickets.filter(t => t.mobile === currentMobile && t.matchId === matchId && t.status === 'Active' && !t.usedForBet);
            if (availableTickets.length === 0) {
                alert("Aapke paas is match ke liye koi unused active ticket nahi hai! Pehle Store se ticket buy karein.");
                return;
            }

            document.getElementById('betMatchInfo').innerText = `${match.seriesName} | ${match.team1} vs ${match.team2} (${match.matchFormat})`;
            
            let tktSelect = document.getElementById('betTicketSelect');
            let tktHtml = '';
            availableTickets.forEach(t => {
                tktHtml += `<option value="${t.id}">Ticket ID: ${t.id} (Paid: ₹${t.pricePaid})</option>`;
            });
            tktSelect.innerHTML = tktHtml;

            let selectEl = document.getElementById('betSelectedTeam');
            selectEl.innerHTML = `
                <option value="${match.team1}">${match.team1}</option>
                <option value="${match.team2}">${match.team2}</option>
            `;
            document.getElementById('betAmountInput').value = '';
            document.getElementById('betUpiPinInput').value = '';
            document.getElementById('bettingModal').classList.remove('hidden');
        }

        function closeBettingModal() {
            document.getElementById('bettingModal').classList.add('hidden');
            activeBetMatchId = null;
        }

        function confirmPlaceBet() {
            let tktId = document.getElementById('betTicketSelect').value;
            let amount = Number(document.getElementById('betAmountInput').value);
            let selectedTeam = document.getElementById('betSelectedTeam').value;
            let pinInput = document.getElementById('betUpiPinInput').value.trim();
            let user = db.users[currentMobile];

            if (!tktId) { alert("Kripya ek active ticket select karein!"); return; }
            if (!amount || amount <= 0) { alert("Kripya valid bet amount enter karein!"); return; }
            if (!pinInput || pinInput.length !== 6) { alert("Kripya 6-digit UPI PIN enter karein!"); return; }
            if (user.upiPin && user.upiPin !== pinInput) { alert("Galat UPI PIN enter kiya gaya hai!"); return; }
            if (user.wallet < amount) { alert("Wallet balance kam hai!"); return; }

            let ticketObj = db.tickets.find(t => t.id === tktId);
            if (!ticketObj || ticketObj.usedForBet) {
                alert("Yeh ticket pehle hi use ki ja chuki hai ya invalid hai!");
                return;
            }

            ticketObj.usedForBet = true;
            ticketObj.status = 'Used for Bet';

            user.wallet -= amount;
            if (!db.bets) db.bets = [];
            db.bets.push({
                id: 'bet_' + Date.now(),
                ticketId: tktId,
                matchId: activeBetMatchId,
                mobile: currentMobile,
                team: selectedTeam,
                amount: amount,
                status: 'Pending'
            });

            saveDB();
            updateHeader();
            closeBettingModal();
            renderActiveTickets();
            renderMyPurchasedTickets();
            alert("UPI PIN Verified! Aapka bet successfully lag gaya hai.");
        }

        function renderActiveTickets() {
            let listDiv = document.getElementById('activeTicketsList');
            let userActiveTickets = db.tickets.filter(t => t.mobile === currentMobile && t.status === 'Active' && !t.usedForBet);

            let storeHTML = '<h3>🛍️ Available Matches Store (Buy Tickets)</h3>';
            let storeMatches = db.matches.filter(m => m.isInternational && m.price > 0 && m.resultStatus === 'Upcoming');

            if (storeMatches.length === 0) {
                storeHTML += '<p style="color:#666; margin-bottom:15px;">Filhal store mein koi ticket available nahi hai.</p>';
            } else {
                let hasSub = checkUserHasActiveSub();
                let user = db.users[currentMobile];
                storeMatches.forEach(m => {
                    let displayPrice = m.price;
                    let priceLabel = `₹${m.price}`;
                    let discPercent = (hasSub && user.subscription) ? user.subscription.discountPercent : 0;

                    if (hasSub && user.freeTicketsLeft > 0) {
                        priceLabel = `<b style="color:var(--success);">FREE (${user.freeTicketsLeft} left)</b>`;
                    } else if (hasSub && discPercent > 0) {
                        displayPrice = Math.round(m.price * (100 - discPercent) / 100);
                        priceLabel = `<span style="text-decoration: line-through; color: #888;">₹${m.price}</span> <b style="color:var(--success);">₹${displayPrice} (${discPercent}% Off)</b>`;
                    }
                    storeHTML += `
                        <div style="background:#fff; padding:18px; margin-bottom:14px; border-radius:10px; border:2px solid var(--border); display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:12px;">
                            <div>
                                <strong style="font-size:1.1rem; color:var(--primary);">${m.seriesName}</strong><br>
                                <span style="font-size:1.05rem; font-weight:bold;">${m.team1} vs ${m.team2}</span><br>
                                <small style="color:#666;">${m.matchFormat} | 📍 ${m.venue} | 📅 ${m.dateTime}</small>
                            </div>
                            <div>
                                <button class="btn btn-success" style="padding:10px 18px; width:auto;" onclick="buyTicket('${m.id}')">Buy Ticket - ${priceLabel}</button>
                            </div>
                        </div>
                    `;
                });
            }

            let ticketsHTML = '<h3 style="margin-top:25px;">🎟️ Your Active Tickets</h3>';
            if(userActiveTickets.length === 0) {
                ticketsHTML += '<p style="color:#666;">Aapke paas koi active ticket nahi hai.</p>';
            } else {
                userActiveTickets.forEach(tkt => {
                    let match = db.matches.find(m => m.id === tkt.matchId);
                    if (!match) return;
                    ticketsHTML += `
                        <div class="physical-ticket">
                            <div class="ticket-header"><span>🎫 Series: ${match.seriesName}</span><span>${match.matchFormat}</span></div>
                            <div class="ticket-teams-title">${match.team1} VS ${match.team2}</div>
                            <div style="text-align:center; font-size:1rem; margin-bottom:8px;">📍 ${match.venue} &nbsp;|&nbsp; 📅 ${match.dateTime}</div>
                            <div class="ticket-footer"><span>ID: ${tkt.id}</span><span>Paid: ₹${tkt.pricePaid}</span></div>
                        </div>
                    `;
                });
            }

            listDiv.innerHTML = storeHTML + '<hr style="margin:25px 0;">' + ticketsHTML;
        }

        function deletePurchasedTicket(tktId) {
            if (confirm("Kya aap is ticket ko history se delete karna chahte hain?")) {
                db.tickets = db.tickets.filter(t => t.id !== tktId);
                saveDB();
                renderActiveTickets();
                renderMyPurchasedTickets();
                alert("Ticket successfully delete kar di gayi hai!");
            }
        }

        function deleteBetRecord(betId) {
            if (confirm("Kya aap is bet record ko history se delete karna chahte hain?")) {
                db.bets = db.bets.filter(b => b.id !== betId);
                saveDB();
                renderMyPurchasedTickets();
                alert("Bet history successfully delete kar di gayi hai!");
            }
        }

        function renderMyPurchasedTickets() {
            let listDiv = document.getElementById('myPurchasedList');
            let userTickets = db.tickets.filter(t => t.mobile === currentMobile);
            let userBets = db.bets.filter(b => b.mobile === currentMobile);

            let tktHTML = '<h3>📦 Purchased Tickets & Satta Store</h3>';
            if (userTickets.length === 0) {
                tktHTML += '<p style="color:#666; margin-bottom:20px;">Aapne koi ticket nahi kharidi hai.</p>';
            } else {
                userTickets.forEach(tkt => {
                    let match = db.matches.find(m => m.id === tkt.matchId);
                    let matchName = match ? `${match.team1} vs ${match.team2}` : 'Match';
                    let seriesName = match ? match.seriesName : '';
                    let venue = match ? match.venue : '';
                    let dateTime = match ? match.dateTime : '';
                    let format = match ? match.matchFormat : '';
                    
                    let sattaBtnHTML = '';
                    if (match && match.resultStatus === 'Upcoming' && !tkt.usedForBet) {
                        sattaBtnHTML = `<button class="btn btn-warning" style="margin-top:10px; padding:10px;" onclick="openBettingModal('${match.id}')">🎲 Satta Lagayein (Use Ticket)</button>`;
                    }

                    tktHTML += `
                        <div class="physical-ticket" style="opacity:0.95; margin-bottom:18px;">
                            <div class="ticket-header"><span>Series: ${seriesName}</span><span>${format}</span></div>
                            <div class="ticket-teams-title">${matchName}</div>
                            <div style="text-align:center; font-size:0.95rem; margin-bottom:8px;">📍 ${venue} | 📅 ${dateTime}</div>
                            <div class="ticket-footer"><span>ID: ${tkt.id} (Paid: ₹${tkt.pricePaid})</span><span>Status: ${tkt.status}</span></div>
                            <div style="display:flex; justify-content:space-between; align-items:center; margin-top:10px;">
                                ${sattaBtnHTML}
                                <button class="btn btn-danger" style="width:auto; padding:6px 12px; font-size:0.85rem;" onclick="deletePurchasedTicket('${tkt.id}')">Delete Ticket</button>
                            </div>
                        </div>`;
                });
            }

            let betHTML = '<h3 style="margin-top:25px;">🎲 Bets History</h3>';
            if (userBets.length === 0) {
                betHTML += '<p style="color:#666;">Aapne koi bet nahi lagayi hai.</p>';
            } else {
                userBets.forEach(bet => {
                    let match = db.matches.find(m => m.id === bet.matchId);
                    let matchName = match ? `${match.team1} vs ${match.team2}` : 'Match';
                    let seriesName = match ? match.seriesName : '';
                    let venue = match ? match.venue : '';
                    let dateTime = match ? match.dateTime : '';

                    betHTML += `
                        <div style="background:#fff; border:2px solid var(--border); border-radius:10px; padding:15px; margin-bottom:12px;">
                            <strong>Series:</strong> ${seriesName}<br>
                            <strong>Match:</strong> ${matchName} (${venue} | ${dateTime})<br>
                            <strong>Selected Team:</strong> ${bet.team}<br>
                            <strong>Bet Amount:</strong> ₹${bet.amount}<br>
                            <strong>Status:</strong> <span style="color:var(--secondary); font-weight:bold;">${bet.status}</span><br>
                            <button class="btn btn-danger" style="width:auto; padding:6px 12px; font-size:0.85rem; margin-top:10px;" onclick="deleteBetRecord('${bet.id}')">Delete Bet History</button>
                        </div>
                    `;
                });
            }

            listDiv.innerHTML = tktHTML + '<br>' + betHTML;
        }

        function openMasterAdminPanel() {
            if (currentMobile !== db.settings.adminNumber) return;
            renderAdminAllMatches();
            renderAdminAllTickets();
            renderAdminPlansList();
            document.getElementById('masterAdminModal').classList.remove('hidden');
        }

        function closeMasterAdminPanel() { document.getElementById('masterAdminModal').classList.add('hidden'); }

        function switchAdminSubTab(tabName, evt) {
            document.querySelectorAll('.admin-sub-tab').forEach(el => el.classList.add('hidden'));
            if (tabName === 'matches') document.getElementById('adminTabMatches').classList.remove('hidden');
            if (tabName === 'tickets') document.getElementById('adminTabTickets').classList.remove('hidden');
            if (tabName === 'plans') document.getElementById('adminTabPlans').classList.remove('hidden');
            
            if(evt && evt.target) {
                let parent = evt.target.parentElement;
                parent.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
                evt.target.classList.add('active');
            }
        }

        function renderAdminAllMatches() {
            let container = document.getElementById('adminAllMatchesList');
            let html = '';
            db.matches.forEach(match => {
                html += `
                    <div class="match-card" style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px;">
                        <div><strong>${match.seriesName}</strong> (${match.team1} vs ${match.team2})<br><small>Status: ${match.resultStatus}</small></div>
                        <div style="display:flex; gap:6px;">
                            <button class="btn btn-warning" style="width:auto; padding:6px 12px; font-size:0.9rem;" onclick="closeMasterAdminPanel(); editMatch('${match.id}')">Edit</button>
                        </div>
                    </div>
                `;
            });
            container.innerHTML = html || '<p>Koi match nahi hai.</p>';
        }

        function renderAdminAllTickets() {
            let container = document.getElementById('adminAllTicketsList');
            let html = '';
            db.tickets.forEach(tkt => {
                html += `<div class="match-card"><p><strong>Ticket ID:</strong> ${tkt.id} | User: ${tkt.mobile} | Status: ${tkt.status}</p></div>`;
            });
            container.innerHTML = html || '<p>Koi ticket nahi hai.</p>';
        }

        function renderAdminPlansList() {
            let container = document.getElementById('adminPlansList');
            let html = '';
            db.settings.plans.forEach((plan, index) => {
                let perks = `${plan.freeTickets || 0} Free Tickets + ${plan.discountPercent || 0}% Discount + ${plan.cashbackPercent || 0}x Payout`;
                html += `
                    <div class="match-card" style="padding:12px; margin-bottom:10px; display:flex; justify-content:space-between; align-items:center;">
                        <div>
                            <strong>${plan.name}</strong> - ₹${plan.price} (${plan.durationDays || 30} Days)<br>
                            <small style="color:var(--primary);">Perks: ${perks}</small>
                        </div>
                        <button class="btn btn-danger" style="width:auto; padding:6px 12px; font-size:0.9rem;" onclick="deleteSubscriptionPlan('${plan.id}')">Delete</button>
                    </div>
                `;
            });
            container.innerHTML = html || '<p>Koi plan available nahi hai.</p>';
        }

        function addNewSubscriptionPlan() {
            let id = document.getElementById('newPlanId').value.trim();
            let name = document.getElementById('newPlanName').value.trim();
            let price = Number(document.getElementById('newPlanPrice').value);
            let days = Number(document.getElementById('newPlanDays').value);
            let freeTkt = Number(document.getElementById('newPlanFreeTickets').value) || 0;
            let disc = Number(document.getElementById('newPlanDiscount').value) || 0;
            let cashback = Number(document.getElementById('newPlanCashback').value) || 2;

            if (!id || !name || !price) { alert("Saari zaroori details bharein!"); return; }

            if (db.settings.plans.some(p => p.id === id)) {
                alert("Yeh Plan ID pehle se maujood hai! Koi dusri ID daalein.");
                return;
            }

            db.settings.plans.push({
                id: id,
                name: name,
                price: price,
                durationDays: days || 30,
                freeTickets: freeTkt,
                discountPercent: disc,
                cashbackPercent: cashback
            });
            saveDB();
            renderSubscriptionPlansHub();
            renderAdminPlansList();
            alert("Naya subscription plan successfully add ho gaya!");
        }

        function deleteSubscriptionPlan(planId) {
            if (confirm("Kya aap sach mein is subscription plan ko delete karna chahte hain?")) {
                db.settings.plans = db.settings.plans.filter(p => p.id !== planId);
                saveDB();
                renderSubscriptionPlansHub();
                renderAdminPlansList();
                alert("Subscription plan successfully delete kar diya gaya hai!");
            }
        }

        function switchTab(tabName, evt) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            if (tabName === 'international') document.getElementById('internationalTabContent').classList.remove('hidden');
            if (tabName === 'apna') document.getElementById('apnaTabContent').classList.remove('hidden');
            if (tabName === 'activeTickets') document.getElementById('activeTicketsTabContent').classList.remove('hidden');
            if (tabName === 'myPurchased') document.getElementById('myPurchasedTabContent').classList.remove('hidden');
            if (tabName === 'messages') document.getElementById('messagesTabContent').classList.remove('hidden');

            if(evt && evt.target) {
                document.querySelectorAll('.tabs .tab-btn').forEach(el => el.classList.remove('active'));
                evt.target.classList.add('active');
            }
        }
    </script>
</body>
</html>
